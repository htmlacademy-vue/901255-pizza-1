<template>
<div class="counter">
  <button type="button" class="counter__button counter__button--minus" @click="minusClick" :disabled="ingredient.count===0">
    <span class="visually-hidden">Меньше</span>
  </button>

  <input type="text" name="counter" class="counter__input" v-model.number="ingredient.count">

  <button type="button" class="counter__button counter__button--plus" @click="plusClick" :disabled="!canIncrease">
    <span class="visually-hidden">Больше</span>
  </button>
</div>
</template>

<script>
export default {
  props: ['ingredient'],
  methods: {
    minusClick(){
      this.ingredient.count--;
    },
    plusClick(){
      this.ingredient.count++;
    },
  },
  computed: {
    canIncrease(){
      return this.ingredient.count < 3
    }
  }
}
</script>

<style></style>