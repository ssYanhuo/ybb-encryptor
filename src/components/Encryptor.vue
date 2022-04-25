<template>
  <div>
    <v-parallax src="../assets/module-bg-s.png" height="400">
      <div
          style="width: 100%; height: 100%; background-image: linear-gradient(to top, rgba(255, 255, 255, 1) 0%, rgba(255, 255, 255, 0.8) 100%);">
        <v-container>
          <v-row
              align="center"
              justify="center">
            <v-col
                class="text-left"
                cols="10"
                md="11">
              <h1 class="text-h4 font-weight-bold mt-12 black--text text-md-h3">
                <p>YBB加密器</p>
                <p>用字母“Y”和“B”加密你的文本！</p>
              </h1>
            </v-col>
          </v-row>
        </v-container>

      </div>
    </v-parallax>
    <v-container style="margin-top: -200px">
      <v-row justify="center">
        <v-col cols="12">
          <v-card :style="{padding: cardPadding + 'px' }">
            <v-row justify="center">
              <v-col cols="12" md="5">
                <v-textarea height="300" no-resize label="原文本" outlined color="primary" v-model="original"></v-textarea>
              </v-col>
              <v-col cols="12" md="2">
                <center style="line-height: 60px; margin-top: 60px" v-if="!isMobile">
                  <v-btn class="mx-2" color="primary" @click="encrypt"><v-icon>mdi-arrow-right</v-icon>加密</v-btn>
                  <v-btn class="mx-2" color="primary" @click="decrypt"><v-icon>mdi-arrow-left</v-icon>解密</v-btn>
                  <v-btn class="mx-2" :outlined="isCapital" :depressed="!isCapital" @click="isCapital = !isCapital">
                    <v-icon>mdi-format-letter-case</v-icon>{{ isCapital ? '大写' : '小写' }}</v-btn>
                </center>
                <center v-else>
                  <v-btn class="mx-2" color="primary" @click="encrypt"><v-icon>mdi-arrow-down</v-icon>加密</v-btn>
                  <v-btn class="mx-2" color="primary" @click="decrypt"><v-icon>mdi-arrow-up</v-icon>解密</v-btn>
                  <v-btn class="mx-2" :outlined="isCapital" :depressed="!isCapital" @click="isCapital = !isCapital">
                    <v-icon>mdi-format-letter-case</v-icon>{{ isCapital ? '大写' : '小写' }}</v-btn>
                </center>
              </v-col>
              <v-col cols="12" md="5">
                <v-textarea height="300" no-resize label="加密文本" outlined color="primary" v-model="encrypted"></v-textarea>
              </v-col>
            </v-row>
          </v-card>
        </v-col>

      </v-row>
    </v-container>
  </div>

</template>

<script>

export default {
  name: "Encryptor",
  computed: {
    cardPadding() {
      switch (this.$vuetify.breakpoint.name) {
        case "lg":
        case "xl":
        case "md":
          return 48
        case "xs":
          return 16
        default:
          return 32
      }
    },
    isMobile() {
      switch (this.$vuetify.breakpoint.name) {
        case "lg":
        case "xl":
        case "md":
          return false
        default:
          return true
      }
    }
  },
  data: function () {
    return {
      original: '',
      encrypted: '',
      isCapital: false
    };
  },
  methods: {
    str2Ybb: function (str){
      let result = [];
      let list = str.split("");
      for(let i = 0; i < list.length; i ++){
        if(i !== 0){
          result.push(" ");
        }
        let item = list[i];
        let binaryStr = item.charCodeAt(0).toString(2);
        result.push(binaryStr);
      }
      console.log(result.join(""))
      let resultStr = ''
      if(this.isCapital){
        resultStr = result.join("").replaceAll('0', 'Y').replaceAll('1', 'B')
      }
      else {
        resultStr = result.join("").replaceAll('0', 'y').replaceAll('1', 'b')
      }
      return resultStr;
    },
    ybb2Str: function (ybb){
      if(ybb === '') return
      let result = [];
      ybb = ybb.replaceAll('y', '0').replaceAll('b', '1').replaceAll('Y', '0').replaceAll('B', '1')
      let list = ybb.split(" ");
      for(let i = 0; i < list.length; i ++){
        let item = list[i];
        let code = parseInt(item,2);
        let charValue = String.fromCharCode(code);
        result.push(charValue);
      }
      console.log(result)
      return result.join("");
    },
    encrypt: function () {
      this.encrypted = this.str2Ybb(this.original)
    },
    decrypt: function () {
      this.original = this.ybb2Str(this.encrypted)
    }
  },
  mounted() {
  }
}
</script>

<style scoped>
/deep/ .v-parallax__content {
  padding: 0 !important;
}

/deep/ .v-input--selection-controls {
  margin-top: 0 !important;
}
</style>