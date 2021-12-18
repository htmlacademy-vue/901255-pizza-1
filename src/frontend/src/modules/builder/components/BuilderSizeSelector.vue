<template>
<div class="content__diameter">
  <div class="sheet">
    <h2 class="title title--small sheet__title">Выберите размер</h2>

    <div class="sheet__content diameter">
      <label class="diameter__input" v-for="(size, index) in builder.pizza.sizes" :key="size.id" :style="`--diameter-size: ${diameterBackgroundSizes[index]}`">
        <input type="radio" name="diameter" :value="size.id" class="visually-hidden" v-model="builder.size">
        <span>{{ size.name }}</span>
      </label>
    </div>
  </div>
</div>
</template>

<script>
export default {
  name: 'BuilderSizeSelector',
  props: ['builder'],
  data(){
    return{
      diameterBackgroundSizes: ['18px', '29px', '100%']
    }
  },
}
</script>

<style>
.diameter__input span::before {
  background-size: var(--diameter-size);
}
</style>