<template>
    <div class="date-indicator">
        <span @click="selectPreviousMonth">
            {{monthSelected}}
        </span>
    </div>
</template>

<script>

import dayjs from "dayjs";

export default {
    props: {
        dateSelected: {
            type: Object,
            required:true
        }
    },
     methods: {
            selectPreviousMonth() {
                let newDateSelected = dayjs(this.dateSelected).subtract(1, "month");
                this.$emit("selectedDate", newDateSelected);
            }
    },
    computed: {
        monthSelected(){
            return this.dateSelected.format("MMMM YYYY");
        }
    }
};
</script>

<style scoped>
.date-indicator{
    font-size: 36px;
    font-weight: 600;
    font-family: Century Gothic;
    color: #ffa100;
    }
.date-indicator > * {
  cursor: pointer;
  user-select: none;
}
</style>