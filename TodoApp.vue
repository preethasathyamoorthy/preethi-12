<template>
    <div class="container" style="max-width: 600px">
       <h2 class="text-center mt-5">My Vue To-do App</h2>
       <div class="d-flex mt-5">
           <input type="text" v-model="task" placeholder="Enter task"
        class="w-100 form control" 
        
          />
          <button class="btn btn-warning rounded-0" @click="submitTask">Submit</button>


       </div>
        <!-- task table -->
       <table class="table table-bordered mt-5">
 <thead>
   <tr>
     <th scope="col">Task</th>
     <th scope="col" style="width:120px">Status</th>
     <th scope="col" class="text-center">Delete</th>
     <th scope="col" class="text-center">Edit</th>
   </tr>
   </thead>
   <tbody>

   <tr v-for="(task,index) in tasks" :key="index">
     
     
     <td>
      <span :class="{'line-through':task.status==='finished'}">
        {{ task.name }}
        </span>
        </td>
        <td>
           <span
              class="pointer select"
              @click="changeStatus(index)"
              :class="{ 
                 'text-danger' :task.status==='to-do',
                 'text-success' :task.status==='finished',
                 'text-warning' :task.status==='in-progress'
              }"
             >
              <!-- {{ capitalizeFirstChar(task.status) }}  -->
             </span>
        </td>
        <td class="text-center">
        <div @click="deleteTask(index)">
           <span class="fa fa-trash pointer"></span>
        </div>
     </td>
     <td class="text-center">
                   <div @click="editTask(index)">
           <span class="fa fa-pen pointer"></span>
        </div>
     </td>

   </tr>
  
   
 </tbody>
</table>

    </div>
</template>

<script>
export default {
  name: 'TodoApp',
  props:{
  msg:String,
  },

data() {
  return {
     task:"",
     editedTask:null,
     status:["to-do","in-progress","finished"],
     // status could be:'to-do'/'in-progress'/'finished'
     tasks: [
        {
           name:"Webcamp code.",
           status:"to-do",
        },
        {
           name:"subscribe now.",
           status:"to-do",
        },
        {
           name:"Create YouTube video.",
           status:"to-do",
        },
     ],
  };
},
methods:{
  // capitalize first character
  capitalizeFirstChat(str){
     return str.charAt(0).toUppercase()+str.slice(1);
  },
  // change status of task by index
  changeStatus(index){
     let newIndex=this.statuses.indexOf(this.task[index].status)
     if(++newIndex>2) newIndex=0;
     this.tasks[index].status=this.statuses[newIndex];

  },
  // delete task by index
  deleteTask(index){
     this.tasks.splice(index,1);
  },
  // edit task
  editTask(index){
     this.task = this.tasks[index].name;
     this.editTask = index;
  },
  // Add/update task
  submitTask(){
     if(this.task.length===0) return;
     // we need to update task
     if(this.editTask !=null){
        this.task[this.editTask].name=this.task;
        this.editTask=null
     }
     else{
        // we need to add new task
        this.tasks.push({
           name:this.task,
           status:"todo",
        });
     }
     this.task="";
  },
},
};

</script>

<style>

</style> 