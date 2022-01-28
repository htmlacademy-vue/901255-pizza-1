<template>
<div class="content__constructor">
  <div class="pizza" :class="pizzaCssClass" @dragover.prevent @drop="onDrop">
    <div class="pizza__wrapper">

      <div class="pizza__filling" :class="filling.cssClasses" v-for="(filling, index) in fillings" :key="index"></div>


    </div>
  </div>
</div>
</template>

<script>
export default{
    props: ['builder'],
    computed: {
        pizzaCssClass(){
            return `pizza--foundation--${this.builder.dough===1 ? 'small' : 'big'}-${this.builder.sauce===1 ? 'tomato' : 'creamy'}`
        },
        fillings(){
            let fillings = []
            for (let ingredient of this.builder.ingredients){
                if (ingredient.count > 0){
                    let name = ingredient.image.substring(ingredient.image.lastIndexOf('/')+1, ingredient.image.lastIndexOf('.'))
                    fillings.push({
                        name, 
                        cssClasses: `pizza__filling--${name}`
                    })

                    if (ingredient.count >= 2){
                        fillings.push({
                            name, 
                            cssClasses: `pizza__filling--${name} pizza__filling--second`
                        })
                    }

                    if (ingredient.count == 3){
                        fillings.push({
                            name, 
                            cssClasses: `pizza__filling--${name} pizza__filling--third`
                        })
                    }

                }
            }
            return fillings
        }
    },
    methods: {
        onDrop(){
            if (this.builder.draggedIngredientId) {
                let ingredient = this.builder.ingredients.find(item => item.id === this.builder.draggedIngredientId);
                ingredient.count++;
            }
        }
    }

}

</script>