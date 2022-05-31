<template>
    <li class="day" 
        :class="{
            'day-not-today': !day.CurrentMonth,
            'day-today': Today
        }"
    >
    <span>{{label}}</span>
    </li>
</template>

<script>
    import dayjs from "dayjs";
    export default {
        name: "DataItems",
        props: {
            day: {
                type: Object,
                required: true
            },
            Today: {
                type: Boolean,
                default: false
            },
            CurrentMonth: {
                type: Boolean,
                default: false
            }
        },
        computed: {
            label() {
                return dayjs(this.day.date).format("D");
            }
        }
    };
</script>

<style scoped>
.day {
  position: relative;
  min-height: 100px;
  font-size: 36px;
  background-color: white;
  color: #160086;
  padding: 5px;
}

.day > span {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  right: 30px;
  
}

.day-not-today {
  background-color: white;
  color: #00ffc7;
}

.day-today {
  padding-top: 4px;
  background-color: white;
}

.day-today > span {
  color: red;
  
}
</style>