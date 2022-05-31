<template>
    <div class="month">
        <!-- Calendar Header-->
        <div class="month-header">
            <!-- Month Name-->
            <DateIndicator 
            :date-selected = "dateSelected" 
            @selectedDate= "isHidden = !isHidden"
            class = "month-header-selected-month" 
            />
            <!-- Applying Pagination-->
            <DateSelector 
            :current-date="today"
            :dateSelected = "dateSelected"
            @selectedDate= "selectDate"
            />
        </div>
        <div class = "usedForHidding" v-if="!isHidden">
            <!-- Grid Header-->
            <Weekdays /> 
            <!-- Grid-->
            <ul class="grid">  
                <MonthDayItem             
                    v-for="day in days" 
                    :key="day.date" 
                    :day="day" 
                    :Today="day.date === today" 
                />
            </ul> 
         </div> 
         <div class= "displayingMonths" v-if="isHidden">
             <ul class="grid1">  
                <Months />
            </ul>
         </div>
    </div>
</template>

<script>
    import dayjs from "dayjs";
    //Getting Weekdays from dayjs
    import weekday from "dayjs/plugin/weekday";
    //Getting Week Number From dayjs
    import weekOfYear from "dayjs/plugin/weekOfYear";
    import DateIndicator from "./DateIndicator";
    import DateSelector from "./DateSelector";
    import MonthDayItem from "./MonthDayItem";
    import Weekdays from "./Weekdays";
    import Months from "./Months";

    dayjs.extend(weekday);
    dayjs.extend(weekOfYear);

    export default {
        name: "CalendarMonth",

        components: {
            DateIndicator,
            DateSelector,
            MonthDayItem,
            Weekdays,
            Months,
        },
        data(){
            return {
                dateSelected: dayjs(),
                isHidden: false,
            };
        },
        computed: {
            today(){
                return dayjs().format("YYYY-MM-DD");
            },
            days() {
                return [
                    ...this.daysInPreviousMonth,
                    ...this.daysInCurrentMonth,
                    ...this.daysInNextMonth                    
                ];
            },
            month(){
                return Number(this.dateSelected.format("M"));
            },  
            year(){
                return Number(this.dateSelected.format("YYYY"));
            },
            //daysInMonth is a plugIn from dayjs
            daysInAMonth() {
                return dayjs(this.dateSelected).daysInMonth();
            },
            daysInCurrentMonth() {
                return [...Array(this.daysInAMonth)].map((day, index) => {
                    return {
                        date: dayjs(`${this.year}-${this.month}-${index + 1}`).format('YYYY-MM-DD'),
                        CurrentMonth: true
                    };
                });
            },
            //days in previous month that are to be shown in selected month
            daysInPreviousMonth() {
                const firstDayOfTheMonth = this.getWeekday(this.daysInCurrentMonth[0].date);
                const previousMonth = dayjs(`${this.year}-${this.month}-01`).subtract(1, "month");
                //if first day of month is Sunday we do not need to add, so we start from 1
                const visibleDaysFromPreviousMonth = firstDayOfTheMonth ? firstDayOfTheMonth - 1 : 6;
                const lastMondayOfPreviousMonth = dayjs(this.daysInCurrentMonth[0].date).subtract(visibleDaysFromPreviousMonth, "day").date();
                return [...Array(visibleDaysFromPreviousMonth)].map((day, index) => {
                    return {
                        date: dayjs(`${previousMonth.year()}-${previousMonth.month() + 1}-${lastMondayOfPreviousMonth + index}`).format("YYYY-MM-DD"),
                        CurrentMonth:false
                    };
                });
            },
            //days in next month that are to be shown in selected month
            daysInNextMonth() {
                const lastDayOfTheMonth = this.getWeekday(`${this.year}-${this.month}-${this.daysInCurrentMonth.length}`);
                const nextMonth = dayjs(`${this.year}-${this.month}-01`).add(1, "month");
                const visibleDaysFromNextMonth = lastDayOfTheMonth ? 7 - lastDayOfTheMonth : lastDayOfTheMonth;
                return [...Array(visibleDaysFromNextMonth)].map((day, index) => {
                    return {
                        date: dayjs(`${nextMonth.year()}-${nextMonth.month() + 1}-${index + 1}`).format("YYYY-MM-DD"),
                        CurrentMonth: false
                    };
                });
            },
        },
        methods: {
            selectDate(newDateSelected) {
                this.dateSelected = newDateSelected;
            },
            //getting dates from previous month to know what day this month starts
            getWeekday(date){
                return dayjs(date).weekday();
            },
            getMonth(date){
                return dayjs(date).month();
            }
        }
    };
</script>

<style scoped>
.month {
    position: relative;
    border: solid 1px #000000;
}
.month-header{
    position: relative;
    
}
.day-in-week,
.grid {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    list-style-type:none;
    margin-top: 10px;
    padding-left: 0px;
}
.day-in-week {
    color: #000000;
    font-size:10px;
    background-color: #ffffff;
    padding-bottom: 5px;
    padding-top: 5px;
    padding-right: 15px;
}
.day-in-week > * {
    text-align: right;
    padding-right: 5px;
}
.grid,
.grid1 {
    height: 100%;
    position: relative;
    border-top: solid 1px grey;
}
.grid1 > * {
    display: grid;
    list-style-type:none;
    margin-top: 10px;
    padding-bottom: 10px;
    padding-left: 0px;
}
</style>