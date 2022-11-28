<template>
  <v-app>
      <Calculator/>
  </v-app>
</template>

<script>
import Calculator from './components/Calculator'
export default {
  name: 'App',
  components:{
    Calculator
  },
  data: () => ({
    //
  }),
};
</script>
