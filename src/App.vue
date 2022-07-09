<template>
  <navbar class="nav"></navbar>
  <router-view />
</template>

<script>
import NavbarVue from "./components/Navbar.vue";
export default {
  components: {
    navbar: NavbarVue,
  },
};
</script>

<style lang="scss">
:root {
  /*  =============
        Variables
      =============   */
  // Colors
  --color-brand-1: #afc2d5;
  --color-brand-2: #dfefca;
  --color-brand-4: #04724d;
  --color-brand-5: #2b2d42;
  // State Colors
  --color-state-info: #4eb4ff;
  --color-state-success: #17c33d;
  --color-state-warning: #ffcb46;
  --color-state-error: #e42020;
  // Black Colors
  --color-black-1: #000000;
  --color-black-2: #1d1d1d;
  --color-black-3: #24252a;
  --color-white-1: #ffffff;
  --color-white-2: #ededed;
  // Grey Colors
  --color-grey-1: #333333;
  --color-grey-2: #4f4f4f;
  --color-grey-3: #828282;
  --color-grey-4: #bdbdbd;
  --color-grey-5: #e0e0e0;

  // Variable Colors
  --color-object-background: var(--color-white-1);
  --color-body-background: #ccddd370;

  // Typography
  // Font Size
  --header-size-1: 3.5rem;
  --header-size-2: 3rem;
  --header-size-3: 2.5rem;
  --header-size-4: 2rem;
  --header-size-5: 1.5rem;
  --header-size-6: 1.25rem;
  // Text
  --text-size-1: 1.25rem;
  --text-size-2: 1.125rem;
  --text-size-3: 1rem;
  --text-size-4: 0.875rem;
}
.h {
  &-header-1 {
    font-size: var(--header-size-1);
    font-weight: bold;
    color: var(--color-black-3);
  }
  &-header-2 {
    font-size: var(--header-size-2);
    font-weight: bold;
    color: var(--color-black-3);
  }
  &-header-3 {
    font-size: var(--header-size-3);
    font-weight: bold;
    color: var(--color-black-3);
  }
  &-header-4 {
    font-size: var(--header-size-4);
    font-weight: bold;
    color: var(--color-black-3);
  }
  &-header-5 {
    font-size: var(--header-size-5);
    font-weight: bold;
    color: var(--color-black-3);
  }
  &-header-6 {
    font-size: var(--header-size-6);
    font-weight: bold;
    color: var(--color-grey-2);
  }
  &-header--l {
    text-align: left;
  }
}
.t {
  &-text-large {
    font-size: var(--text-size-1);
    color: var(--color-black-3);
  }
  &-text-large-bold {
    font-size: var(--text-size-1);
    font-weight: bold;
    color: var(--color-black-3);
  }
  &-text-medium {
    font-size: var(--text-size-2);
    color: var(--color-black-3);
  }
  &-text-medium-bold {
    font-size: var(--text-size-2);
    font-weight: bold;
    color: var(--color-black-3);
  }
  &-text-normal {
    font-size: var(--text-size-3);
    color: var(--color-black-3);
  }
  &-text-normal-bold {
    font-size: var(--text-size-3);
    font-weight: bold;
    color: var(--color-black-3);
  }
  &-text-small {
    font-size: var(--text-size-4);
    color: var(--color-black-3);
  }
  &-text-small-bold {
    font-size: var(--text-size-4);
    font-weight: bold;
    color: var(--color-black-3);
  }
}
body {
  margin: 0;
  background-color: var(--color-body-background);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
