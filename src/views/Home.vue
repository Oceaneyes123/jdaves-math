<template>
  <v-container>
    <v-container v-if="noAnswer">
      <v-row class="d-flex justify-center">
        <div class="display-3 font-weight-regular mb-3">JDave Game</div>
      </v-row>
      <v-card class="pa-3 mb-3" color="#42A5F5">
        Choose a random two digit number (e.g. 28).
        <br />Add the two digits (2+8=10).
        <br />Subtract the result from the number (28-10=18).
        <br />Remember the result (18).
        <br />Find the Corresponding Color Below
      </v-card>
      <v-row v-for="(row, rowIndex) in 8" :key="rowIndex">
        <v-col cols="3" md="1" v-for="(column, index) in 12" :key="index">
          <v-card
            :color="populateColor(column + ((row - 1) * 12) -1)"
            class="text-center pa-3"
          >{{column + ((row - 1) * 12)}}</v-card>
        </v-col>
      </v-row>
      <v-row class="d-flex justify-center mt-5">
        <v-col cols="5">
          <v-btn block large color="primary" @click="noAnswer = false">Find Out</v-btn>
        </v-col>
      </v-row>
    </v-container>
    <v-container v-else>
      <v-card :color="colorAnswer" width="100%" height="500" class="text-center">
        <v-row class="d-flex justify-center align-center" style="height:100%">
          <v-col cols="5">
            <p>Is this Your Color?</p>
            <v-btn color="primary" @click="reload()">Try Again</v-btn>
          </v-col>
        </v-row>
      </v-card>
    </v-container>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      noAnswer: true,
      numArray: [],
      colors: [
        "#EF9A9A",
        "#CE93D8",
        "#F48FB1",
        "#9FA8DA",
        "#90CAF9",
        "#80CBC4",
        "#C8E6C9",
        "#E6EE9C",
        "#FFCC80"
      ],

      colorArray: [],

      colorAnswer: ""
    };
  },

  mounted() {
    this.color();
  },

  computed: {},

  methods: {
    color() {
      // this.numArray = [...Array(100)].map(() => {
      //   var num = Math.floor(Math.random() * 8 + 1);
      //   return num;
      // });

      // for (var i = 0; i < 100; i++) {
      //   if ((i + 1) % 9 == 0) {
      //     this.numArray[i] = 9;
      //   }
      // }

      //console.log(this.numArray);

      var temp_num = Math.floor(Math.random() * 8);
      var temp_color = this.colors[temp_num];
      this.colors.splice(temp_num, 1);
      this.colorAnswer = temp_color;

      // console.log(temp_num);
      // console.log(temp_color);
      // console.log(this.colors);

      this.colorArray = [...Array(96)].map(() => {
        var rand_color;

        for (var i = 0; i < 96; i++) {
          rand_color = this.colors[Math.floor(Math.random() * 8)];
        }

        return rand_color;
      });

      for (var i = 0; i < 96; i++) {
        if ((i + 1) % 9 == 0) {
          this.colorArray[i] = temp_color;
        }
      }

      console.log(this.colorArray, "array");
    },

    populateColor(num) {
      setTimeout(() => {}, 1500);

      return this.colorArray[num];
    },

    reload() {
      location.reload();
    }
  }
};
</script>
