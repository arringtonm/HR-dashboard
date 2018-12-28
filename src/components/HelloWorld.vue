<template>
  <div>

    <!-- <h3>All events by ID</h3>
    <ul>
      <li>
        <div class="column head">Employee</div>
        <div class="column head">Type</div>
        <div class="column head">Date</div>
      </li>
      <li v-for="event in lifeEventData" :key="event.id">
        <div class="column">{{ employees[event[2]] }}</div>
        <div class="column">{{ eventTypes[event[1]] }}</div>
        <div class="column">{{ event[3].toDateString() }}</div>
      </li>
    </ul>

    <h3>All events by employee (1)</h3>
    <ul>
      <li>
        <div class="column head">Employee</div>
        <div class="column head">Type</div>
        <div class="column head">Date</div>
      </li>
      <li v-for="event in sortByEmployee(1)" :key="event.id">
        <div class="column">{{ employees[event[2]] }}</div>
        <div class="column">{{ eventTypes[event[1]] }}</div>
        <div class="column">{{ event[3].toDateString() }}</div>  
      </li>
    </ul>

    <h3>All events by type (hire)</h3>
    <ul>
      <li>
        <div class="column head">Employee</div>
        <div class="column head">Type</div>
        <div class="column head">Date</div>
      </li>
      <li v-for="event in sortByType(1)" :key="event.id">
        <div class="column">{{ employees[event[2]] }}</div>
        <div class="column">{{ eventTypes[event[1]] }}</div>
        <div class="column">{{ event[3].toDateString() }}</div>  
      </li>
    </ul> -->


    <h3>All events by date</h3>
    <label class="label" for="dateStartInput">Start Date <span class="smallcaps">(YYYY-MM-DD)</span></label>
    <input class="input-date" id='dateStartInput' :value='startDate.toJSON().substring(0,10)' @change='startDate = new Date($event.target.value)'>
    <label class="label" for="dateEndInput">End Date <span class="smallcaps">(YYYY-MM-DD)</span></label>
    <input class="input-date" id='dateEndInput' :value='endDate.toJSON().substring(0,10)' @change='endDate = new Date($event.target.value)'>
    <ul>
      <li>
        <div class="column head">Employee</div>
        <div class="column head">Type</div>
        <div class="column head">Date</div>
      </li>
      <li v-for="date in dateRangeChecker" :key="date.index">
        <div class="column">{{ employees[date[2]] }}</div>
        <div class="column">{{ eventTypes[date[1]] }} </div>
        <div class="column">{{ date[3].toDateString() }}</div>
      </li>

    </ul>


  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data: function() {
    return {
      startDate: new Date("1990/01/01"),
      endDate: new Date("2020/01/01"),
      employees: { 1: "Ricky Carmichael", 2: "Ryan Dungey" },
      eventTypes: {
        1: "Date of hire",
        2: "Marriage",
        3: "Birth/Adoption",
        4: "Gain of other coverage",
        5: "Loss of other coverage"
      },
      lifeEventData: [
        // note for later that toDateString() uses 0-index.
        [1, 1, 1, new Date(2008, 7, 4)],
        [2, 2, 1, new Date(2010, 4, 12)],
        [3, 4, 1, new Date(2011, 1, 1)],
        [4, 1, 2, new Date(2015, 8, 10)],
        [5, 3, 2, new Date(2016, 2, 15)],
        [6, 3, 2, new Date(2017, 11, 30)],
        [7, 5, 1, new Date(2018, 6, 5)]
      ]
    };
  },
  computed: {
    dateRangeChecker() {
      const datesInRange = this.lifeEventData.filter(variable =>
        this.inDateRange(variable[3], this.startDate, this.endDate)
      );
      return datesInRange;
    }
  },
  // mounted: {},
  methods: {
    sortByEmployee(id) {
      const employeeEvents = this.lifeEventData.filter(
        empID => empID[2] === id
      );
      return employeeEvents;
    },
    sortByType(type) {
      const typeEvents = this.lifeEventData.filter(
        eventType => eventType[1] === type
      );
      return typeEvents;
    },
    inDateRange(dateToCheck, startDate, endDate) {
      return dateToCheck >= startDate && dateToCheck <= endDate;
    },
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
ul {
  // margin: none;
  // padding-left: none;
}
li {
  display: flex;
  flex-direction: row;
  padding: 0.75em;
  margin-left: none;
  list-style: none;
}
li:nth-child(odd) {
  background-color: #eee;
}
.column {
  width: 200px;
  margin-right: 2em;
}
.head {
  font-weight: 800;
}

.input-date {
  padding: 0.25em;
  font-family: Avenir;
  font-size: 1em;
}
.smallcaps {
  font-variant: small-caps;
  font-size: 0.8em;
}
.label {
  font-size: 0.9em;
  position: absolute;
  display: inline-block;
  transform: translateY(-1.5em);
}
</style>
