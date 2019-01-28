<template>
  <div class="add-r">
    <div>
      <ion-icon class="btn-close" name="close" @click="closeInput"></ion-icon>
    </div>
    <div >
      <textarea
        name="reminder"
        id="reminder"
        class="ib-ctrl"
        v-model="reminder"
        placeholder="What would you like to add?"
        rows="8"
      ></textarea>
      <div class="ml-auto text-right">
        <button class="ion-empty-btn">
          <ion-icon name="attach"></ion-icon>
        </button>
        <button class="ion-empty-btn">
          <ion-icon name="calendar"></ion-icon>
        </button>
      </div>
    </div>
    <div>
      <button class="fixed-add-btn btn-block" @click="addReminder">
        <ion-icon name="add"></ion-icon>
      </button>
    </div>
  </div>
</template>

<style lang="less">
</style>


<script>

export default {
  name: "AddReminder",
  data: function() {
    return {
      reminder: "",
      date: ""
    };
  },
  methods: {
    addReminder: function() {
      if (!this.reminder.trim()) {
        return;
      }
      this.$emit("add-reminder", this.reminder);
      this.reminder = "";
      this.closeInput();
    },
    closeInput: function() {
      this.$emit("close-input");
    }
  }
};
</script>