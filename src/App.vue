<template>
  <div>
    <v-app>
    <!-- <Trello /> -->
    <Test />
    <!-- <progressCard/> -->
    <!-- <listingbackUp /> -->
    <!-- <trelloBoard /> -->
    <!-- <dragDrop/> -->
    </v-app>
    
  </div>
</template>

<script>

// import listingbackUp from './components/ListingBackup.vue'
import Test from './components/test.vue'
// import progressCard from './components/progresscard.vue'
// import Trello from './components/Trello.vue';
// import trelloBoard from './components/board.vue';
// import dragDrop from './components/dragDrop.vue'

export default {
  name: "App",
  components: {
    // Trello,
    Test,
    // progressCard,
    // listingbackUp,
    // trelloBoard,
    // dragDrop,
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
