<template>
<div class="content__ingredients">
  <div class="sheet">
    <h2 class="title title--small sheet__title">Выберите ингредиенты</h2>

    <div class="sheet__content ingredients">

      <div class="ingredients__sauce">
        <p>Основной соус:</p>

        <label class="radio ingredients__input" v-for="sauce in builder.pizza.sauces" :key="sauce.id">
          <input type="radio" name="sauce" :value="sauce.id" v-model="builder.sauce">
          <span>{{ sauce.name }}</span>
        </label>
      </div>

      <div class="ingredients__filling">
        <p>Начинка:</p>

        <ul class="ingredients__list">
          <li class="ingredients__item" v-for="ingredient in builder.ingredients" :key="ingredient.id">
            <span class="filling" :style="`--item-image: url(${ingredient.image})`" :draggable="ingredient.count<3" @dragstart="onIngredientDragStart(ingredient)" @dragend="onIngredientDragEnd">{{ ingredient.name }}</span>


            <ItemCounter class="counter--orange ingredients__counter" :value="ingredient.count" :maxCount="3" @changed="onIngredientChange($event, ingredient)"></ItemCounter>
          </li>
        </ul>

      </div>

    </div>
  </div>
</div>
</template>

<script>
import ItemCounter from '@/common/components/ItemCounter.vue';
export default {
  props: ['builder'],
  components: {
    ItemCounter
  },
  methods: {
    onIngredientDragStart(ingredient){
      this.builder.draggedIngredientId = ingredient.id
    },
    onIngredientDragEnd(){
      this.builder.draggedIngredientId = null
    },
    onIngredientChange(event, ingredient){
      ingredient.count = event
    }
  }
}
</script>

<style>
.filling::before {
  background-image: var(--item-image);
}
.ingredients__item .filling{
  cursor: move;
}
</style>