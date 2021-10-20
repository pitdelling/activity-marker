<template>
  <date-picker
    :paintingDateMethod="paintingDateMethod"
    :shouldDateBePainted="shouldDateBePainted"
  />
</template>

<script>
import moment from 'moment'
import DatePicker from '../../components/DatePicker.vue'
import sharedMethods from '../../shared/SharedMethods'

export default {
  name: 'ABDatePicker',

  components: {
    DatePicker
  },

  data: () => ({
  }),

  computed: {
  },

  methods: {
    paintingDateMethod () {
      sharedMethods.teste
      return 'red'
    },
    shouldDateBePainted (date) {
      const calendarDay = moment(date, 'YYYY-MM-DD')
      const atualDate = moment()
      return this.isDateAWeekDay(atualDate) && calendarDay.isSameOrBefore(atualDate)
    }
  }
};
</script>

<style>
* {
  height: 100%;
  width: 100%;
}

#App {
  background: black !important;
  color: white !important;
}

#app-bar-right-side {
  width: 260px;
}
</style>
