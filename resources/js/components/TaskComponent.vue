<template>
    <div class="container">
        <button id="show-modal" v-on:click="showModal()">+</button>
            <!-- use the modal component, pass in the prop -->
            <!-- Modal -->
        <div class="modal fade" id="exampleModalCenter" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
            <div class="modal-dialog modal-dialog-centered" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="exampleModalCenterTitle">News Task</h5>
                        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                        </button>
                    </div>
                    <div class="modal-body">
                        <div class="mb-3">
                            <label for="exampleFormControlInput1" class="form-label">Title</label>
                            <input type="email" class="form-control" v-model="title" placeholder="Task 1">
                        </div>
                        <div class="mb-3">
                            <label for="exampleFormControlTextarea1" class="form-label">Description</label>
                            <textarea class="form-control" v-model="description" rows="3"></textarea>
                        </div>
                    </div>
                    <div class="modal-footer">
                        <button v-on:click="addTask()">Save</button> 
                    </div>
                </div>
            </div>
           
        </div>
    </div>
</template>

<script>
import taskApi from '../api/task';

    export default {
        data() {
            return {
                title : '',
                description :'',
            }
        },
        //Once the component is loaded log
        mounted() {
            console.log('Component is ready.')
        },
        //Once the component is created fetch all tasks of today
        created() {
            console.log('component is created')
        },

        methods : {
            //method to show modal task
            showModal(){
                $('#exampleModalCenter').modal('show')
            },
            //persiste data via api
            addTask(){
                        taskApi.add({
                        title : this.title,
                        description : this.description
                    })
                    .then(response => {
                        //push the new task to the array of tasks 
                        //so it will be just an event the parent component will be listening to it .
                        this.$root.$emit('taskItemAdded', response);
                       
                    }).catch(error => {
                        alert(error.response.data.message)
                    })
            }
            
        }
        
    }
</script>
