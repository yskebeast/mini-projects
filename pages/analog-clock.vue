<template>
  <fs-project-container title="analog clock">
    <div class="analog-clock">
      <button class="toggle" @click="isTime24 = !isTime24">SWITCH TO {{ timeDisplay }} HOUR</button>
      <div class="main">
        <div class="container">
          <div class="time hour">{{ hour }}</div>
          <span class="colon" :class="tickStyle">:</span>
          <div class="time minute">{{ min }}</div>
          <span class="colon" :class="tickStyle">:</span>
          <div class="time seconds">{{ sec }}</div>
        </div>
        <div class="ampm">
          <div v-if="isTime24">{{ time }}</div>
        </div>
      </div>
    </div>
  </fs-project-container>
</template>

<script>
export default {
  name: "analog-clock",
  data() {
    return {
      hour: null,
      min: null,
      sec: null,
      isTime24: false,
      isTick: false,
    };
  },
  computed: {
    timeDisplay() {
      return this.isTime24 ? 24 : 12;
    },
    tickStyle() {
      return this.isTick && "active";
    },
    time() {
      const currentDate = new Date();
      const hr = currentDate.getHours();
      console.log(hr);
      if (hr < 12) {
        return "AM";
      } else {
        return "PM";
      }
    },
  },
  methods: {
    formatTime(time) {
      return time.toString().padStart(2, "0");
    },
    initClock() {
      const currentDate = new Date();
      const hr = currentDate.getHours();
      const min = currentDate.getMinutes();
      const sec = currentDate.getSeconds();

      this.hour = this.isTime24 && this.formatTime(hr) > 12 ? this.formatTime(hr) % 12 : this.formatTime(hr);
      this.min = this.formatTime(min);
      this.sec = this.formatTime(sec);
      this.isTick = !this.isTick;
      setTimeout(this.initClock, 1000);
    },
  },
  mounted() {
    this.initClock();

    // const hour = document.querySelector(".hour");
    // const minute = document.querySelector(".minute");
    // const seconds = document.querySelector(".seconds");
    // const colon = document.querySelectorAll(".colon");
    // const timeToggle = document.querySelector(".toggle");
    // let isTime24 = false;
    // let isTick = false;
    // timeToggle.addEventListener("click", () => {
    //   isTime24 = !isTime24;
    // });
    // function changeButtonText() {
    //   const text = "switch to : ";
    //   if (isTime24) {
    //     timeToggle.textContent = text + "24 hour";
    //   } else {
    //     timeToggle.textContent = text + "12 hour";
    //   }
    // }
    // function stylingColon() {
    //   isTick = !isTick;
    //   colon.forEach((item) => {
    //     if (isTick) {
    //       item.classList.add("active");
    //     } else {
    //       item.classList.remove("active");
    //     }
    //   });
    // }
    // function formatTime(time) {
    //   return time.toString().padStart(2, "0");
    // }
    // function digitalClock() {
    //   const currentDate = new Date();
    //   const hr = currentDate.getHours();
    //   const min = currentDate.getMinutes();
    //   const sec = currentDate.getSeconds();
    //   const formatHour = formatTime(hr);
    //   const formatMin = formatTime(min);
    //   const formatSec = formatTime(sec);
    //   hour.textContent = isTime24 ? formatHour % 12 : formatHour;
    //   minute.textContent = formatMin;
    //   seconds.textContent = formatSec;
    //   stylingColon();
    //   changeButtonText();
    //   setTimeout(digitalClock, 1000);
    // }
    // window.addEventListener("load", () => {
    //   digitalClock();
    // });
  },
};
</script>

<style lang="scss" scoped>
.analog-clock {
  padding: 3rem 0;
  height: 100vh;
  background-color: #ececec;
}

.main {
  width: 40em;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
}
.container {
  margin: 5rem auto;
  width: 32em;
  height: 8em;
  display: flex;
  align-items: center;
  justify-content: space-around;
  font-weight: 600;
}

.time {
  background-color: #ffffff;
  height: 100%;
  width: 3.2em;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2.5em;
  color: #150c41;
  border-radius: 0.4em;
  box-shadow: 0 1em 2em rgba(0, 0, 0, 0.3);
  letter-spacing: 0.05em;
}

.colon {
  font-weight: 800;
  font-size: 2.5rem;
  color: #ffffff;
  &.active {
    color: #150c41;
  }
}

.toggle {
  margin: 1rem auto 0;
  text-align: center;
  display: block;
  padding: 1rem;
  cursor: pointer;
  font-weight: 600;
  background-color: #ffffff;
  border-radius: 0.4em;
  box-shadow: 0 1em 2em rgba(0, 0, 0, 0.3);
  border: none;
}

.ampm {
  font-size: 2rem;
  width: 45px;
  font-weight: bold;
}
</style>
