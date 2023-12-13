<!-- useDateComposable.vue -->
<script>
import { ref } from 'vue';

export default function useDate() {
  let date = ref(new Date());

  let getDay = () => {
    return date.value.getDay() + 1;
  };

  let getMonth = () => {
    return date.value.getMonth() + 1;
  };

  const addDay = (numberOfDays, mainDate = date.value) => {
    const newDate = new Date(mainDate);
    newDate.setDate(newDate.getDate() + numberOfDays);
    return newDate;
    // N.B if day after adding is greater than the number of days for that month, date returned should be a new month date
  };

  const addMonth = (numberOfMonths, mainDate = date.value) => {
    const newDate = new Date(mainDate);
    newDate.setMonth(newDate.getMonth() + numberOfMonths);
    return newDate;
    // N.B if month after adding is greater than 11, date returned should be a new year
  };

  return { date, getDay, getMonth, addDay, addMonth };
}
</script>
