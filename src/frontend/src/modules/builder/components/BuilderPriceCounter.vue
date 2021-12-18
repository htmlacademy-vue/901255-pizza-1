<template>
<div class="content__result">
  <p>Итого: {{ price }} ₽</p>
  <button type="button" class="button" :disabled="!builder.name">Готовьте!</button>
</div>
</template>

<script>
export default{
    props: ['builder'],
    computed: {
        price(){
            let multiplier = this.builder.pizza.sizes.find((size)=>this.builder.size===size.id).multiplier
            let doughPrice = this.builder.pizza.dough.find((dough)=>this.builder.dough===dough.id).price
            let saucePrice = this.builder.pizza.sauces.find(sauce=>this.builder.sauce===sauce.id).price
            let ingredientsPrice = 0
            for (let ingredient of this.builder.ingredients){ 
                ingredientsPrice += ingredient.count * ingredient.price
            }
            return multiplier*(doughPrice+saucePrice+ingredientsPrice)
        }
    }
}
</script>