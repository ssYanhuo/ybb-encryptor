<template>
  <v-app>
    <v-app-bar app color="white">
      <div class="d-flex align-center">
        <v-toolbar-title>YBB Encryptor</v-toolbar-title>
      </div>

      <v-spacer></v-spacer>

      <v-btn
          text @click="showProject">
        <span class="mr-2">GitHub</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <Encryptor/>
    </v-main>
  </v-app>
</template>

<script>
import Encryptor from './components/Encryptor';

export default {
  name: 'App',

  components: {
    Encryptor: Encryptor,
  },

  data: () => ({
    //
  }),
  methods:{
    showProject: function () {
      window.open('https://github.com/ssYanhuo/ybb-encryptor', '_blank')
    }
  }
};
</script>
