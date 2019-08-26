<template>
  <div id="app" class="weeklyNotes grid">
    <div class="ruler grid">
      <div v-for="per in period" v-bind:key="per.id" class="per">{{per}}</div>
      <div v-for="rul in 9" v-bind:key="rul.id" class="rul"></div>
    </div>
    <div class="wrapTable grid">
    <div class="wrappDay">
    <div v-for="day in days" v-bind:key="day.id" class="weeklyDay grid">
          <div class="Day">
            <p>{{ day }}</p>
          </div>
          <div class="daySelectAll"></div>
        </div>
      </div>
      <div class="dayTime grid">
        <div
          v-for="(item, i) in items"
          v-on:click="eventTarget(i)"
          v-bind:key="item.id"
          v-bind:index="i"
          v-bind:data-id="i"
          class="notesItem"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
import AppProgress from '@/components/AppProgress'


export default {

  name: "app",
  data() {
    return {
      maxNumbers: 10,
      itemActive: false,
      items: 168,
      numbers: [],
      days: ["MO", "TU", "WE", "TH", "FR", "SA", "SU"],
      period: [
        "ALL DAY",
        "00:00",
        "03:00",
        "06:00",
        "09:00",
        "12:00",
        "15:00",
        "18:00",
        "21:00"
      ],
      weekJson: {
        mo: [{ bt: 240, et: 779 }],
        tu: [],
        we: [],
        th: [{ bt: 240, et: 779 }, { bt: 1140, et: 1319 }],
        fr: [{ bt: 660, et: 1019 }],
        sa: [{ bt: 0, et: 1439 }],
        su: []
      }
    };
  },
  computed: {

    sum() {
      let sum = 0;
      for (let i = 0; i < this.numbers.length; i++) {
        sum += this.numbers[i];
      }
      return sum;
    },
    btnText() {
      return this.itemActive ? "Hide profit" : "Show profit";
    },
    done() {
      return this.numbers.length >= this.maxNumbers;
    }
  },
  methods: {
        eventTarget(i){
        if(event.target.getAttribute('index') == i){
          event.target.classList.toggle("active");
          console.log(event.target)
        };
    },
    itemFunc(event) {
      this.itemActive = !this.itemActive;
      console.log(event);
    },
    addNumber() {
      if (!this.done) {
        let rnd = Math.floor(Math.random() * 11) - 5;
        this.numbers.push(rnd);
      }
    }
  },
  components: {
    AppProgress
  }
};
</script>

<style>
#app {
  /* font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale; */
  font-weight: bold;
  color: #bbb;
}
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
.grid {
  display: grid;
}
.weeklyNotes {
  justify-content: center;
  grid-template-rows: 65px 1fr;
}
.wrapTable {
  grid-template-columns: 100px auto;
}
.weeklyDay {
  grid-template-columns: 50px 50px;
}
.daySelectAll {
  background-color: #989898;
}
.dayTime {
  grid-template-columns: repeat(24, 30px);
}
.notesItem,
.Day,
.daySelectAll {
  border: 1px solid #c6c6c6;
  border-collapse: collapse;
}

.Day:hover,
.notesItem:hover {
  box-shadow: 0 0 5px #ff0000;
}

.Day {
  text-align: center;
  line-height: 55px;
  user-select: none;
}

.ruler {
  grid-template-columns: 100px repeat(8, 90px);
  grid-template-rows: 50px 15px;
}
.ruler .rul {
  border-left: 1px solid #c6c6c6;
}
.ruler .rul:first-child {
  border: none;
}
.ruler .per {
  align-self: end;
}
.ruler .per:first-child {
  justify-self: end;
  padding-left: 60px;
  grid-row: 1/3;
}
.active {
  background-color: #35a4ff;
}
</style>
