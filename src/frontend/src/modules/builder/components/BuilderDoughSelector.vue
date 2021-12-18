<template>
<div class="content__dough">
  <div class="sheet">
    <h2 class="title title--small sheet__title">Выберите тесто</h2>
    <div class="sheet__content dough">

      <label class="dough__input" :style="`--dough-image: url(${dough.image})`" v-for="dough in builder.pizza.dough" :key="dough.id">
        <input type="radio" name="dought" :value="dough.id" class="visually-hidden" v-model="builder.dough">
        <b>{{ dough.name }}</b>
        <span>{{ dough.description }}</span>
      </label>
    </div>

  </div>

</div>
</template>

<script>
export default{
  name: 'BuilderDoughSelector',
  props: ['builder']
}
</script>

<style>
  .dough__input b::before {
    background-image: var(--dough-image);
  }
</style>