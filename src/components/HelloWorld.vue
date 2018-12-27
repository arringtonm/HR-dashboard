<template>
  <div>
    <ul>
      <li>
        <div class="column head">Type</div>
        <div class="column head">Employee</div>
        <div class="column head">Date</div>
      </li>
      <li v-for="event in lifeEventData">
        <div class="column">{{ eventTypes[event[0]] }}</div>
        <div class="column">{{ employees[event[1]] }}</div>
        <div class="column">{{ event[2].toDateString() }}</div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data: function() {
    return {
      msg: "Hello there friends",
      employees: { 1: "Ricky Carmichael", 2: "Ryan Dungey"},
      eventTypes: { 
        1: "Date of hire",
        2: "Marriage",
        3: "Birth/Adoption",
        4: "Gain of other coverage",
        5: "Loss of other coverage"
      },
      lifeEventData: {
        // note for later that toDateString() uses 0-index. 
        1: [1, 1, new Date(2008,7,4)],
        2: [2, 1, new Date(2010,4,12)],
        3: [4, 1, new Date(2011,1,1)],
        4: [1, 2, new Date(2015,8,10)],
        5: [3, 2, new Date(2016,2,15)],
        6: [3, 2, new Date(2017,11,30)],
        7: [5, 1, new Date(2018,6,5)]
      }
    }
  },  
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
ul {
  margin: none;
}
li {
  display: flex;
  flex-direction: row;
  padding: 1em;
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
</style>
