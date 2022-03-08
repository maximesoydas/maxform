<template>
  <div class="home">
      <v-text-field
      v-model="newTaskTitle"
      @click:append="addTask"
      @keyup.enter="addTask"
      class="pa-4"
      outlined
      label="Add Task"
      append-icon="mdi-plus"
      hide-details
      clearable
    ></v-text-field>

    <v-list class="pt-0"
      flat
    >
      <div        
      v-for="task in tasks" 
      :key='task.id'
      >
        <v-list-item
        @click="doneTask(task.id)"
        :class="{'blue lighten-5' : task.done}"
        >
        <!-- Checkbox -->
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox
                :input-value="task.done"
                color="primary"
              ></v-checkbox>
            </v-list-item-action>

          <!-- Title -->
            <v-list-item-content>
              <v-list-item-title
              :class="{ 'text-decoration-line-through' : task.done }"
              >
                
                {{ task.title }}
                
                </v-list-item-title>
            </v-list-item-content>

          <!-- Button -->
            <v-btn
             @click.stop="deleteTask(task.id)"
             icon>
               <v-icon color="red lighten-1">mdi-delete</v-icon>
            </v-btn>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>

export default {
  name: 'Todo',
  data() {
    return {
      newTaskTitle: '',
      tasks: [
        // {
        //   id: 1,
        //   title: 'Eat',
        //   done: false,
        // },
        // {
        //   id: 2,
        //   title: 'Work',
        //   done: false,
        // },
        // {
        //   id: 3,
        //   title: 'Rest',
        //   done: false,
        // },
        // {
        //   id: 4,
        //   title: 'Sleep',
        //   done: false,
        // },
      ]
    }
  },
    methods: {
      addTask(){
        // console.log('addTask')

        //  Create an object and append to tasks array
        //  our dictionary/object
        let newTask = {
          id: Date.now(),
          title: this.newTaskTitle,
          done: false
        }
        // tasks.append(newTask)
        this.tasks.push(newTask)
        this.newTaskTitle = ''

      },
      doneTask(id){
        // Returns an array of objects not a single object adding [0] really return the value
       let task = this.tasks.filter(task => task.id === id)[0]
      //  task value true or falso 
       task.done = !task.done
      },
      deleteTask(id) {
        this.tasks = this.tasks.filter(task => task.id != id)
      }
    }
  }

</script>
