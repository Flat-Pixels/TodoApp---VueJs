<template>
  <div id="app">
    <button
      class="JS-add-tasks-group btn btn--light"
      @click="addTasksGroup()">
      add tasks group
    </button>

    <div class="container">

      <div 
        v-for="tasksGroup in tasksGroups">

        <tasks-group
          v-if="!tasksGroup.deleted"
          @delete="deleteTasksGroup(tasksGroup)">
        </tasks-group>
      </div>

    </div>
  </div>
</template>

<script>
import TasksGroup from './components/TasksGroup';
import Vue from 'vue';

export default {
  name: 'app',
  data : function(){
    return {
      tasksGroups: []
    }
  },
  methods: {
    /**
     * Add a new tasksGroup
     * Set the property {deleted} to false
     */
    addTasksGroup: function(){
      this.tasksGroups.push({deleted: false});
    },

    /**
     * Delete a specific tasksGroup
     * @param  {Object} tasksGroup The tasksGroup to delete
     * @return {Void}
     */
    deleteTasksGroup: function(tasksGroup){
      tasksGroup.deleted = true;
    },
  },
  components: {
    TasksGroup
  }
}
</script>

<style>
html,
body {
  padding: 0;
  margin: 0;

  background-color: #e5e5f5;

  font-family: "Source sans pro", sans-serif;
  font-size: 17px;
}

* { box-sizing: border-box; }

.container {
  position: relative;

  max-width: 500px;
  margin: 0 auto;
}

.btn {
  display: block;

  margin: 20px auto;
  padding: 15px 25px;

  background-color: #e5e5f5;
  border-radius: 293px;
  border: none;
  color: #afafb9;

  cursor: pointer;
  transition: all .2s;
  outline: none;
}

.btn--light { background-color: white; }

.btn--warning {
  color: #a26a6a;
  background-color: #f8aaaa;
}
</style>
