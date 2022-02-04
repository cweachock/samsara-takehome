<template>
  <img :src="`./images/${src}.png`" :alt="alt" />
</template>

<script>
export default {
  name: "Media",
  props: {
    src: {
      type: String,
      required: true,
    },
    alt: {
      type: String,
      default: "",
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
img {
  border-radius: 20px;
  width: 100%;
  position: relative;
}
</style>
