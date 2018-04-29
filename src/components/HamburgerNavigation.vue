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
}
</script>

<style lang="scss">
$purple: rgb(58, 23, 76); //#3a174c
$icon-color: rgb(255, 255, 255); //#ffffff

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
    height: 50px;
    margin-top: 5px;
    margin-bottom: 0;
    position: relative;
    width: 50px;

    &.nav-item--toggle {
      z-index: 9999;
    }

    svg {
      display: block;
      height: 50px;
      margin: 0 auto;
    }

    a, a:link, a:visited, a:hover, a:active {
      color: $icon-color;
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
    margin-top: -50px;
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
    margin-top: -50px;
  }
}

.menu-nav-enter-active {
  animation: menu-expand .2s;
}
@keyframes menu-expand {
  0% {
    margin-bottom: -55px;
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
    margin-bottom: -55px;
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
