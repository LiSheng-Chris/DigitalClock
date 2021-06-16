<template>
  <div id="clock">
    <div v-if="time" class="seconds">
      <label>Decrement Seconds: </label>
      <input class="input" type="number" v-model="seconds" />
    </div>
    <p class="date">{{ date }}</p>
    <p class="time">{{ time }}</p>
  </div>
</template>

<script>
export default {
  name: "Clock",
  data() {
    return {
      time: "",
      date: "",
      count: 1,
      seconds: 1,
      dateTime: new Date(),
      week: ["SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT"],
    };
  },
  methods: {
    updateTime() {
      var cd = new Date(this.dateTime - this.count++ * this.seconds * 1000);
      this.time =
        this.zeroPadding(cd.getHours(), 2) +
        ":" +
        this.zeroPadding(cd.getMinutes(), 2) +
        ":" +
        this.zeroPadding(cd.getSeconds(), 2);
      this.date =
        this.zeroPadding(cd.getFullYear(), 4) +
        "-" +
        this.zeroPadding(cd.getMonth() + 1, 2) +
        "-" +
        this.zeroPadding(cd.getDate(), 2) +
        " " +
        this.week[cd.getDay()];
    },
    zeroPadding(num, digit) {
      var zero = "";
      for (var i = 0; i < digit; i++) {
        zero += "0";
      }
      return (zero + num).slice(-digit);
    },
  },
  created() {
    this.updateTime();
    this.timerID = setInterval(this.updateTime, 1000);
  },
  watch: {
    seconds: function() {
      this.dateTime = new Date();
      this.count = 0;
    },
  },
  beforeDestroy() {
    clearInterval(this.timerID);
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#clock {
  font-family: "Share Tech Mono", monospace;
  color: #ffffff;
  text-align: center;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  color: #daf6ff;
  text-shadow: 0 0 20px rgba(10, 175, 230, 1), 0 0 20px rgba(10, 175, 230, 0);
}
.time {
  letter-spacing: 0.05em;
  font-size: 80px;
  padding: 5px 0;
}
.date {
  letter-spacing: 0.1em;
  font-size: 24px;
}
.seconds {
  letter-spacing: 0.1em;
  font-size: 24px;
  padding: 20px 0;
}
.input {
  font-size: 24px;
  width: 50px;
  cursor: pointer;
  border-radius: 6px;
}
</style>
