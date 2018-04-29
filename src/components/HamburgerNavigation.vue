<template>
  <div :class="classes">
    <nav>
      <transition name="menu-nav">
        <div
          v-show="menuExpanded"
          class="menu-nav-items"
        >
          <div
            v-for="(item, key) in navMenuItems"
            :key="key"
          >
            <transition name="fan">
              <div
                v-show="menuExpanded"
                :key="`nav-item-${key}`"
                class="nav-item"
              >
                <a
                  :href="item.url"
                  target="_blank"
                >
                  <span>{{ item.label }}</span>
                  <font-awesome-icon
                    :icon="item.icon"
                    size="3x"
                  />
                </a>
              </div>
            </transition>
          </div>
        </div>
      </transition>
      <div
        class="nav-item"
        @click.stop.prevent="toggleMenu"
      >
        <transition name="scale" mode="out-in">
          <font-awesome-icon
            v-if="menuExpanded"
            key="close"
            :icon="closeIcon"
            size="2x"
          />
          <font-awesome-icon
            v-else-if="!menuExpanded"
            key="menu"
            :icon="menuIcon"
            size="2x"
          />
        </transition>
      </div>
    </nav>
    <transition name="fade">
      <div
        v-if="menuExpanded"
        class="overlay"
        @click.stop.prevent="toggleMenu"
      />
    </transition>
  </div>
</template>

<script>
import { faGithub, faInstagram, faTwitter } from '@fortawesome/fontawesome-free-brands';
import { faFileAlt } from '@fortawesome/fontawesome-free-regular';
import { faTimes, faBars } from '@fortawesome/fontawesome-free-solid';
import FontAwesomeIcon from '@fortawesome/vue-fontawesome';

export default {
  name: 'app',
  components: {
    FontAwesomeIcon,
  },
  props: {
    classes: {
      type: Object,
      default() {
        return {
          navigation: true,
        };
      },
    },
  },
  data() {
    return {
      menuExpanded: false,
      navMenuItems: {
        github: {
          icon: faGithub,
          label: 'GitHub',
          url: 'https://github.com/adrichey',
        },
        twitter: {
          icon: faTwitter,
          label: 'Twitter',
          url: 'https://twitter.com/adrichey',
        },
        instagram: {
          icon: faInstagram,
          label: 'Instagram',
          url: 'https://www.instagram.com/campfirekansas/',
        },
        resume: {
          icon: faFileAlt,
          label: 'Resume',
          url: '/Alan_Richey_Resume.pdf',
        },
      },
    };
  },
  computed: {
    closeIcon() {
      return faTimes;
    },
    menuIcon() {
      return faBars;
    },
  },
  methods: {
    toggleMenu() {
      this.menuExpanded = !this.menuExpanded;
    },
  },
};
</script>

<style lang="scss">
$purple: rgb(58, 23, 76); //#3a174c
$icon-color: rgb(255, 255, 255); //#ffffff
$nav-item-radius: 50px;
$tooltip-height: 32px;

/**
 * Nav Menu Styles
 */
nav {
  bottom: 0;
  margin: 0 15px 15px 0;
  position: fixed;
  right: 0;
  z-index: 9998;

  .nav-item {
    backface-visibility: hidden;
    background-color: $purple;
    border-radius: 50%;
    color: $icon-color;
    cursor: pointer;
    height: $nav-item-radius;
    margin-top: 5px;
    margin-bottom: 0;
    position: relative;
    width: $nav-item-radius;

    &.nav-item--toggle {
      z-index: 9999;
    }

    svg {
      display: block;
      height: $nav-item-radius;
      margin: 0 auto;
    }

    a, a:link, a:visited, a:hover, a:active {
      color: $icon-color;
      display: block;
      font-family: 'Playfair Display', serif;
      position: relative;

      span {
        background-color: $purple;
        border-radius: ($tooltip-height / 8);
        font-size: 1.2em;
        height: $tooltip-height;
        line-height: $tooltip-height;
        margin-right: $nav-item-radius + ($tooltip-height / 4) + 5px;
        margin-top: ($tooltip-height / 4);
        opacity: 0;
        padding: 0 ($tooltip-height / 4);
        position: absolute;
        right: 0;
        top: 0;
        text-align: right;
        transition: opacity .3s ease-in-out;

        // 16px tall arrow
        &:before {
          border-top: ($tooltip-height / 4) solid transparent;
          border-bottom: ($tooltip-height / 4) solid transparent;
          border-left: ($tooltip-height / 4) solid $purple;
          content: '';
          height: 0;
          position: absolute;
          right: -($tooltip-height / 4);
          top: ($tooltip-height / 4);
          width: 0;
        }
      }
    }

    a:hover span {
      opacity: 1;
    }
  }
}

/**
 * Overlay when navigation is expanded
 */
.overlay {
  background-color: lighten($purple, 70%);
  height: 100vh;
  left: 0;
  opacity: 0.8;
  position: fixed;
  top: 0;
  width: 100vw;
  z-index: 9997;
}

/**
 * Animations
 */
.scale-enter-active {
  animation: scale-in .1s;
}
.scale-leave-active {
  animation: scale-out .1s;
}
@keyframes scale-in {
  0% {
    transform: scale(0, 0);
  }
  100% {
    transform: scale(1, 1);
  }
}
@keyframes scale-out {
  0% {
    transform: scale(1, 1);
  }
  100% {
    transform: scale(0, 0);
  }
}

.fade-enter-active {
  animation: fade .3s;
}
.fade-leave-active {
  animation: fade .3s reverse;
}
@keyframes fade {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 0.8;
  }
}

.fan-enter-active {
  animation: fan-out .2s;
}
@keyframes fan-out {
  0% {
    margin-top: -($nav-item-radius);
  }
  100% {
    margin-top: 5px;
  }
}

.fan-leave-active {
  animation: collapse-in .2s;
}
@keyframes collapse-in {
  0% {
    margin-top: 5px;
  }
  100% {
    margin-top: -($nav-item-radius);
  }
}

.menu-nav-enter-active {
  animation: menu-expand .2s;
}
@keyframes menu-expand {
  0% {
    margin-bottom: -($nav-item-radius + 5);
  }
  100% {
    margin-bottom: 0;
  }
}

.menu-nav-leave-active {
  animation: menu-collapse .2s;
}
@keyframes menu-collapse {
  0% {
    margin-bottom: 0px;
  }
  100% {
    margin-bottom: -($nav-item-radius + 5);
  }
}

/**
 * Media Queries
 */
@media (min-width: 768px) {
  nav {
    margin: 0 40px 40px 0;
  }
}
</style>
