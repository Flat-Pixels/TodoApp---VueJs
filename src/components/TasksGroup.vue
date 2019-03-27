<template>
  <div>
    <!-- The form to add a new task
      To the current taskgroup
    -->
    <div class="modal" v-bind:class="{'is-active': isModalActive}">
      <div class="container">
        <div class="modal__form">
          <button class="btn btn--warning" @click.prevent="toggleModal()">Close</button>
          <form>
            <input
              type="text" 
              name="label" 
              placeholder="Ex: Check my recent mail tonight" 
              class="modal__form__input" 
              required="required" v-model="taskLabel">
            <!--<textarea name="description" class="modal__form__input modal__form__input--area"></textarea>-->

            <button type="submit" class="btn" @click.prevent="addTask(taskLabel)">Add</button>
          </form> 
        </div>      
      </div>
    </div>

    <div class="tasks-group">
    	<div class="tasks-group__delete-btn" @click="deleteThis()"></div>
    	<div class="tasks">
    		<!-- List the tasks here ... -->
  		<div class="tasks-item" v-for="task in tasks" v-bind:class="{ 'is-complete': task.completed }">
  			<div class="tasks-item__mark-btn" @click="markAsComplete(task)"></div>
  			<div class="tasks-item__label">{{ task.label }}</div>
  			<div class="tasks-item__options" @click="deleteTask(task)"></div>
  		</div>
    	</div>
    	<button class="btn" @click.prevent="toggleModal()">Add task</button>
    </div>
  </div>
</template>

<script>
  export default {
  	name: 'tasks-group',
  	data: function(){
  	  return {
  	  	tasks: [],
        taskLabel: '',
        isModalActive: false
  	  }
  	},
  	methods: {
      /**
       * Add a task to the current tasksGroup
       */
  	  addTask: function(){
  	  	var task = {
  	  	  label: this.taskLabel,
  	  	  completed: false
  	  	}

  	  	this.tasks.push(task);
        this.taskLabel = '';
  	  },

      /**
       * Toggle the form to add task to a tasksGroup
       * @return {Void}
       */
      toggleModal: function(){
        this.isModalActive = !this.isModalActive;
      },

      /**
       * Mark a task as completed
       * @param  {Object} task The task to completed or not
       * @return {Void}
       */
  	  markAsComplete: function(task){
  	  	task.completed = !task.completed;
  	  },

      /**
       * Delete a task
       * @param  {Object} task The task to delete
       * @return {Void}
       */
  	  deleteTask: function(task){
  	  	this.tasks.splice(this.tasks.indexOf(task), 1);
  	  },

      /**
       * Delete the current taksGroup
       * And dele the entire component
       * 
       * @return {Void}
       */
      deleteThis: function(){
        this.$emit('delete');
        this.$destroy();
      }
  	}
  }
</script>

<style scoped>

.modal {
  position: fixed;
  left: 0;
  top: 0;
  z-index: 999;

  height: 0;
  width: 0;

  opacity: 0;

  background-color: rgba(0, 0, 0, .3);
}

.modal.is-active {
  width: 100%;
  height: 100%;

  opacity: 1;
}

.modal .container {
  top: 50%;
  transform: translateY(-50%);
}

.modal__form {
  width: 100%;
  padding: 30px;

  background-color: white;
}

.modal__form__input {
  width: 100%;
  height: 40px;

  margin-bottom: 15px;
  padding: 10px;

  background-color: white;
  border-radius: 3px;
  border: none;
  outline: none;
  color: #868686;
  border: 1px solid #f3f3f3;
  background-color: #f9f9f9;

  font-family: "Source sans pro", sans-serif;
  font-size: 16px;

}

.modal__form__input--area {
  height: 200px;
  resize: none;
}

.tasks-group {
  position: relative;

  width: 100%;
  padding: 25px;
  margin: 20px auto;

  background-color: #f9f9f9;
  border-radius: 3px;
  box-shadow: 0px 15px 25px rgba(0, 0, 0, .2);

}

.tasks-group__delete-btn {
  position: absolute;
  top: 10px;
  right: 10px;

  width: 20px;
  height: 10px;

  border-radius: 293px;
  
  background-color: #ff9f9f;

  cursor: pointer;
}

.tasks {
  //padding: 15px;
}

.tasks-item {
  display: flex;
  align-items: center;
  justify-content: space-between;

  padding: 10px;
} 

.tasks-item__mark-btn {
  width: 25px;
  height: 25px;

  border-radius: 50%;
  border: 5px solid #b5ea81;

  cursor: pointer;
}

.tasks-item__label {
  width: calc(100% - 40px);
  padding: 0 20px;
}

.tasks-item__options { 
  width: 15px;
  height: 15px;

  border-radius: 50%;
  background-color: #f8aaaa;
  border: 2px solid #a26a6a;

  cursor: pointer;
}

.tasks-item.is-complete .tasks-item__mark-btn {
  border-color: #ddfbbf;
  background-color: #c7eaa5;
}

.tasks-item.is-complete .tasks-item__label {
  color: #a7a7a7;
  text-decoration: line-through;
}
</style>