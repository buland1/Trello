<template>
  <div>
    <v-app>
    <!-- <Trello /> -->
    <!-- <Card1 /> -->
    <!-- <Card2 /> -->
    <!-- <Card3 /> -->
    <!-- <v-app> -->
    <!-- <IssueList /> -->
     <!-- <IssueList1 /> -->
    <Test />
    <!-- <Abc /> -->
    <!-- <Progress/> -->
    <!-- <backUp /> -->
    </v-app>
    
  </div>
</template>

<script>

// import Trello from "./components/Trello.vue";
// import Card1 from "./components/Card1.vue";
// import Card2 from './components/Card2.vue'
// import Card3 from './components/Card3.vue'
// import IssueList from './components/issuelisting.vue'
// import backUp from './components/ListingBackup.vue'
import Test from './components/test.vue'
// import Abc from './components/Abc.vue'
// import Progress from './components/progresscard.vue'
export default {
  name: "App",
  components: {
    // Trello,
    // Card1,
    // Card2,
    // Card3,
    // IssueList,
    // IssueList1,
    Test,
    // Abc,
    // Progress
    // backUp,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
