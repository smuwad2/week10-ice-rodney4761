<script>
    // TODO: Complete the code
    export default { 
        data() {
            return {
                
            }
        },
        // Hint: insert properties task (Object) and idx (Number)
        props: {
            task: Object,
            idx: Number
        }
    }
</script>

<template>
    <!-- TODO: add your template code here --> 
     <div class="card" style="width: 20rem; padding: 0">
        <div class="card-body" style="text-align: left; ">
            <h5 class="card-title">Deadline: {{ task.deadline }}</h5>
            <hr></hr>
            <p class="card-text">{{ task.desc }}</p>
            <button class="btn btn-primary" v-on:click="$emit('delete-task',idx)">Done</button>
        </div>
    </div>
   
</template>
