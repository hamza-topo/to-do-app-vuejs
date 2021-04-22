<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-12">
                <div class="card">
                    <div class="card-header text-center">Tasks List</div>

                    <div class="card-body">
                            <div class="col-md-10 row">
                                <div class="row" v-for="task in tasks" :key="task.id"> 
                                    <div class="col-md-5">
                                        {{task.title}}
                                    </div>
                                    <div class="col-md-5">
                                        {{task.description}}
                                    </div>
                                    <div class="col-md-2">
                                        Actions
                                    </div>
                                </div> 
                            </div>
                            <div class="col-md-2">
                                <task-component></task-component>
                                <!-- <button @click="addTask()">+</button> -->
                            </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import taskApi from '../api/task'
    export default {
        data() {
            return {
                tasks : [],
            }
        },
        //Once the component is created fetch all tasks of today
        created() {
            taskApi.all().then(response=>{
                    this.tasks = response.data;
            });
        },
        //Once the component is loaded log
        mounted() {
          
            //so u will be listening to event that added the task to tasks list 
            this.$root.$on('taskItemAdded',res => {
                // if item doesnt exist in tasks

                 let itemExists = this.tasks.filter(item => {
                    return item.id === res.data.id
                        }).length !== 0

                if (itemExists) {
                            this.tasks = this.tasks.map(item => {
                                if (item.id === res.data.id) {
                                    return res.data
                                }
                                return item;
                            })
                } else {
                this.tasks.push(res.data)
                }
                $('#exampleModalCenter').modal('hide')
            });
        },
        
    }
</script>
