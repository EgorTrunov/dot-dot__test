<template>
  <Forms />
</template>

<script>
import Forms from '@/components/Forms.vue';

export default {
  name: 'App',
  components: {
    Forms,
  },
};
</script>

<style lang="scss">

body, body:before, body:after, 
*, *:before, *:after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

@font-face {
  font-family: "Helvetica";
  src: url('./assets/fonts/HelveticaNeueRegular.woff');
  font: {
    weight: 400;
  }
}

@font-face {
  font-family: "Helvetica";
  src: url('./assets/fonts/HelveticaNeueBold.woff');
  font: {
    weight: 700;
  }
}

$primary-color: #343539;

body {
  background: $primary-color;
  font-family: Helvetica, sans-serif;
}

#app {
  font-family: Helvetica, sans-serif;
  font-weight: 400;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

</style>
