<template>
  <input
    type="text"
    class="form-control"
    placeholder="Neue Aufgabe"
    v-model="content"
  />
  <div class="d-grid my-2">
    <button class="btn btn-secondary" @click="submitTask()">Eintragen</button>
  </div>
</template>

<script>
export default {
  name: "NewTask",
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
    };
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
