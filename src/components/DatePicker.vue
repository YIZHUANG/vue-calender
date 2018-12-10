<template>
  <div class='datePicker'>
    <div class='datePicker--content'>
      <div class='datePicker--top'>
        <button @click='toPreviousMonth()' class='arrow datePicker-to-previous-month' />
        <span class='datePicker-month-display'>{{currentMonthYear}}</span>
        <button @click='toNextMonth()' class='arrow datePicker-to-next-month' />
      </div>
      <div class='datePicker--bottom'>
        <div class='datePicker--bottom--days' v-for='dayName in daysNames'>
          <div class='datePicker--bottom--dayName'>
            {{dayName.slice(0,2)}}
          </div>
          <div>
            <div
              class='datePicker--bottom--day'
              v-for='day in correspondDates(dayName)'
              v-bind:class="{
                'datePicker-isSameDay': ifItsSameDay(day.date,currentDate),
                'datePicker-hasPass': ifDateHasPass(day.date)
                }"
              @click='changeDate(day.date)'
              >
              {{day.dayNumber}}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
/* eslint-disable */
import {
  ifDateHasPass,
  ifItsSameDay,
  ifItsSameHour,
  renderDayNames,
  renderDaysInMonth,
  getCurrentWeekNumber
} from "../utils";
export default {
  data() {
    return {
      ifItsSameDay,
      ifDateHasPass
    };
  },
  // propsTypes to do..
  props: [
    "currentDate",
    "daysNames",
    "currentMonthYear",
    "daysInAMonth",
    "changeDate",
    "toPreviousMonth",
    "toNextMonth"
  ],
  computed: {},
  methods: {
    correspondDates(dayName) {
      return this.daysInAMonth.filter(day => day.dayName === dayName);
    }
  }
};
</script>

<style lang='scss' scoped>
.datePicker {
  position: absolute;
  width: 250px;
  max-width: 250px;
  &-month-display {
    color: #000;
    font-weight: bold;
    font-size: 0.944rem;
  }
  &--content {
    margin: 10px;
    padding: 5px;
  }
  &--top {
    display: flex;
    justify-content: space-between;
    background-color: #f0f0f0;
    border-bottom: 1px solid #aeaeae;
    border-top-left-radius: 0.3rem;
    border-top-right-radius: 0.3rem;
    padding: 5px;
  }
  &--bottom {
    display: flex;
    margin-top: 10px;
    justify-content: space-between;
    &--dayName {
      margin-bottom: 5px;
    }
    &--days {
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;
    }
    &--day {
      padding: 2px;
      cursor: pointer;
      &:hover {
        background-color: #f0f0f0;
      }
    }
  }
  &-hasPass {
    background-color: #f0f0f9;
  }
}
.datePicker-to-previous-month {
  border: 0.45rem solid transparent;
  border-right-color: #ccc;
}
.datePicker-to-next-month {
  border: 0.45rem solid transparent;
  border-left-color: #ccc;
}
.arrow {
  height: 10px;
  width: 10px;
  cursor: pointer;
  padding: 0;
  background: none;
}
.datePicker-isSameDay {
  border-radius: 0.3rem;
  background-color: #216ba5;
  color: white;
}
</style>
