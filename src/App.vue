<template>
  <div class="app">
    <h1>{{ newdate }}</h1>

    <div class="input-container">
      <p>
        Day: {{ getNewDayOfWeek }} {{ getNewDay }}
        <span v-if="addedDay !== 0">
          {{
            addedDay === 1 ? ` (+ ${addedDay} day)` : ` (+ ${addedDay} days)`
          }}
        </span>
      </p>
      <button @click="handleAddedDay">Add Days</button>
    </div>

    <div class="input-container">
      <p>
        Month: {{ getNewMonth }}
        <span v-if="addedMonth !== 0">
          {{
            addedMonth === 1
              ? ` (+ ${addedMonth} month)`
              : ` (+ ${addedMonth} months)`
          }}
        </span>
      </p>
      <button @click="handleAddedMonth">Add Months</button>
    </div>

    <div class="action-btn">
      <button
        @click="handleChangeDate"
        class="change-btn"
        title="Click to set new date"
      >
        Change Date
      </button>
      <button @click="handleReset" class="reset-btn">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      date: new Date(),
      addedDay: 0,
      addedMonth: 0,
      newdate: this.formatDate(new Date()),
    };
  },
  computed: {
    getNewMonth() {
      const resultDate = this.addMonth(this.addedMonth);
      return resultDate.toLocaleString('default', { month: 'long' });
    },
    getNewDayOfWeek() {
      const resultDate = this.addDay(this.addedDay);
      return resultDate.toLocaleString('default', { weekday: 'long' });
    },
    getNewDay() {
      return this.addDay(this.addedDay).getDate();
    },
  },
  methods: {
    addDay(numberOfDays, baseDate = this.date) {
      const newDate = new Date(baseDate);
      newDate.setDate(newDate.getDate() + numberOfDays);
      return newDate;
    },
    addMonth(numberOfMonths, baseDate = this.date) {
      const newDate = new Date(baseDate);
      newDate.setMonth(newDate.getMonth() + numberOfMonths);
      return newDate;
    },
    formatDate(date) {
      const dayOfWeek = date.toLocaleString('default', { weekday: 'long' });
      const day = date.getDate().toString().padStart(2, '0');
      const month = (date.getMonth() + 1).toString().padStart(2, '0');
      const year = date.getFullYear();
      return `${dayOfWeek} ${day}/${month}/${year}`;
    },
    handleAddedDay() {
      this.addedDay += 1;
    },
    handleAddedMonth() {
      this.addedMonth += 1;
    },
    handleChangeDate() {
      const resultDate = this.addMonth(
        this.addedMonth,
        this.addDay(this.addedDay)
      );
      this.newdate = this.formatDate(resultDate);
    },
    handleReset() {
      this.newdate = this.formatDate(this.date);
      this.addedDay = 0;
      this.addedMonth = 0;
    },
  },
};
</script>

<style scoped>
  :root {
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;

  color-scheme: light dark;
  color: rgba(255, 255, 255, 0.87);
  background-color: #242424;

  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  /* 1rem = 10px(62.5%) */
  font-size: 62.5%;
}

body {
  min-width: 32rem;
  min-height: 100vh;
  font-size: 1.6rem;
  display: flex;
  place-items: center;
  justify-content: center;
  align-items: center;
}

h1 {
  font-size: 2.4rem;
  line-height: 1.1;
}

button {
  border-radius: 8px;
  border: 1px solid transparent;
  padding: 0.6rem 1.2rem;
  margin-top: 0.4rem;
  font-size: 1.2rem;
  font-weight: 500;
  font-family: inherit;
  background-color: #1a1a1a;
  cursor: pointer;
  transition: border-color 0.25s;
}

button:hover {
  border-color: #646cff;
}

button:focus,
button:focus-visible {
  outline: 4px auto -webkit-focus-ring-color;
}

#app {
  padding: 2rem;
  text-align: center;
}

.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2rem;
}

.action-btn {
  display: flex;
  gap: 2rem;
}


.action-btn > button {
  width: 14rem;
  height: 3.2rem;
}

.change-btn {
  background-color: green;
}

.reset-btn {
  background-color: red;
}

@media (prefers-color-scheme: light) {
  :root {
    color: #213547;
    background-color: #ffffff;
  }

  button {
    background-color: #f9f9f9;
  }
}


</style>
