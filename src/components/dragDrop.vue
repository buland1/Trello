<template>
  <div class="row">
    <div class="col-3">
      <h3>Draggable 1</h3>
      <draggable
        class="list-group-issue"
        :list="list1"
        group="people"
        @change="log"
        @end="onEnd"
      >
        <div
          class="list-group-item"
          v-for="(element, index) in list1"
          :key="element.name"
        >
          {{ element.name }} {{ index }}
        </div>
      </draggable>
    </div>

    <div class="col-3">
      <h3>Draggable 2</h3>
      <draggable
        class="list-group-onprogress"
        :list="list2"
        group="people"
        @change="log"
        @end="onEnd"
      >
        <div
          class="list-group-item"
          v-for="(element, index) in list2"
          :key="element.name"
        >
          {{ element.name }} {{ index }}
        </div>
      </draggable>
    </div>
  </div>
</template>
<script>
import draggable from "vuedraggable";
export default {
  name: "dragDrop",
  display: "Two Lists",
  order: 1,
  components: {
    draggable,
  },
  data() {
    return {
      list1: [
        { name: "John", id: 1 },
        { name: "Joao", id: 2 },
        { name: "Jean", id: 3 },
        { name: "Gerard", id: 4 },
      ],
      list2: [
        { name: "Juan", id: 5 },
        { name: "Edgard", id: 6 },
        { name: "Johnson", id: 7 },
      ],
    };
  },
  methods: {
    log: function (evt) {
      window.console.log(evt);
    },
   onEnd: function (evt) {
      console.log(evt);
  }
 }
}
</script>
<style scoped>
.list-group {
  min-height: 100px;
}
</style>