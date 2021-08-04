<template>
  <div class="calender__wrapper">
    <div class="left__side">
      <h3 class="day__name">{{ currentDayName() }}</h3>
      <h1 class="date">{{ currentDate }}</h1>
    </div>
    <div class="right__side">
      <div class="text-center month">
        {{ currentMonthName }} {{ currentYear }}
      </div>
      <div class="days d-flex text-center flex-wrap">
        <p class="text-danger" v-for="day in days" :key="day">{{ day }}</p>
      </div>
      <div class="dates d-flex text-center flex-wrap">
        <p v-for="day in startingDay()" :key="day"></p>
        <p
          :class="currentDateClass(date)"
          v-for="date in lastDate()"
          :key="date"
        >
          {{ date }}
        </p>
      </div>
      <div class="button-group d-flex justify-content-between px-3">
        <button class="btn btn-lg" @click="prev">Prev</button>
        <button class="btn btn-lg" @click="next">Next</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      days: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
      currentDate: new Date().getDate(),
      currentMonth: new Date().getMonth() + 1,
      currentYear: new Date().getFullYear(),
    };
  },
  computed: {
    currentMonthName() {
      return new Date(
        this.currentYear,
        this.currentMonth - 1
      ).toLocaleString("en-us", { month: "long" });
    },
  },
  methods: {
    lastDate() {
      return new Date(this.currentYear, this.currentMonth, 0).getDate();
    },
    startingDay() {
      return new Date(this.currentYear, this.currentMonth - 1, 1).getDay();
    },
    currentDayName() {
      return new Date(
        new Date().getFullYear(),
        new Date().getMonth(),
        this.currentDate
      ).toLocaleString("en-us", { weekday: "long" });
    },
    currentDateClass(date) {
      const calenderFullDate = new Date(
        this.currentYear,
        this.currentMonth - 1,
        date
      ).toDateString();
      const currentFullDate = new Date().toDateString();
      return calenderFullDate === currentFullDate && "activeDay";
    },
    next() {
      if (this.currentMonth === 12) {
        this.currentMonth = 1;
        this.currentYear++;
      } else {
        this.currentMonth++;
      }
    },
    prev() {
      if (this.currentMonth === 1) {
        this.currentMonth = 12;
        this.currentYear--;
      } else {
        this.currentMonth--;
      }
      console.log(this.currentMonth);
    },
  },
};
</script>

<style>
.calender__wrapper {
  width: 80%;
  height: 700px;
  background: #4ecdc4;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  box-shadow: 0px 0px 17px 0px #1da197;
  display: flex;
}
.left__side,
.right__side {
  width: 50%;
  height: 100%;
  background: #4ecdc4;
}
.left__side {
  text-align: center;
  padding: 10px;
}
.day__name {
  font-size: 50px;
  color: rgba(255, 255, 255, 0.466);
  font-family: Impact, Haettenschweiler, "Arial Narrow Bold", sans-serif;
  margin-top: 50px;
  text-transform: uppercase;
}
.date {
  font-size: 400px;
  color: #fff;
  font-family: Impact, Haettenschweiler, "Arial Narrow Bold", sans-serif;
  font-weight: normal;
}
.right__side {
  background: #fff;
  padding: 10px;
}
.month {
  margin-top: 50px;
  margin-bottom: 50px;
  font-size: 50px;
  color: #4ecdc4;
  font-family: Impact, Haettenschweiler, "Arial Narrow Bold", sans-serif;
  margin-top: 50px;
}
.days p,
.dates p {
  font-weight: bold;
  font-size: 20px;
  text-transform: uppercase;
  width: 14.28%;
}
.dates {
  height: 383px;
}
.button-group button {
  background: #4ecdc4;
  color: #fff;
  font-weight: bold;
}
.activeDay {
  color: #4ecdc4;
  font-weight: bolder;
  font-size: 25px !important;
}
</style>
