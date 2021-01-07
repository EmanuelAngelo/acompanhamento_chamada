<template>
  <v-app>
   

    <v-main>
      <Acomp/>
    </v-main>
  </v-app>
</template>

<script>
import Acomp from './components/Acomp';

export default {
  name: 'App',

  components: {
    Acomp,
  },

  data: () => ({
    //
  }),
};
</script>
