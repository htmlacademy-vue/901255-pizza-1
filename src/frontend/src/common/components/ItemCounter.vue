<template>
<div class="counter">
  <button type="button" class="counter__button counter__button--minus" @click="minusClick" :disabled="count===0">
    <span class="visually-hidden">Меньше</span>
  </button>

  <input type="text" name="counter" class="counter__input" v-model.number="count">

  <button type="button" class="counter__button counter__button--plus" @click="plusClick" :disabled="!canIncrease">
    <span class="visually-hidden">Больше</span>
  </button>
</div>
</template>

<script>
export default {
  props: ['value', 'maxCount'],
  emits: ['changed'],
  data(){
    return {
      'count': this.value,
    }
  },
  methods: {
    minusClick(){
      this.count--;
      this.$emit('changed', this.count)
    },
    plusClick(){
      this.count++;
      this.$emit('changed', this.count)
    },
  },
  computed: {
    canIncrease(){
      return this.count < this.maxCount
    }
  },
  watch: {
    value(){
      this.count = this.value
    }
  }
}
</script>

<style></style>