<template>
  <div>
    <md-table v-model="events" md-sort="name" md-sort-order="asc" md-card>
      <md-table-toolbar>
        <h1 class="md-title">Life Events</h1>
      </md-table-toolbar>
      <md-table-row slot="md-table-row" slot-scope="{ item }">
        <md-table-cell md-label="ID" md-sort-by="id">{{ item.id }}</md-table-cell>
        <md-table-cell md-label="Type" md-sort-by="type">{{ eventTypes[item.type] }}</md-table-cell>
        <md-table-cell md-label="Name" md-sort-by="employee">{{ employees[item.employee] }}</md-table-cell>
        <md-table-cell md-label="Date" md-sort-by="date">{{ dateRender(item.date) }}</md-table-cell>
      </md-table-row>
    </md-table>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data: function() {
    return {
      startDate: "2000/01/01",
      endDate: "2018/01/28",
      employees: { 1: "Ricky Carmichael", 2: "Ryan Dungey" },
      eventTypes: {
        1: "Date of hire",
        2: "Marriage",
        3: "Birth/Adoption",
        4: "Gain of other coverage",
        5: "Loss of other coverage"
      },
      events: [
        {
          id: 1,
          type: 1,
          employee: 1,
          date: "2008/7/4"
        },
        {
          id: 2,
          type: 2,
          employee: 1,
          date: "2010/4/12"
        },
        {
          id: 3,
          type: 4,
          employee: 1,
          date: "2011/1/1"
        },
        {
          id: 4,
          type: 1,
          employee: 2,
          date: "2015/8/10"
        },
        {
          id: 5,
          type: 3,
          employee: 2,
          date: "2016/2/15"
        },
        {
          id: 6,
          type: 3,
          employee: 2,
          date: "2017/11/30"
        },
        {
          id: 7,
          type: 5,
          employee: 1,
          date: "2018/6/5"
        }
      ]
    };
  },
  computed: {
    dateRangeChecker() {
      const datesInRange = this.lifeEventData.filter(dateRange =>
        this.inDateRange(dateRange[date], this.startDate, this.endDate)
      );
      return datesInRange;
    }
  },
  methods: {
    dateRender(date) {
      const dateOut = new Date(date);
      return dateOut
        .toLocaleString("en-us")
        .split(" ", 1)
        .toString()
        .slice(0, -1);
    },
    // customFilter() {
    // },
    sortByEmployee(id) {
      const employeeEvents = this.events.filter(empID => empID.employee === id);
      return employeeEvents;
    },
    sortByType(typeToCheck) {
      const typeEvents = this.lifeEventData.filter(
        eventType => eventType.type === typeToCheck
      );
      return typeEvents;
    },
    inDateRange(dateToCheck, startDate, endDate) {
      return dateToCheck >= startDate && dateToCheck <= endDate;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
</style>
