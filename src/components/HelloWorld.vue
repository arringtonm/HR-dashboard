<template>
  <div>
    <md-table-toolbar>
      <h1 class="md-title">Life Events Tracker</h1>
    </md-table-toolbar>
    <md-table>
      <md-table-cell>
        <label for="startDate">Start Date</label>
        <md-datepicker id="startDate" v-model="startDate" :md-open-on-focus="false" />
      </md-table-cell>
      <md-table-cell>
        <label for="endDate">End Date</label>
        <md-datepicker id="endDate" v-model="endDate" :md-open-on-focus="false" />
      </md-table-cell>
      <md-table-cell>
        <md-field class="md-field-modify">
          <label for="employee" class="label-modify">Employee</label>
          <md-select v-model="employeeSelected" name="employee" id="employee">
            <md-option value="all">All</md-option>
            <div v-for="(employee, key) in employees" :key="employee.id">
              <md-option :value="key">{{ employee }}</md-option>
            </div>
          </md-select>
        </md-field>
      </md-table-cell>
      <md-table-cell>
        <md-field class="md-field-modify">
          <label for="eventtype" class="label-modify">Event Type</label>
          <md-select v-model="eventTypeSelected" name="eventtype" id="eventtype">
            <md-option value="all">All</md-option>
            <div v-for="(type, key) in eventTypes" :key="type.id">
              <md-option :value="key">{{ type }}</md-option>
            </div>
          </md-select>
        </md-field>
      </md-table-cell>
      <md-table-cell>
        <md-button class="md-raised" @click="resetFilters()">Reset Filters</md-button>
      </md-table-cell>
    </md-table>
    <md-table v-model="this.customFilter()" md-sort="name" md-sort-order="asc" md-card>
      <md-table-row slot="md-table-row" slot-scope="{ item }">
        <md-table-cell md-label="ID" md-sort-by="id">{{ item.id }}</md-table-cell>
        <md-table-cell md-label="Name" md-sort-by="employee">{{ employees[item.employee] }}</md-table-cell>
        <md-table-cell md-label="Type" md-sort-by="type">{{ eventTypes[item.type] }}</md-table-cell>
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
      endDate: new Date(),
      employeeSelected: "all",
      eventTypeSelected: "all",
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
  methods: {
    dateRender(date) {
      const dateOut = new Date(date);
      return dateOut
        .toLocaleString("en-us")
        .split(" ", 1)
        .toString()
        .slice(0, -1);
    },
    customFilter() {
      return this.sortByDate(this.sortByType(this.sortByEmployee(this.events)));
    },
    sortByEmployee(input) {
      if (this.employeeSelected === "all") {
        return input;
      } else {
        const output = input.filter(
          empID => empID.employee == this.employeeSelected
        );
        return output;
      }
    },
    sortByType(input) {
      if (this.eventTypeSelected == "all") {
        return input;
      } else {
        const typeEvents = input.filter(
          eventType => eventType.type == this.eventTypeSelected
        );
        return typeEvents;
      }
    },
    sortByDate(input) {
      const output = input.filter(dateCheck => this.inDateRange(dateCheck));
      return output;
    },
    inDateRange(dateToCheck) {
      if (
        new Date(dateToCheck.date) >= new Date(this.startDate) &&
        new Date(dateToCheck.date) <= new Date(this.endDate)
      ) {
        return true;
      }
    },
    resetFilters() {
      this.startDate = "2000/01/01";
      this.endDate = new Date();
      this.employeeSelected = "all";
      this.eventTypeSelected = "all";
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.md-field-modify {
  transform: translateY(0.7em);
}
.label-modify {
  transform: translateY(-1.5em);
}
</style>
