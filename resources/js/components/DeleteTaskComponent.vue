<template>
    <div>
        <button v-on:click="showModal()">Remove</button>
        <div class="modal fade" id="DeleteTaskModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
            <div class="modal-dialog modal-dialog-centered" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="exampleModalCenterTitle">Delete Task</h5>
                        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                        </button>
                    </div>
                    <div class="modal-body">
                        <div class="mb-12">
                           Do you really want to delete this task {{taskId}} ? 
                        </div>
                    </div>
                    <div class="modal-footer">
                        
                        <button v-on:click="deleteTask(taskId)">Delete</button> 
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import taskApi from '../api/task'
export default {
    props: [
        'taskId'
    ],


    methods:{
        //method to show modal task
            showModal(){
                $('#DeleteTaskModal').modal('show')
            },
            deleteTask(id){
                taskApi.destroy(id).then(response=>{
                this.$root.$emit('taskItemDeleted',id)
                $('#DeleteTaskModal').modal('hide')
            }).catch(error => {
                console.log("Something went wrong")
                });            
            }
    }



}
</script>