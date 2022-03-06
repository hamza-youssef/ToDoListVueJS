<template>
  <div class="container">
    <h1 class="text-center mt-5">Todo App With Vue</h1>

    <div class="d-flex">
      <input type="text" class="form-control" v-model="task" />
      <button class="btn btn-warning rounded" @click="AddTask">Submit</button>
    </div>

    <table class="table table-bordered">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">Edit</th>
          <th scope="col" class="text-center">Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>
<span :class="{'finished': task.Status === 'finished'} ">
{{ task.name }}
</span>

</td>
          <td >
<span class="pointer" @click="ChangeStatus(index) "
:class=" {'text-danger': task.Status === 'to-do',
'text-warning': task.Status === 'in-progress',
'text-success': task.Status === 'finished'
} "
>
{{ task.Status }}
</span>
</td>
          <td>
            <div class="text-center pointer" @click="Edit(index)">
              <i class="fas fa-edit"></i>
            </div>
          </td>
          <td>
            <div class="text-center pointer" @click="Delete(index)">
              <i class="fas fa-trash"></i>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },

  data() {
    return {
      task: "",
      newTask:null,
      availableStatus:["to-do" , "in-progress" , "finished"],
      tasks: [
        {
          name: "Buy a pear from the store",
          Status: "to-do",
        },
        {
          name: "Buy a prickly pear from the store",
          Status: "in-progress",
        },
      ],
    };
  },

  methods: {
    AddTask() {
      if (this.task.length === 0) return;

      if(this.newTask === null){
      this.tasks.push({
        name: this.task,
        Status: "to-do",
      }); } else {
this.tasks[this.newTask].name = this.task ;
this.newTask=null ;
}

      this.task = "";
    },

Delete(index){
this.tasks.splice(index,1)
},

Edit(index){
this.task = this.tasks[index].name;
this.newTask = index
},

ChangeStatus(index){
let newIndex = this.availableStatus.indexOf(this.tasks[index].Status)
if(++newIndex>2) newIndex=0 ;
this.tasks[index].Status= this.availableStatus[newIndex];
},

  },
};
</script>

<style>
.pointer{
cursor: pointer;
}
.finished{
text-decoration-line: line-through;
}
</style>
