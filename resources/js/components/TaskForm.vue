<template>

            <div class="col-md-8 mt-4">
                <div class="card">
                    <div class="card-header"> Task Form</div>

                    <div class="card-body">

                        <form action="./api/task" method="post" @submit.prevent="addTask()">

                            <div class="form-group">

                                <input type="text" name="title" v-model="title" placeholder="Task title" class="form-control">


                                    {{ errors.get('title') }}


                            </div>


                            <div class="form-group">

                                <input type="submit" value="Add Task" class="btn btn-info">

                            </div>

                        </form>

                    </div>
                </div>
            </div>

</template>

<script>


    class Errors{

        constructor(){

            this.errors = {};
        }

        get(field){

            //console.log(this.errors.title);

            if (this.errors[field]){

                console.log('fdfs');

                return this.errors.title[0];
            }




        }
        record(errors){

            this.errors = errors;

        }


    }

    export default {



        data(){

            return {

                title:'',
                errors: new Errors()


            }
        },
        
        methods:{

            addTask:function () {

                axios.post('./api/task',{

                    title: this.title,


                }).then( (response) => {


                    this.title = '';

                    Event.$emit('taskCreated');

                    console.log(response.data.message);

                }).catch(error => {




                  this.errors.record(error.response.data.errors);



                });




            }
            
        }

    }
</script>
