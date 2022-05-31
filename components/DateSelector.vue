<template>
    <div class="date-selector">
        <span @click="selectPreviousMonth">Prev| </span>
        <span @click="selectCurrentMonth"> Today| </span>
        <span @click="selectNextMonth">Next </span>
    </div>
</template>

<script>
    import dayjs from "dayjs";

    export default{
        name: "DateSelector",
        props: {
            dateCurrent: {
                type: String,
                required: true
            },
            dateSelected: {
                type: Object,
                required:true
            }
        },
        methods: {
            selectPreviousMonth() {
                let newDateSelected = dayjs(this.dateSelected).subtract(1, "month");
                this.$emit("selectedDate", newDateSelected);
            },
            selectCurrentMonth() {
                let newDateSelected = dayjs(this.dateCurrent);
                this.$emit("selectedDate", newDateSelected);
            },
            selectNextMonth() {
                let newDateSelected = dayjs(this.dateSelected).add(1, "month");
                this.$emit("selectedDate", newDateSelected);
            }
        }
    };
</script>

<style scoped>
.date-selector {
  display: flex;
  font-family: Century Gothic;
  width: 150px;
  color: var(--grey-800);
  font-size: 18px;
}

.date-selector > * {
  cursor: pointer;
  user-select: none;
}
</style>