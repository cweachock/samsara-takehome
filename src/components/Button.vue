<template>
  <button class="button" v-html="text" />
</template>

<script>
export default {
  name: "Button",
  props: {
    text: String,
  },
  methods: {},
};
</script>

<style lang="scss" scoped>
button {
  pointer-events: auto;
  &:hover {
    cursor: pointer;
    opacity: 0.5;
  }
}
</style>
