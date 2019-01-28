<template>
  <div class="container mt-5 mx-4">
    <div v-if="isInput">
      <add-reminder v-on:add-reminder="addReminder" v-on:close-input="toggleInput"></add-reminder>
    </div>
    <div v-else>
      <div class="profile-margin">
        <div class="profile-title rtext d-inline">Hello Floyd Mullins</div>
        <div class="d-inline">
          <img class="profile-img" src="./assets/task-1.png" alt>
        </div>
        <p class="text-secondary rtext">You have {{getNoOfPendingTasks}} tasks</p>
      </div>
      <list-reminders
        class="my-5"
        :reminders="reminders"
        name="list"
        v-on:show-input="toggleInput"
        @delete="deleteReminder"
      ></list-reminders>
    </div>
  </div>
</template>

<script>
import ListReminders from "./components/ListReminders";
import AddReminder from "./components/AddReminder";
export default {
  name: "app",
  components: {
    AddReminder,
    ListReminders
  },
  data: function() {
    return {
      rId: 0,
      reminders: [],
      cReminders: [],
      isInput: false
    };
  },
  computed: {
    getNoOfPendingTasks: function() {
      return this.reminders.length;
    }
  },
  methods: {
    addReminder: function(e) {
      this.reminders.push({
        id: ++this.rId,
        text: e,
        date: this.getRandomDate()
      });
    },
    processCompleted: function(e) {
      var reminder = this.reminders.find(el => el.id == e.id);
      this.reminders.splice(reminder.index, 1);
      this.cReminders.push(reminder);
    },
    toggleInput: function() {
      this.isInput = !this.isInput;
    },
    getRandomDate() {
      var dateNow = new Date().setHours(0, 0, 0, 0);
      var max = 30;
      var min = -100;
      var ds = (Math.floor(Math.random() * (max - min)) + min) * 86400000;
      return new Date(dateNow + ds).toDateString().slice(0, -4);
    },
    deleteReminder(e) {
      this.reminders.splice(e, 1);
    }
  }
};
</script>

<style lang="less">

h1, h2, h3 {
  margin: 0;
}
.container{
  display: flex;
  flex-flow: column wrap;
}
body{ 
padding: .3em;
}

.icon-trash{
  width: fit-content;
  height: fit-content;
  color: white;
  background: rgb(255, 100, 100);
  border: 0;
  cursor: pointer;
  outline: none;
  font-size: 1.5em;
  display: flex;
  flex-direction: row;
  justify-content: center;
  text-align: center;
  padding: 0.4em;
  border-radius: 50%;
}

.btn-round {
  border: 0;
  cursor: pointer;
  outline: none;
  font-size: 1.5em;
  display: flex;
  flex-direction: row;
  justify-content: center;
  text-align: center;
  padding: 0.4em;
  border-radius: 50%;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}
.profile-margin{
  .mb(25);
}
.profile-title {
  font-size: 1.6em;
  color: rgb(49, 49, 49);
}
.profile-img {
  width: 3em;
  height: 3em;
  border-radius: 50%;
  margin-top: .8em;
  float: right;
}
.text-secondary {
  color: gray;
}
.btn-primary {
  background-color: #167bd4;
  color: white;
  font-weight: bold;
}
.card {
  .my(10);
  padding: .8em;
  flex-direction: column;
  min-width: 0;
  word-wrap: break-word;
  background-color: #fff;
  background-clip: border-box;
  box-shadow: #e4e4e4 0px 2px 20px;
}
.rtext {
  font-family: 'Ubuntu', sans-serif;
}
.reminder-foot-text {
  font-size: 0.8em;
  color: gray;
}
.lead {
  font-size: 1em;
  font-weight: 400;
}
.fixed-add-btn {
  bottom: 0;
  position: fixed;
}

.fixed-add-btn2{
  bottom: 1em;
  position: fixed;
  left: 45%;
}
::-webkit-scrollbar {
    width: 0px;  /* remove scrollbar space */
    background: transparent;  /* optional: just make scrollbar invisible */
}
.btm-action-btn {
  position: absolute;
}
[draggable="true"] {
  cursor: move;
  -khtml-user-drag: element;
  -webkit-user-drag: element;
}

/*
* margin
*/
.ml(@val) {
  margin-left: (@val* .1em);
}
.mr(@val) {
  margin-right: (@val* .1em);
}
.mt(@val) {
  margin-top: (@val* .1em);
}
.mb(@val) {
  margin-bottom: (@val* .1em);
}
.m(@val) {
  margin: (@val* .1em);
}
.my(@val) {
  .mt(@val);
  .mb(@val);
}
.mx(@val) {
  .ml(@val);
  .mr(@val);
}

.m-auto {
  margin: auto;
}
.ml-auto {
  margin-left: auto;
}
.mr-auto {
  margin-right: auto;
}
.mt-auto {
  margin-top: auto;
}
.mb-auto {
  margin-bottom: auto;
}
.my-auto {
  .mb-auto();
  .mt-auto();
}
.mx-auto {
  .ml-auto();
  .mr-auto();
}

.generate-margin(5);

.generate-margin(@n, @i:0) when (@i <= @n) {
  .m-@{i} {
    .m(@i);
  }
  .mr-@{i} {
    .mr(@i);
  }
  .ml-@{i} {
    .ml(@i);
  }
  .mt-@{i} {
    .mt(@i);
  }
  .mb-@{i} {
    .mb(@i);
  }
  .mx-@{i} {
    .ml(@i);
    .mr(@i);
  }
  .my-@{i} {
    .mt(@i);
    .mb(@i);
  }
  .generate-margin(@n, (@i+1));
}

/*
* text alignments
*/
@alignments: left, right, center, none;
each(@alignments, {
  .text-@{value} {
    text-align: @value;
  }
});

/**
* width & height
*/
each(range(100), {
  .w-@{value} {
    width: (@value * 1%);
  }
  .h-@{value} {
    height: (@value * 1%);
  }
});

ion-icon {
  font-size: 1.4em;
  font-weight: bold;
}
.add-r{
  margin-left: -1em;
  margin-right: -1em;
}
.btn-block {
  font-size: 1.2em;
  padding: .9em;
  text-align: center;
  width: 100%;
  .mx(0);
  left:0;
  border: none;
  cursor: pointer;
  border-radius: 0.1em;
  color: #fff;
  background: #167bd4;
}
/**
* display
*/

@displays: none, table, block, inline, flex;

each(@displays, {
  .d-@{value} {
    display: @value;
  }
});

.btn-close {
  cursor: pointer;
}
.ib-ctrl {
  border: 0;
  font-size: 1.5em;
  font-family: 'Ubuntu', sans-serif;
  resize: none;
  width: 100%;
  flex: 1;
  outline: none;
}
.ion-empty-btn {
  border: none;
  background: none;
  padding: .5em;
  font-size: 1.2em;
}
*, *:before, *:after  {
  font-family: 'Ubuntu', sans-serif;
  -webkit-box-sizing: border-box;
     -moz-box-sizing: border-box;
          box-sizing: border-box;
}
</style>
