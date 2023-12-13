<template>
  <use-date/>
  <div>
    <div class="container">
      {{ title }}
      <br />
    </div>
    Date: {{ updatedDate }}
    <br />
    Day: {{ getDate() }}
    <br />
    Month: {{ getMonth() }}
    <br />
    <div>
      Add Day:
      <input type="number" v-model.number="daysAddition" style="margin-bottom: 2px;" />
      <br />
      Add Month:
      <input type="number" v-model.number="monthsAddition" />
      <br />
      <button @click="handleChangeDate">
        Change The World
      </button>
    </div>
  </div>
</template>

<script>
import useDate  from './components/useDateMain.vue';
export default {
  name: 'App',
  components: {useDate},
  data() {
    return {
      title: 'Present date:',
      date: new Date(),
      daysAddition: 0,
      monthsAddition: 0,
    };
  },
  computed: {
    updatedDate() {
      return this.handleChangedDate().toString();
    },
  },
  methods: {
    getDate() {
      return this.date.getDate();
    },
    getMonth() {
      return this.date.getMonth() + 1;
    },
    addDay(numberOfDays, mainDate = this.date) {
      const newDate = new Date(mainDate);
      newDate.setDate(newDate.getDate() + numberOfDays);
      return newDate;
    },
    addMonth(numberOfMonths, mainDate = this.date) {
      const newDate = new Date(mainDate);
      newDate.setMonth(newDate.getMonth() + numberOfMonths);
      return newDate;
    },
    handleChange({ target }) {
      const { name, value } = target;
      if (name === 'day') {
        this.daysAddition = parseInt(value);
      }
      if (name === 'month') {
        this.monthsAddition = parseInt(value);
      }
    },
    handleChangedDate() {
      const newDate = this.addMonth(this.monthsAddition, this.addDay(this.daysAddition, this.date));
      return newDate;
    },
    handleChangeDate() {
      this.title = 'Calculated date:';
      this.date = this.handleChangedDate();
    },
  },
};
</script>

<style scoped>
input,
button {
  margin: 2px;
  border-radius: 4px;
  padding: 2px;
}
.container {
  text-align: center;
  font-size: 20px;
  font-weight: 100;
}
</style>
