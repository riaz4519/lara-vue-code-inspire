<template>

            <div class="col-md-8 mt-4">
                <div class="card">
                    <div class="card-header"> Task List</div>

                    <div class="card-body">

                        <ul>
                            <li v-for="task in tasks" :key="task.id">{{ task.title}}</li>
                        </ul>



                    </div>
                </div>
            </div>

</template>

<script>
    export default {


        data(){

            return {

                tasks:[],

            }
        },

        methods:{


        },

        created(){

            Event.$on('taskCreated',() => {

                axios.get('./api/task').then( response => this.tasks = response.data);

            });

            axios.get('./api/task').then( response => this.tasks = response.data);


        },
        


    }
</script>
