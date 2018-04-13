<template>
  <div class="iCountUp">
    <ICountUp
      :startVal="startVal"
      :endVal="endVal"
      :decimals="decimals"
      :duration="duration"
      :options="options"
      @onReady="change"
    />
  </div>
</template>

<script type="text/babel">
import ICountUp from "vue-countup-v2";
export default {
  name: "demo",
  props: {
    startVal: {
      type: Number
    },
    endVal: {
      type: Number
    },
    decimals: {
      type: Number
    },
    duration: {
      type: Number
    }
  },
  components: {
    ICountUp
  },
  data() {
    return {
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
  methods: {
    change: function(instance, CountUp) {
      instance.update(parseInt(that.decimals));
    }
  }
};
</script>

