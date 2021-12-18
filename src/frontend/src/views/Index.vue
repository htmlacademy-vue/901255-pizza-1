<template>
<AppLayout>
  <main class="content">
    <form action="#" method="post">

      <div class="content__wrapper">
        <h1 class="title title--big">Конструктор пиццы</h1>

        <BuilderDoughSelector :builder="builder"></BuilderDoughSelector>
        <BuilderSizeSelector :builder="builder"></BuilderSizeSelector> 
        <BuilderIngredientsSelector :builder="builder"></BuilderIngredientsSelector>
        

        <div class="content__pizza">
          <label class="input">
            <span class="visually-hidden">Название пиццы</span>
            <input type="text" name="pizza_name" placeholder="Введите название пиццы" v-model="builder.name">
          </label>

          <BuilderPizzaView :builder="builder"></BuilderPizzaView>
          
          <BuilderPriceCounter :builder="builder"></BuilderPriceCounter>
          
        </div>

      </div>

    </form>
  </main>
</AppLayout>

</template>

<script>
import misc from '@/static/misc.json';
import pizza from '@/static/pizza.json';
import user from '@/static/user.json';
import BuilderDoughSelector from '@/modules/builder/components/BuilderDoughSelector.vue';
import BuilderSizeSelector from '@/modules/builder/components/BuilderSizeSelector.vue';
import BuilderIngredientsSelector from '@/modules/builder/components/BuilderIngredientsSelector.vue';
import BuilderPizzaView from '@/modules/builder/components/BuilderPizzaView.vue';
import BuilderPriceCounter from '@/modules/builder/components/BuilderPriceCounter';
import AppLayout from '@/layouts/AppLayout.vue'; 

export default {
    name: 'IndexHome',
    data(){
      for (let ingredient of pizza.ingredients){
        ingredient.count = 0;
      }
      return {
        misc,
        user,
        builder: {
          pizza,
          dough: 1,
          sauce: 1,
          size: 1,
          ingredients: pizza.ingredients,
          name: '',
          draggedIngredientId: null,
        },
      };
    },
    components: {
      BuilderDoughSelector,
      BuilderSizeSelector,
      BuilderIngredientsSelector,
      BuilderPizzaView,
      BuilderPriceCounter,
      AppLayout,
    }
}
</script>

