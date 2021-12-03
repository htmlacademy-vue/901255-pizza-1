<template>
<div>
  <header class="header">
    <div class="header__logo">
      <a href="index.html" class="logo">
        <img src="img/logo.svg" alt="V!U!E! Pizza logo" width="90" height="40">
      </a>
    </div>
    <div class="header__cart">
      <a href="cart.html">0 ₽</a>
    </div>
    <div class="header__user">
      <a href="#" class="header__login"><span>Войти</span></a>
    </div>
  </header>

  <main class="content">
    <form action="#" method="post">

      <div class="content__wrapper">
        <h1 class="title title--big">Конструктор пиццы</h1>

        <div class="content__dough">

          <div class="sheet">
            <h2 class="title title--small sheet__title">Выберите тесто</h2>
            <div class="sheet__content dough">

              <label class="dough__input" :style="`--dough-image: url(${dough.image})`" v-for="dough in pizza.dough" :key="dough.id">
                <input type="radio" name="dought" :value="dough.id" class="visually-hidden" checked>
                <b>{{ dough.name }}</b>
                <span>{{ dough.description }}</span>
              </label>
            </div>

          </div>

        </div>

        <div class="content__diameter">
          <div class="sheet">
            <h2 class="title title--small sheet__title">Выберите размер</h2>

            <div class="sheet__content diameter">
              <label class="diameter__input" v-for="(size, index) in pizza.sizes" :key="size.id" :style="`--diameter-size: ${diameterBackgroundSizes[index]}`">
                <input type="radio" name="diameter" value="size.id" class="visually-hidden" checked>
                <span>{{ size.name }}</span>
              </label>
            </div>
          </div>
        </div>

        <div class="content__ingredients">
          <div class="sheet">
            <h2 class="title title--small sheet__title">Выберите ингредиенты</h2>

            <div class="sheet__content ingredients">

              <div class="ingredients__sauce">
                <p>Основной соус:</p>

                <label class="radio ingredients__input" v-for="sauce in pizza.sauces" :key="sauce.id">
                  <input type="radio" name="sauce" value="tomato" checked>
                  <span>{{ sauce.name }}</span>
                </label>
              </div>

              <div class="ingredients__filling">
                <p>Начинка:</p>

                <ul class="ingredients__list">
                  <li class="ingredients__item" v-for="item in pizza.ingredients" :key="item.id">
                    <span class="filling" :style="`--item-image: url(${item.image})`">{{ item.name }}</span>

                    <div class="counter counter--orange ingredients__counter">
                      <button type="button" class="counter__button counter__button--minus" disabled>
                        <span class="visually-hidden">Меньше</span>
                      </button>
                      <input type="text" name="counter" class="counter__input" value="0">
                      <button type="button" class="counter__button counter__button--plus">
                        <span class="visually-hidden">Больше</span>
                      </button>
                    </div>
                  </li>
                </ul>

              </div>

            </div>
          </div>
        </div>

        <div class="content__pizza">
          <label class="input">
            <span class="visually-hidden">Название пиццы</span>
            <input type="text" name="pizza_name" placeholder="Введите название пиццы">
          </label>

          <div class="content__constructor">
            <div class="pizza pizza--foundation--big-tomato">
              <div class="pizza__wrapper">
                <div class="pizza__filling pizza__filling--ananas"></div>
                <div class="pizza__filling pizza__filling--bacon"></div>
                <div class="pizza__filling pizza__filling--cheddar"></div>
              </div>
            </div>
          </div>

          <div class="content__result">
            <p>Итого: 0 ₽</p>
            <button type="button" class="button" disabled>Готовьте!</button>
          </div>
        </div>

      </div>

    </form>
  </main>
</div>
</template>

<script>
import misc from '@/static/misc.json';
import pizza from '@/static/pizza.json';
import user from '@/static/user.json';

export default {
    name: 'IndexHome',
    data(){
        return {
            misc,
            pizza,
            user,
            diameterBackgroundSizes: ['18px', '29px', '100%']
        };
    },
}
</script>

<style>
    .dough__input b::before {
      background-image: var(--dough-image);
    }

    .diameter__input span::before {
      background-size: var(--diameter-size);
    }

    .filling::before {
      background-image: var(--item-image);
    }

</style>