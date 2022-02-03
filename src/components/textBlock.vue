<template>
  <div class="tb">
    <h1 class="tb-header">{{ header }}</h1>
    <h2 class="tb-header">{{ subheader }}</h2>
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

h1,
h2 {
  font-family: $fontnormal;
}
h1 {
  color: $whitecolor;
  font-size: 90px;
  font-weight: 500;
  padding: 0 0 0.5em 0;
}
h2 {
  color: $primaryaccentcolor;
  font-size: 36px;
}
</style>
