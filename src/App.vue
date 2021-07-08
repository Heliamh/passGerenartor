<template>
  <v-app>
    <v-main>
      <pass-generator/>
    </v-main>
  </v-app>
</template>

<script>
import PassGenerator from "@/components/passGenerator";

export default {
  name: 'App',

  components: {
    PassGenerator,
  },

  data: () => ({
    //
  }),
};
</script>
<style>
@font-face {
  font-family: 'LondonBridge';
  src: url('../src/assets/LondonBridge-Regular.ttf') format('truetype');
}
body{
  font-family: 'LondonBridge';
}
.v-application{
  font-family: 'LondonBridge';
}
</style>
