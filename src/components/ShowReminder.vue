<template>
  <div class="card rtext">
    <div class="lead">
      <span class="text-left">{{reminder.text}}</span>
      <span style="float: right">
        <ion-icon name="alarm"></ion-icon>
      </span>
      <p class="reminder-foot-text">Due {{reminder.date}}</p>
    </div>
  </div>
</template>
<script>
export default {
  name: "ShowReminder",
  props: {
    reminder: Object,
    rtype: String
  },
  components: {},
  data: function() {
    return {};
  },
  methods: {
    complete: function() {
      this.$emit("completed", this.reminder);
    }
  }
};
</script>