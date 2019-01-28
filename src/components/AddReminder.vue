<template>
  <div class="add-r">
    <!-- <form @submit.prevent="addReminder">
    <div class="input-group input-group-lg mb-3 shadow-lg">
      <input type="text" class="form-control" name="reminder" id="reminder" v-model="reminder" autofocus>
      <div class="input-group-append">
        <button type="submit" class="bg-primary text-white input-group-text">Add reminder</button>
      </div>
    </div>
    </form>-->
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
      <!-- <date-pick v-model="date" :inputAttributes="{readonly: true}"></date-pick> -->
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
  components: {
    // DatePick
  },
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