<template>
  <div id="app">
    <h2 class="title">{{msg}}</h2>
    <count-up class="countup"
       :startVal="+startVal"
       :endVal="+endVal"
       :decimals="+decimals"
       :duration="duration"
       :options="options"></count-up>
    <div class="formbox">
      <div class="ps">＊起始值若大於最終值，則會修正另外一個不是正在編輯的＊</div>
      <label for="start">Start Index</label>
      <input class="form-control" id="start" type="text" v-model.number="startVal"/>
      <label for="start">End Index</label>
      <input class="form-control" id="end" type="text" v-model.number="endVal"/>
      <label for="dec">Decimals</label>
      <input class="form-control" id="dec" type="text" v-model.number="decimals"/>
    </div>
    <hr>
    <div class="formCheckBox">
      <label for="easing">useEasing? <span style="color:red;font-weight:600">{{options.useEasing}}</span> </label>
      <input class="form-check-input" id="easing" type="checkbox" v-model="options.useEasing"/>
      <label for="group">useGrouping? <span style="color:red;font-weight:600">{{options.useGrouping}}</span></label>
      <input class="form-check-input" id="group" type="checkbox" v-model="options.useGrouping" />
    </div>
    <hr>
    <div class="formTokenBox">
      <label for="separtor">Seperator</label>
      <input class="form-control token" id="separtor" type="text" v-model="options.separator" />
      <label for="Decimal">Decimal</label>
      <input class="form-control token" id="Decimal" type="text" v-model="options.decimal" />
    </div>
    <hr>
    <div class="formSubStr">
      <label for="pre">Pre-Fix</label>
      <input class="form-control token" id="pre" type="text" v-model="options.prefix" />
      <label for="suf">Suf-Fix</label>
      <input class="form-control token" id="suf" type="text" v-model="options.suffix" />
    </div>
  </div>
</template>

<script type="text/babel">
import ICountUp from "vue-countup-v2";
export default {
  name: "app",
  data() {
    return {
      msg: "CountUp js Template",
      startVal: 20,
      endVal: 2000,
      decimals: 0,
      duration: 2,
      options: {
        useEasing: true,
        useGrouping: true,
        separator: ",",
        decimal: ".",
        prefix: "",
        suffix: ""
      }
    };
  },
  components: {
    "count-up": ICountUp
  },
  mounted() {
    window.oriStr =
      Math.round(
        document.getElementsByClassName("countup")[0].textContent *
          10 ** this.decimals
      ) /
      this.decimals ** 10;
  },
  watch: {
    startVal: function(val) {
      if (val >= this.endVal) this.endVal = val + 100;
    },
    endVal: function(val) {
      if (this.startVal >= val) this.startVal = val - 200;
    },
    decimals: function(n) {
      console.log(n);
      let arr = document
        .getElementsByClassName("countup")[0]
        .textContent.split(".");

      // 都是string
      let int = arr[0];
      let dec = arr[1];

      dec = new Array(n).fill(0).join("");
      let endValue = [int, dec].join(".");
      // string
      document.getElementsByClassName("countup")[0].textContent = endValue;
    },
    "options.decimal": function(val) {
      let str = oriStr + "";
      if (str.match(/\./)) var result = str.replace(".", val);
      document.getElementsByClassName("countup")[0].innerHTML = result;
    },
    "options.separator": function(val) {
      let str = oriStr + "";
      if (str.match(/\./)) var result = str.replace(".", val);
      document.getElementsByClassName("countup")[0].innerHTML = result;
    },
    "options.prefix": function(val) {
      let result = val + oriStr;
      if (this.options.suffix) result += this.options.suffix;
      document.getElementsByClassName("countup")[0].innerHTML = result;
    },
    "options.suffix": function(val) {
      let result = oriStr + val;
      if (this.options.prefix) result = this.options.prefix + result;
      document.getElementsByClassName("countup")[0].innerHTML = result;
    }
  }
};
</script>



<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 80px;
}

.title {
  font-size: 30px;
}
h1,
h2 {
  font-weight: normal;
}
.formbox {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.form-control {
  width: 20%;
  margin-bottom: 30px;
}
.formCheckBox,
.formTokenBox,
.formSubStr {
  display: flex;
  margin: 10px auto;
  justify-content: center;
  align-items: center;
}
.formTokenBox input,
.formSubStr input {
  height: 40px;
}
.formCheckBox input {
  display: none;
  margin: 10px 15px;
  line-height: 1.5em;
}
.formCheckBox label {
  border: #2c3e50 1px solid;
  padding: 20px;
  cursor: pointer;
  width: 400px;
  box-sizing: border-box;
}
.formTokenBox input {
  width: 5%;
  line-height: 1.5em;
}

.formSubStr input {
  width: 7%;
}
input ~ label {
  margin-left: 30px;
}
label ~ input {
  margin-left: 10px;
}
.ps {
  margin-bottom: 30px;
}
hr {
  width: 70%;
}
.countup {
  font-size: 4em;
  margin: 0;
  color: #4d63bc;
}
</style>
