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
                <span class="list-numerator" v-html="listNumerator(item.id)" />
                <Button
                  v-if="item.type === 'modal'"
                  class="main-section-01-container--button"
                  :text="item.featureName"
                  @click.native="
                    $refs.modal.openModal(
                      item.featureName,
                      item.featureDescription
                    )
                  "
                />
              </li>
            </ul>
          </div>
          <div class="main-section-01-container">
            <Media
              class="main-section-01-container--media"
              :src="featuresList[0].media.src"
              :alt="featuresList[0].media.alt"
              ref="media"
            />
          </div>
        </div>
      </section>
      <Modal ref="modal">
        <template v-slot:header />
        <template v-slot:body />
      </Modal>
    </main>
  </div>
</template>

<script>
import TextBlock from "@/components/TextBlock.vue";
import Button from "@/components/Button.vue";
import data from "@/data/data.json";
import Media from "@/components/Media.vue";
import Modal from "@/components/Modal.vue";

export default {
  name: "SamsaraApp",
  data() {
    return {
      headline: data.headline,
      subheader: data.subheader,
      featuresList: data.featuresList,
      active: false,
    };
  },
  components: {
    TextBlock,
    Button,
    Media,
    Modal,
  },
  computed: {},
  methods: {
    listNumerator(index) {
      if (index < 10) {
        return "0" + index;
      } else {
        return index;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/scss/includes/globals.scss";
@import "./css/reset.css";
@import "@/scss/includes/mixins.scss";

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
    height: 100%;
    width: 100%;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    .list-numerator {
      font-size: 100px;
      @include fluid-type($small, $large, 30px, 100px);
      color: $whitecolor;
      font-family: $fontnormal;
      padding-right: 0.5em;
    }
    &-container {
      button {
        width: 200px;
      }
      &:nth-child(1) {
        max-width: 70%;
      }
      &:nth-child(2) {
        max-width: 30%;
        align-self: center;
        padding-left: 3em;
        margin-top: 6em;
        padding-right: 2em;
      }
      &--button {
        font-size: 36px;
        @include fluid-type($small, $large, 21px, 32px);
        font-family: $fontnormal;
        color: $whitecolor;
        background: transparent;
        border: none;
        padding: 1em 0;
        text-align: left;
      }
      &--media {
        max-width: 400px;
      }
      &--center {
        display: flex;
        flex-direction: row;
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
