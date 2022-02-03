<template>
  <div>
    <header></header>
    <main id="SamsaraApp">
      <section class="main-section-01">
        <div class="main-section-01-container--center">
          <div class="main-section-01-container">
            <TextBlock
              class="main-section-01-container-intro"
              :header="headline"
              :subheader="subheader"
            />
            <ul role="list">
              <li v-for="(item, i) in featuresList" :key="i">
                <Button
                  class="main-section-01-container--button"
                  :text="item.feature"
                >
                </Button>
              </li>
            </ul>
          </div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
import TextBlock from "@/components/TextBlock.vue";
import Button from "@/components/Button.vue";
import data from "@/data/data.json";

export default {
  name: "SamsaraApp",
  data() {
    return {
      headline: data.headline,
      subheader: data.subheader,
      featuresList: data.featuresList,
    };
  },
  components: {
    TextBlock,
    Button,
  },
};
</script>

<style lang="scss" scoped>
@import "@/scss/includes/globals.scss";
@import "./css/reset.css";

#SamsaraApp {
  h1,
  h2,
  h3,
  h4,
  h5,
  p {
    font-family: "Rooto", Helvetica, Arial, sans-serif;
  }
  h1,
  h2,
  h3,
  h4,
  h5 {
    font-weight: 700;
  }
  p {
    font-weight: 400;
  }
  .main-section-01 {
    height: 100vh;
    width: 100vw;
    background: $darkcolor;
    &-container {
      &--button {
        font-size: 36px;
        font-family: $fontnormal;
        color: $whitecolor;
        background: transparent;
        border: none;
        padding: 1em 0;
        text-align: left;
      }
      &--center {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100%;
      }
      &-intro {
        padding-bottom: 2em;
      }
    }
  }
}
</style>
