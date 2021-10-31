<template>
  <input
    type="text"
    class="form-control"
    placeholder="Neue Aufgabe"
    v-model="content"
    v-focus="{ color: 'green' }"
  /><small>Noch {{ numberOfCharsLeft }} Zeichen erlaubt</small>
  <div class="d-grid my-2">
    <button class="btn btn-secondary" @[mode]="submitTask()">Eintragen</button>
  </div>
  <teleport to="#settings">
    <select class="form-select" v-model="mode">
      <option value="click">Einfacher Klick</option>
      <option value="dblclick">Doppelklick</option>
    </select>
  </teleport>
</template>

<script>
export default {
  name: "NewTask",
  inject: ["maxNumberOfChars"],
  emits: {
    "new-task": (task) => {
      if (task.content === "") {
        console.warn("NewTaskComponent: Content darf nicht leer sein!");
        return false;
      }
      return true;
    },
  },
  data() {
    return {
      content: "",
      mode: "click",
    };
  },
  computed: {
    numberOfCharsLeft() {
      return this.maxNumberOfChars - this.content.length;
    },
  },
  methods: {
    submitTask() {
      // Event ausrufen - Kind an Elternteil
      this.$emit("new-task", {
        // kebap-case
        //Payload
        content: this.content,
      });
      this.content = "";
    },
  },
};
</script>

<style scopeds></style>
