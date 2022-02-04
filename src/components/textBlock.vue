<template>
  <div class="tb">
    <h1 class="tb-header">{{ header }}</h1>
    <h2 class="tb-header" v-html="subheader" />
  </div>
</template>

<script>
export default {
  name: "TextBlock",
  props: {
    header: String,
    subheader: String,
  },
};
</script>

<style lang="scss" scoped>
@import "@/scss/includes/globals.scss";
@import "@/scss/includes/mixins.scss";

h1,
h2 {
  font-family: $fontnormal;
  padding-left: 5px;
  @media (min-width: $small) {
    padding-left: 0;
  }
}
h1 {
  color: $whitecolor;
  @include fluid-type($small, $large, 30px, 75px);
  font-weight: 500;
}
h2 {
  color: $primaryaccentcolor;
  @include fluid-type($small, $large, 21px, 26px);
  line-height: 1.3;
  font-weight: 400;
  padding-right: 2em;

  @media (min-width: $small) {
    padding-right: 0;
  }
}
</style>
