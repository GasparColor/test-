<template>
  <div id="app">
    <Article
      :view="article"
    />
  </div>
</template>

<script>
import Article from './components/Article.vue';

export default {
  name: 'app',
  components: {
    Article,
  },
  data: () => ({
    article: {
      title: 'Хорошо, что у меня была страховка!',
      text: 'Большинство людей не считают приобретение страховки каким-то знаковым событием в своей жизни. Да, чаще всего ничего плохого не происходит, и этот тот редкий случай, когда радуешься, что покупкой не пришлось воспользоваться. Но если всё-таки неприятность произошла, лучше, чтобы страховка была. Многие считают, что получить выплату в страховой компании — это сложный квест, но это не так. Вместе с вами мы посмотрим путь двух клиентов, которые купили страховку и позже воспользовались ею. Все обстоятельства и отзывы — реальные.',

      totalList: [
        {
          key: 'Елена',
          value: '«Я получила полную пошаговую поддержку»',
        },
        {
          key: 'Программа',
          value: '«Семейный» (застрахована вся семья, включая детей)',
        },
        {
          key: 'Срок действия',
          value: '12 месяцев с 8 июня 2018 года',
        },
      ],

      operations: [
        {
          date: '8 июня 2018',
          text: 'Елена купила страховку в отделении в Вологде',
          icon: 'cart',
          increment: '',
          decrement: '3000',
        },
        {
          date: '23 июня',
          text: 'Наступил страховой случай: ребенок катался на велосипеде и упал, сломав руку',
          icon: 'injury',
          increment: '',
          decrement: '',
        },
        {
          date: '2 августа',
          text: 'По совету сотрудников Елена позвонила в контактный центр. Там ей объяснили, как заявить о страховом случае через <a href="#" style="text-decoration:none;color:#159e6f">сайт</a>, уточнив, что документы можно направлять частями',
          icon: 'call',
          increment: '',
          decrement: '',
        },
        {
          date: '3 августа',
          text: 'Через сайт от клиента получены документы по страховому случаю',
          icon: 'doc',
          increment: '',
          decrement: '',
        },
        {
          date: '',
          text: 'Елена позвонила в контактный центр, чтобы уточнить, были ли получены ее документы и нужно ли выслать оригиналы Почтой России. Оператор сказал, что для принятия решения будет достаточно копий, направленных через сайт',
          icon: 'call',
          increment: '',
          decrement: '',
        },
        {
          date: '6 августа',
          text: 'Елена позвонила в контактный центр для уточнения статуса обращения',
          icon: 'call',
          increment: '',
          decrement: '',
        },
        {
          date: '',
          text: 'Произведена выплата, при этом страховка продолжает действовать со страховым покрытием <mark style="background-color:transparent; color: #159e6f">240 тыс. рублей</mark> для взрослых и <mark style="background-color:transparent; color: #159e6f">112,5 тыс. рублей</mark> для детей',
          icon: 'money',
          increment: '2500',
          decrement: '',
        },
      ],

      assessment: {
        title: 'Пожалуйста, оцените материал «В центре внимания»',
        buttons: [
          {
            type: 'good',
            text: 'Отлично',
          },
          {
            type: 'normal',
            text: 'Нормально',
          },
          {
            type: 'bad',
            text: 'Плохо',
          },
        ],
      },
    },
  }),
};
</script>

<style lang="scss">
@import "./styles/normalize.css";

@font-face {
  font-family: "Bnpp-rounded";
  src: url("fonts/bnpp-rounded-v2.woff") format("woff");
  font-style: normal;
}

@font-face {
  font-family: "Bnpp-rounded-bold";
  src: url("fonts/bnpp-rounded-bold-v2.woff") format("woff");
  font-style: normal;
}

html {
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
*, *::before, *::after {
  -webkit-box-sizing: inherit;
  box-sizing: inherit;
}

#app {
  font-family: "Bnpp-rounded", Helvetica, Arial, sans-serif;
}
</style>
