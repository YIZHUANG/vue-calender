<template>
  <div class='vue-simple-calendar'>
    <h1>You have selected {{currentDateDetail}}</h1>
    <DatePicker
      :currentDate='currentDate'
      :changeDate='changeDate'
      :selectView='selectView'
      :onShowDatePicker='onShowDatePicker'
      :onDatePickerClick='onDatePickerClick'
      :daysNames='daysNames'
      :daysInAMonth='daysInAMonth'
      :currentMonthYear='currentMonthYear'
      :toPreviousMonth='toPreviousMonth'
      :toNextMonth='toNextMonth'
      v-if='showDatePicker'
      />
  </div>
</template>

<script>
import addMonths from "date-fns/add_months";
import subMonths from "date-fns/sub_months";
import format from "date-fns/format";
import getDate from "date-fns/get_date";

import DatePicker from "./DatePicker.vue";

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
      showDatePicker: true,
      currentDate: new Date(),
      selectedView: "monthly"
    };
  },
  components: {
    DatePicker
  },
  methods: {
    selectView(view) {
      this.selectView = view;
    },
    changeDate(date) {
      this.currentDate = date;
    },
    onShowDatePicker() {
      this.showDatePicker !== this.showDatePicker;
    },
    onDatePickerClick(view, date) {},
    toPreviousMonth() {
      this.currentDate = subMonths(this.currentDate, 1);
    },
    toNextMonth() {
      this.currentDate = addMonths(this.currentDate, 1);
    }
  },
  computed: {
    daysNames() {
      return renderDayNames(this.currentDate);
    },
    daysInAMonth() {
      return renderDaysInMonth(this.currentDate);
    },
    currentMonthYear() {
      return format(this.currentDate, "MMMM YYYY");
    },
    currentDateDetail() {
      const dayFormat = "dddd";
      const dayName = format(this.currentDate, dayFormat);
      const dayNumber = getDate(this.currentDate);
      return `${this.currentMonthYear} ${dayName} ${dayNumber}`;
    }
  }
};
</script>

<style lang='scss' scoped>
.vue-simple-calendar {
  position: relative;
}
</style>
