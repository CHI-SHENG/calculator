<template>
  <v-main>
    <v-container>
      <v-row justify="center">
          <v-col cols="6" class="text-center">
              <v-card>  
              </v-card>
          </v-col>
      </v-row>
      <v-row justify="center">
        <v-col cols="5" class="text-center">
          <v-card color="brown">
            <input class="display" v-model="current">
            <v-row>
              <v-col cols="3">
                <v-btn fab dark @click="clear">C</v-btn>
              </v-col>
              <v-col cols="3">
                <v-btn fab dark @click="sign">+/-</v-btn>
              </v-col>
              <v-col cols="3">
                <v-btn fab dark @click="percent">%</v-btn>
              </v-col>
              <v-col cols="3">
                <v-btn fab dark color="orange" @click="divide"  >/</v-btn>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="3">
                <v-btn fab dark color="grey" @click="append('7')">7</v-btn>
              </v-col>
              <v-col cols="3">
                <v-btn fab dark color="grey" @click="append('8')">8</v-btn>
              </v-col>
              <v-col cols="3">
                <v-btn fab dark color="grey" @click="append('9')">9</v-btn>
              </v-col>
              <v-col cols="3">
                <v-btn fab dark color="orange" @click="multiply">x</v-btn>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="3">
                <v-btn fab dark color="grey" @click="append('4')">4</v-btn>
              </v-col>
              <v-col cols="3">
                <v-btn fab dark color="grey" @click="append('5')">5</v-btn>
              </v-col>
              <v-col cols="3">
                <v-btn fab dark color="grey" @click="append('6')">6</v-btn>
              </v-col>
              <v-col cols="3">
                <v-btn fab dark color="orange" @click="minus">-</v-btn>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="3">
                <v-btn fab dark color="grey" @click="append('1')">1</v-btn>
              </v-col>
              <v-col cols="3">
                <v-btn fab dark color="grey" @click="append('2')">2</v-btn>
              </v-col>
              <v-col cols="3">
                <v-btn fab dark color="grey" @click="append('3')">3</v-btn>
              </v-col>
              <v-col cols="3">
                <v-btn fab dark color="orange" @click="plus">+</v-btn>
              </v-col>
            </v-row>
            <v-row>
              <v-col cols="6">
                <v-btn rounded x-large dark color="grey" @click="append('0')" width="80%">0</v-btn>
              </v-col>
              <v-col cols="3">
                <v-btn fab dark color="grey" @click="dot">.</v-btn>
              </v-col>
              <v-col cols="3">
                <v-btn fab dark color="orange" @click="equal">=</v-btn>
              </v-col>
            </v-row>
          </v-card>
        </v-col>
      </v-row>  
    </v-container>
  </v-main>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      current: "",
      previous: "",
      operator: null,
      operatorClicked: false
    };
  },
  watch: {
    current: {
      immediate: true,
      handler() {

        if (this.current.length > 10) {
          this.current = this.current.slice(0, 10);
        }
      }
    }
  },
  methods: {
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    clear() {
      this.current = "";
      this.operator = null;
      this.operatorClicked = false;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) this.current = "";
      this.operatorClicked = false;
      this.current =
        this.current === "0" ? `${number}` : `${this.current}${number}`;
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      console.log(this.current, this.previous);
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
      this.operator = null;
      this.operatorClicked = false;
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    }
  }
};
</script>

<style>  
.display {
  text-align: right;
  background-color: #D3D3D3;
  color: #333;
  padding: 3px;
  margin-bottom: 10px;
  margin-top: 10px;
  font-size: 36px;
}   
</style>