<template lang="pug">
    div.article
      div.article__wrapper
        h2.article__title(v-text="$props.title")
        p.article__text(v-text="text")


</template>

<script>
export default {
  name: 'Article',
  props: {
    title: String,
    text: String,
  },
};
</script>


<style scoped lang="scss">

  @font-face {
    font-family: "Bnpp-rounded";
    src: url("../fonts/bnpp-rounded-v2.woff") format("woff");
    font-style: normal;
  }

  @font-face {
    font-family: "Bnpp-rounded-bold";
    src: url("../fonts/bnpp-rounded-bold-v2.woff") format("woff");
    font-style: normal;
  }

.article__wrapper {
  max-width: 824px;
  margin: 0 auto;
}

.article__title {
  font-family: "Bnpp-rounded-bold", Helvetica, Arial, sans-serif;
  font-size: 48px;
  line-height: 1.13;
  color: #000000;
}

.article__text {
  font-size: 32px;
  line-height: 1.25;
  color: #000000;
}

</style>
