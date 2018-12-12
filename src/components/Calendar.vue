<template>
  <!-- eslint-disable -->
  <div class='vue-simple-calendar'>
    <DatePicker
      :currentDate='currentDate'
      :changeDate='changeDate'
      :selectView='selectView'
      :onShowDatePicker='onShowDatePicker'
      :daysNames='daysNames'
      :daysInAMonth='daysInAMonth'
      :currentMonth='currentMonth'
      :currentYear='currentYear'
      :toPreviousMonth='toPreviousMonth'
      :toNextMonth='toNextMonth'
      :changeMonth='changeMonth'
      :showMonthlyDropdown= 'showMonthlyDropdown'
      :onMonthClick='onMonthClick'
      :changeYear='changeYear'
      :showYearlyDropdown= 'showYearlyDropdown'
      :onYearClick='onYearClick'
      v-if='showDatePicker'
    />
  </div>
</template>

<script>
import addMonths from "date-fns/add_months";
import subMonths from "date-fns/sub_months";
import format from "date-fns/format";
import getDate from "date-fns/get_date";
import setMonth from "date-fns/set_month";
import setYear from "date-fns/set_year";

import DatePicker from "./DatePicker.vue";

import {
  ifDateHasPass,
  ifItsSameDay,
  ifItsSameHour,
  renderDayNames,
  renderDaysInMonth
} from "../utils";

export default {
  data() {
    return {
      showDatePicker: true,
      currentDate: new Date(),
      selectedView: "monthly",
      showMonthlyDropdown: false,
      showYearlyDropdown: false
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
    toPreviousMonth() {
      this.currentDate = subMonths(this.currentDate, 1);
    },
    toNextMonth() {
      this.currentDate = addMonths(this.currentDate, 1);
    },
    changeMonth(month) {
      this.currentDate = setMonth(this.currentDate, month - 1);
    },
    onMonthClick(close = false) {
      if (close) {
        this.showMonthlyDropdown = false;
      } else this.showMonthlyDropdown = !this.showMonthlyDropdown;
      this.showYearlyDropdown = false;
    },
    changeYear(year) {
      this.currentDate = setYear(this.currentDate, year);
    },
    onYearClick(close = false) {
      if (close) {
        this.showYearlyDropdown = false;
      } else this.showYearlyDropdown = !this.showYearlyDropdown;
      this.showMonthlyDropdown = false;
    }
  },
  computed: {
    daysNames() {
      return renderDayNames(this.currentDate);
    },
    daysInAMonth() {
      return renderDaysInMonth(this.currentDate);
    },
    currentMonth() {
      return format(this.currentDate, "MMMM");
    },
    currentYear() {
      return format(this.currentDate, "YYYY");
    }
  }
};
</script>

<style lang='scss' scoped>
.vue-simple-calendar {
  position: relative;
}
</style>
