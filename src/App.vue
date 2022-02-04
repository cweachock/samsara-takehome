<template>
  <div>
    <header>
      <a :href="headerLink"><Logo /></a>
    </header>
    <main id="SamsaraApp">
      <section class="main-section-01" :class="wrapperClass">
        <div class="main-section-01-container--center">
          <div class="main-section-01-container">
            <TextBlock
              class="main-section-01-container-intro"
              :header="headline"
              :subheader="subheader"
            />
            <ul v-if="device === 'm'" role="list">
              <li
                v-for="(item, i) in featuresList"
                :key="i"
                :class="[index === item.id ? 'active' : 'inactive']"
                ref="featureItem"
              >
                <span class="list-numerator" v-html="listNumerator(item.id)" />
                <p v-html="item.featureName" />
                <Media
                  v-if="item.type === 'modal'"
                  class="main-section-01-container--media"
                  :src="item.media.src"
                  :alt="item.media.src"
                  ref="media"
                  role="button"
                  :aria-label="`view the ${item.featureName} feature`"
                  @click.native="
                    $refs.modal.openModal(
                      item.featureName,
                      item.featureDescription,
                      item.id
                    )
                  "
                />
              </li>
            </ul>
            <ul v-else role="list">
              <li
                v-for="(item, i) in featuresList"
                :key="i"
                :class="[index === item.id ? 'active' : 'inactive']"
                ref="featureItem"
              >
                <span class="list-numerator" v-html="listNumerator(item.id)" />
                <Button
                  v-if="item.type === 'modal'"
                  class="main-section-01-container--button"
                  :text="item.featureName"
                  @click.native="
                    $refs.modal.openModal(
                      item.featureName,
                      item.featureDescription,
                      item.id
                    )
                  "
                />
              </li>
            </ul>
          </div>
          <div class="main-section-01-container" v-if="device === 'd'">
            <Media
              class="main-section-01-container--media"
              :src="src"
              :alt="alt"
              ref="media"
              :aria-label="` view ${featureName} feature`"
              role="button"
              @click.native="
                $refs.modal.openModal(featureName, featureDescription, index)
              "
            />
          </div>
        </div>
      </section>
      <Modal ref="modal">
        <template v-slot:id />
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
import Logo from "@/components/Logo.vue";

export default {
  name: "SamsaraApp",
  data() {
    return {
      headline: data.headline,
      headerLink: data.header.link,
      subheader: data.subheader,
      featuresList: data.featuresList,
      src: data.featuresList[0].media.src,
      alt: data.featuresList[0].media.alt,
      featureName: data.featuresList[0].featureName,
      featureDescription: data.featuresList[0].featureDescription,
      active: false,
      device: null,
      index: 1,
    };
  },
  watch: {
    index() {
      if (this.device === "d") {
        for (let i = 0; i < this.featuresList.length; i++) {
          if (this.index === this.featuresList[i].id) {
            this.src = this.featuresList[i].media.src;
            this.alt = this.featuresList[i].media.alt;
            this.featureName = this.featuresList[i].featureName;
            this.featureDescription = this.featuresList[i].featureDescription;
          }
        }
      }
    },
  },
  components: {
    TextBlock,
    Button,
    Media,
    Modal,
    Logo,
  },
  computed: {
    listClasses() {
      return {
        active: this.active,
        inactive: !this.active,
      };
    },
    wrapperClass() {
      return {
        "device-m": this.device === "m",
        "device-d": this.device === "d",
      };
    },
  },
  methods: {
    onWindowResize() {
      if (window.innerWidth < 640) {
        this.device = "m";
      }
      if (window.innerWidth > 1025) {
        this.device = "d";
      }
    },
    checkActiveState(id) {
      if (this.index === id) {
        this.$nextTick(() => {
          if (this.featuresList[id] !== undefined) {
            this.src = this.featuresList[id].media.src;
          }
        });
        return true;
      }
    },
    rotateFeature() {
      if (this.device === "d") {
        setInterval(
          function () {
            if (this.index !== this.featuresList.length) {
              this.index += 1;
            } else {
              this.index = 1;
            }
          }.bind(this),
          3000
        );
      }
    },
    listNumerator(index) {
      if (index < 10) {
        return "0" + index;
      } else {
        return index;
      }
    },
  },
  mounted() {
    window.addEventListener("resize", this.onWindowResize);
    this.onWindowResize();
    this.rotateFeature();
  },
};
</script>

<style lang="scss" scoped>
@import "@/scss/includes/globals.scss";
@import "./css/reset.css";
@import "@/scss/includes/mixins.scss";

header {
  position: absolute;
  height: 60px;
  width: 60px;
  top: 1em;
  right: 1em;
  z-index: 1;
  a {
    height: 100%;
    display: block;
    position: relative;
    &:hover {
      opacity: 0.75;
    }
  }
}

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

    &.device-m {
      .main-section-01-container--center {
        padding: 0;
      }
      ul {
        display: flex;
        overflow-x: scroll;
        li {
          padding: 0.5em;
          position: relative;
          opacity: 1;
          .list-numerator {
            font-size: 18px;
            padding-left: 0.5em;
            padding-top: 0.5em;
          }
          p {
            position: absolute;
            font-size: 21px;
            left: 2em;
            top: 0.5em;
            color: $whitecolor;
            margin: 0;
            width: min-content;
          }
          img {
            width: 275px;
            margin-top: 2.5em;
          }
        }
      }
    }
    .list-numerator {
      @include fluid-type($small, $large, 40px, 80px);
      color: $whitecolor;
      font-family: $fontnormal;

      @media (min-width: $small) {
        position: absolute;
      }
    }
    &-container {
      button {
        width: 200px;
        margin-left: 7vw;
      }
      &:nth-child(1) {
        max-width: 100%;
        @media (min-width: $small) {
          max-width: 40%;
        }
      }
      &:nth-child(2) {
        max-width: 100%;
        align-self: center;
        padding: 0 2em;
        margin-top: 2em;
        @media (min-width: $small) {
          max-width: 60%;
        }
      }
      li {
        width: max-content;
        padding-bottom: 24px;
        transition: all 300ms ease;
        &.inactive {
          opacity: 0.5;
          &:hover {
            opacity: 1;
          }
        }
        &.active {
          opacity: 1;
        }

        @media (min-width: $small) {
          padding-bottom: 75px;
        }
      }
      &--button {
        font-size: 36px;
        @include fluid-type($small, $large, 21px, 32px);
        font-family: $fontnormal;
        color: $whitecolor;
        background: transparent;
        border: none;
        text-align: left;
      }
      &--media {
        max-width: 400px;
        transition: all 300ms ease;
        &:hover {
          cursor: pointer;
          opacity: 0.7;
        }
        &:active {
          transform: translateY(-5px);
        }
      }
      &--center {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100%;
        max-width: $content-width;
        margin: 0 auto;
        padding: 0 1em;
        @media (min-width: $small) {
          flex-direction: row;
          padding: 0;
        }
      }
      &-intro {
        padding-bottom: 2em;
      }
    }
  }
}
</style>
