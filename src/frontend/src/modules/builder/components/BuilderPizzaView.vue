<template>
<div class="content__constructor">
  <div class="pizza" :class="pizzaCssClass" @dragover="onDragOver" @drop="onDrop">
    <div class="pizza__wrapper">

      <div class="pizza__filling" :class="filling.cssClasses" v-for="filling in fillings" :key="filling.name"></div>


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
                    let cssClasses = `pizza__filling--${name}`
                    if (ingredient.count === 2){
                        cssClasses += ' pizza__filling--second'
                    }
                    if (ingredient.count === 3){
                        cssClasses += ' pizza__filling--third'
                    }
                    fillings.push({
                        name,
                        cssClasses
                    })
                }
            }
            // pizza__filling--ananas
            return fillings
        }
    },
    methods: {
        onDragOver(event){
            event.preventDefault()
        },
        onDrop(){
            if (this.builder.draggedIngredientId) {
                let ingredient = this.builder.ingredients.find(item => item.id === this.builder.draggedIngredientId);
                ingredient.count++;
            }
        }
    }

}

</script>