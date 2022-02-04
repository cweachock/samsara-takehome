<template>
  <div>
    <header>
      <a :href="headerLink"><Logo /></a>
    </header>
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
          <div class="main-section-01-container">
            <Media
              class="main-section-01-container--media"
              :src="src"
              :alt="alt"
              ref="media"
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
      index: 1,
    };
  },
  watch: {
    index() {
      for (let i = 0; i < this.featuresList.length; i++) {
        if (this.index === this.featuresList[i].id) {
          this.src = this.featuresList[i].media.src;
          this.alt = this.featuresList[i].media.alt;
          this.featureName = this.featuresList[i].featureName;
          this.featureDescription = this.featuresList[i].featureDescription;
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
  },
  methods: {
    checkActiveState(id) {
      if (this.index === id) {
        this.$nextTick(() => {
          if (this.featuresList[id] !== undefined) {
            this.src = this.featuresList[id].media.src;
          }
        });
        //console.log(this.$refs.media);
        return true;
      }
    },
    rotateFeature() {
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
    .list-numerator {
      font-size: 100px;
      position: absolute;
      @include fluid-type($small, $large, 30px, 80px);
      color: $whitecolor;
      font-family: $fontnormal;
    }
    &-container {
      button {
        width: 200px;
        margin-left: 7vw;
      }
      &:nth-child(1) {
        max-width: 40%;
      }
      &:nth-child(2) {
        max-width: 60%;
        align-self: center;
        padding: 0 2em;
        margin-top: 2em;
      }
      li {
        padding-bottom: 75px;
        width: max-content;
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
        flex-direction: row;
        align-items: center;
        justify-content: center;
        height: 100%;
        max-width: $content-width;
        margin: 0 auto;
        padding: 0 1em;
      }
      &-intro {
        padding-bottom: 2em;
      }
    }
  }
}
@keyframes logoHoverTransition {
  0% {
    clip-path: polygon(
      -14.99% 102.64%,
      -17.95% 4.13%,
      91.14% -17.77%,
      137.11% 80.61%,
      46.2% 130.11%
    );
  }
  100% {
    clip-path: polygon(
      -0.44% 60.14%,
      -17.95% 4.13%,
      91.14% -17.77%,
      97.11% 53.11%,
      53.47% 80.11%
    );
  }
}
</style>
