<template>
    <ul class="day-in-week">
        <li v-for="day in weekdays" :key="day">
            {{day}}
        </li>
    </ul>
</template>

<script>
    const WEEKDAYS = ["MON","TUE","WED","THU","FRI","SAT","SUN"];
    export default {
        name: 'Weekdays',
        computed: {
            weekdays() {

                return WEEKDAYS
            }
        }
    }
</script>

<style scoped>
.day-in-week {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  font-size: 36px;
}

.day-in-week > * {
  text-align: right;
  padding-right: 5px;
  font-size: 28px;
}
</style>