<template>
  <div>
    <div v-for="(reminder, idx) in reminders" :key="'div'+reminder.id">
      <drag
        class="drag"
        :key="'drag'+reminder.id"
        :transfer-data="{reminder, idx}"
        @dragstart="toggleDelete"
        @dragend="toggleDelete"
      >
        <show-reminder
          :key="reminder.id"
          :reminder="reminder"
          :rtype="rtype"
          :name="idx"
        ></show-reminder>
      </drag>
    </div>

    <div v-if="deleting">
    <drop class="drop" @drop="onDrop">
      <div class="icon-trash fixed-add-btn2">
        <ion-icon name="trash"></ion-icon>
      </div>
    </drop>
    </div>
    <div v-else>
      <button class="btn-round btn-primary fixed-add-btn2" @click="showInput()">
        <ion-icon id="c-add" name="add"></ion-icon>
      </button>
    </div>
  </div>
</template>


<script>
import { Drag, Drop } from "vue-drag-drop";
import ShowReminder from "./ShowReminder";
export default {
  name: "ListReminders",
  props: {
    reminders: Array,
    rtype: String
  },
  components: {
    ShowReminder,
    Drag,
    Drop
  },
  data: function() {
    return {deleting: false};
  },
  methods: {
    showInput: function() {
      this.$emit("show-input");
    },
    onDrop: function(e) {
      this.$emit("delete", e.idx);
      this.toggleDelete();
    },
    toggleDelete: function(){
      this.deleting = !this.deleting;
    }
  }
};
</script>