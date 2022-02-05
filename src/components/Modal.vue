<template>
  <transition name="fade">
    <div class="m" v-if="show" :class="wrapperClass" ref="modal">
      <div class="m-modal">
        <div class="m-modal-backdrop" @click="closeModal()" />
        <div class="m-modal-dialog" ref="modaldialog">
          <div class="m-modal-body" ref="modalbody" tabindex="-1">
            <span class="m-modal-numerator" v-if="id" v-html="id" />
            <h1 v-if="header" v-html="header" />
            <span class="header-separator" />
            <p v-if="body" v-html="body" />
            <button
              type="button"
              class="m-modal-close"
              @click="closeModal()"
              aria-label="Close Modal"
              ref="closeicon"
            >
              <span class="icon-close"></span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "Modal",
  data() {
    return {
      show: false,
      previousFocus: null,
      focusableContent: null,
      focusableElements: "button, a",
      body: "",
      header: "",
      id: null,
    };
  },
  computed: {
    wrapperClass() {
      return {
        "m-show": this.show,
        "m-hidden": !this.show,
      };
    },
  },
  methods: {
    keyDown(e) {
      if (e.key === "Tab") {
        if (e.shiftKey) {
          // we are going backward with focus
          if (document.activeElement === this.focusableContent[0]) {
            // we are on the first focusable element
            // so we need to wrap back to the last
            e.preventDefault(); // prevent double tabbing
            this.focusableContent[this.focusableContent.length - 1].focus();
          }
        } else {
          // we are going forward with focus
          if (
            document.activeElement ===
            this.focusableContent[this.focusableContent.length - 1]
          ) {
            // we are on the last focusable element
            // so we need to wrap forward to the first
            e.preventDefault(); // prevent double tabbing
            this.focusableContent[0].focus();
          }
        }
        // if we reach this point, let the "Tab" functionality
        // behave as it normally does, no looping or preventing default.
        // we only care about the wrapping parts
      }
      if (e.key === "Escape") {
        this.closeModal();
      }
    },
    closeModal() {
      this.show = false;
      document.removeEventListener("keydown", this.keyDown);
      document.querySelector("html").classList.remove("modal-active");
      if (this.previousFocus) {
        this.previousFocus.focus();
      }
    },
    openModal(header, body, id) {
      this.show = true;
      if (id < 10) {
        this.id = "0" + id;
      } else {
        this.id = id;
      }
      this.body = body;
      this.header = header;
      this.previousFocus = document.activeElement;
      this.$nextTick(() => {
        this.$refs.modalbody.focus();
        document.addEventListener("keydown", this.keyDown);
        this.focusableContent = this.$refs.modal.querySelectorAll(
          this.focusableElements
        );
      });
      document.querySelector("html").classList.add("modal-active");
    },
  },
  mounted() {},
};
</script>

<style lang="scss" scoped>
@import "@/scss/includes/globals.scss";
@import "@/scss/includes/mixins.scss";

$duration: 1000ms;
$delay: 250ms;
$easing: ease;
.m {
  overflow-x: hidden;
  overflow-y: auto;
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 9;
  height: 0;
  visibility: hidden;
  &-modal {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
    &-numerator {
      font-family: $fontnormal;
      //@include fluid-type(30px, 80px);
      //font-size: min(max(1rem, 4vw), 80px);
      font-size: clamp(30px, 4vw, 80px);
      //@include fluid-type($small, $large, 30px, 80px);
      font-weight: 500;
      color: $primaryaccentcolor;
    }
  }
  &-modal-backdrop {
    background-color: rgba(0, 0, 0, 0.5);
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 1;
    &:hover {
      cursor: pointer;
    }
  }
  &-modal-dialog {
    background-color: $whitecolor;
    position: relative;
    width: 600px;
    height: auto;
    min-height: 400px;
    margin: 50px auto;
    display: flex;
    flex-direction: column;
    border-radius: 5px;
    z-index: 2;
    overflow: hidden;
    @media (max-width: $small) {
      width: 90%;
    }
  }
  &-modal-close {
    background: none;
    position: absolute;
    top: 0.5em;
    right: 0.5em;
    margin: 0.5em;
    border: 0;
    padding: 1em;
    border-radius: 50%;
    transition: all 100ms ease-out;
    background: none;
    z-index: 2;
    transform-origin: center;

    &:hover {
      opacity: 1;
      transform: scale(1.1);
      cursor: pointer;
    }
    .icon-close {
      color: $darkcolor;
      position: absolute;
      right: 0;
      top: 0;
      width: 32px;
      height: 32px;
      opacity: 0.5;
      left: 0;
      bottom: 0;

      &:hover {
        opacity: 1;
        transform: scale(1.1);
        cursor: pointer;
      }
      &:before,
      &:after {
        position: absolute;
        left: 15px;
        content: " ";
        height: 33px;
        width: 2px;
        background-color: $darkcolor;
      }
      &:before {
        transform: rotate(45deg);
      }
      &:after {
        transform: rotate(-45deg);
      }
    }
  }
  &-modal-body {
    padding: 30px 20px;
    padding-top: 60px;
    overflow: auto;
    display: flex;
    flex-direction: column;
    align-items: stretch;
    height: 100%;

    h1 + .header-separator {
      width: 70px;
      height: 1px;
      margin-top: 1em;
      background: $darkcolor;
    }

    h1,
    h2,
    p {
      font-family: $fontnormal;
      color: $darkcolor;
    }
    h1,
    h2 {
      font-family: $fontnormal;
      //@include fluid-type(30px, 40px);
      //font-size: min(max(1rem, 4vw), 40px);
      font-size: clamp(30px, 4vw, 40px);
      // @include fluid-type($small, $large, 30px, 40px);
      font-weight: 500;
      color: $darkcolor;
    }
    p {
      //@include fluid-type(18px, 21px);
      //font-size: min(max(1rem, 4vw), 21px);
      font-size: clamp(18px, 4vw, 21px);
      //@include fluid-type($small, $large, 18px, 21px);
      font-weight: 400;
      line-height: 1.4;
      margin-top: 1em;
    }
  }
}
.m-show {
  height: auto;
  visibility: visible;
  z-index: 9999;
}
.m-hidden {
  height: 0;
  visibility: hidden;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
