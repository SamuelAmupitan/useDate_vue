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
.app {
  text-align: center;
  height: 60vh;
  margin: 20px;
  padding: 20px;
  border: 1px solid #3498db;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  background-color: #ecf0f1;
  color: #333;
}

.input-container {
  margin: 10px 0;
}

button {
  margin-top: 10px;
  padding: 10px;
  margin-right: 10px;
  cursor: pointer;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 4px;
  font-size: 14px;
  transition: background-color 0.3s ease;
}

.action-btn {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

.change-btn {
  background-color: #27ae60;
}

.reset-btn {
  background-color: #e74c3c;
}

h1 {
  font-size: 24px;
  color: #3498db;
  margin-bottom: 10px;
}
</style>
