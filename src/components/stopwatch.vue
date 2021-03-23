<template>
  <div class="flex min-h-screen">
    <div class="m-auto">
      <div class="text-center p-5 text-4xl">
        <span v-if="hours > 0">{{ convertZero(hours) + ':' }}</span>
        <span>{{ convertZero(minutes) + ':' }}</span>
        <span>{{ convertZero(seconds.toFixed(0)) }}</span>
      </div>
      <div>
        <button
          v-on:click="startStopWatch()"
          class="focus:outline-none text-white bg-green-500 p-4 py-3 px-6 rounded-full"
        >
          Start
        </button>
        <button
          v-on:click="stopStopWatch()"
          class="focus:outline-none text-white bg-red-500 p-4 py-3 px-6 rounded-full"
        >
          Stop
        </button>
        <button
          v-if="active != true" 
          v-on:click="clearStopWatch()"
          class="focus:outline-none text-white bg-blue-500 p-4 py-3 px-6 rounded-full"
        >
          Clear
        </button>
        <button
          v-if="active == true" 
          v-on:click="lapStopWatch()"
          class="focus:outline-none text-white bg-blue-500 p-4 py-3 px-6 rounded-full"
        >
          Lap
        </button>
      </div>
      <div class="mt-5 text-center text-xl">
          <ul>
            <li v-for="(lap, index) in laps" :key="index" class="m-3">
              <span v-on:click="laps.splice(index, 1)">
                {{convertZero(lap.hours) + ':' + convertZero(lap.minutes) + ':' + convertZero(lap.seconds.toFixed(0))}}
              </span>
            </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>

import { ref } from "vue";

export default {
  name: "stopwatch",
  setup() {
    var seconds = ref(0);
    var minutes = ref(0);
    var hours = ref(0);
    var active = ref(false);
    var laps = ref([]);
    var interval = ref(null);

    console.log("MOUNTED");
    interval = setInterval(updateStopWatch, 10);
    console.log(laps);

    function convertZero(type) {
      var convStr = type.toString();
      if (convStr.length == 2) {
        return convStr;
      } else {
        return "0" + convStr;
      }
    }

    function startStopWatch() {
      active.value = true;
    }

    function stopStopWatch() {
      active.value = false;
    }

    function clearStopWatch() {
      hours.value = 0;
      minutes.value = 0;
      seconds.value = 0;
    }

    function lapStopWatch() {
      laps.value.push({ hours: hours.value, minutes: minutes.value, seconds: seconds.value });
      console.log(laps);
    }

    function updateStopWatch() {
      if (active.value == true) {
        seconds.value += 0.01;
      }
      if (seconds.value >= 60) {
        seconds.value = 0;
        minutes.value += 1;
      }
      if (minutes.value >= 60) {
        minutes.value = 0;
        hours.value++;
      }
    }

    return {
      seconds,
      minutes,
      hours,
      active,
      laps,
      interval,
      convertZero,
      startStopWatch,
      stopStopWatch,
      clearStopWatch,
      lapStopWatch,
      updateStopWatch,
    }
  },
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
