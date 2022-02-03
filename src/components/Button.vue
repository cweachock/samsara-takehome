<template>
  <button class="button" v-html="text" />
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
  },
};
</script>

<style lang="scss" scoped>
button {
  pointer-events: auto;
}
</style>
