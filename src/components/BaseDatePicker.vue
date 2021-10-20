<template>
  <div id="date-picker">
    <v-menu
      v-model="isShowMenu"
      :close-on-content-click="false"
      transition="scroll-x-reverse-transition"
      offset-x
      offset-y
      bottom
      dark
      nudge-left="290"
      max-width="290px"
      min-width="auto"
      max-height="291px"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-text-field
          id="refDate"
          v-model="computedDateFormatted"
          :hide-details="true"
          prepend-inner-icon="mdi-calendar"
          prepend-icon="mdi-chevron-left"
          append-outer-icon="mdi-chevron-right"
          label="Data de Referência"
          readonly
          v-bind="attrs"
          v-on="on"
          class="d-flex align-center"
          @click:prepend="lastDay"
          @click:append-outer="dayAfter"
        />
      </template>
      <v-date-picker
        v-model="computedDateFormattedForDatePicker"
        no-title
        @input="isShowMenu = false"
        :event-color="paintingDateMethod"
        :events="shouldDateBePainted"
      />
    </v-menu>
  </div>
</template>

<script>
import moment from 'moment'

export default {
  name: 'DatePicker',

  props: {
    paintingDateMethod: {
      type: Function,
      require: false,
      default: () => {}
    },
    shouldDateBePainted: {
      type: Function,
      require: false,
      default: () => {}
    },
  },

  data: () => ({
    refDate: moment(),
    isShowMenu: false
  }),

  computed: {
    computedDateFormatted () {
      return this.refDate.format('DD/MMM./YYYY')
    },
    computedDateFormattedForDatePicker: {
      get () {
        return this.convertMomentDateToIsoString(this.refDate)
      },
      set (newValue) {
        this.refDate = this.convertIsoStringToMomentDate(newValue)
      }
    }
  },

  methods: {
    convertMomentDateToIsoString (momentDate) {
      return momentDate.format('YYYY-MM-DD')
    },
    convertIsoStringToMomentDate (isoString) {
      return moment(isoString, 'YYYY-MM-DD')
    },
    dayAfter () {
      this.refDate = moment(this.refDate).add(1, 'days')
    },
    isDateAWeekDay (date) {
      return ![0, 6].includes(date.weekday())
    },
    lastDay () {
      this.refDate = moment(this.refDate).subtract(1, 'days')
    }
  }
};
</script>

<style scoped>
#date-picker /deep/ .v-label--active {
  left: -32px !important;
  width: auto;
}

#date-picker /deep/ .v-input__prepend-outer {
  width: auto;
  align-items: center;
}

#date-picker /deep/ .v-input__prepend-inner {
  width: auto;
  margin-right: 5px;
}

#date-picker /deep/ .v-input__append-outer {
  width: auto;
  align-items: center;
}

/deep/ .v-date-picker-years > li {
  height: auto;
}
</style>
