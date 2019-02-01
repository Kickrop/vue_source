<template>
    <div class="container">
        <div class="row">
            <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
                <h1>Http</h1>
                <div class="form-group">
                    <label for="">Username</label>
                    <input class="form-control" type="text" v-model="user.username"> 
                </div>
                <div class="form-group">
                    <label for="">Mail</label>
                    <input class="form-control" type="text" v-model="user.email">
                </div>
                <div class="btn btn-primary" @click="submit">Submit</div>
                <hr>
                <button class="btn btn-primary" @click="fetchData">Get Data</button>
                <ul class="list-group">
                    <li class="list-group-item" v-for="u in users">{{ u.username }} - {{ u.email }}</li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                user: {
                    username: '',
                    email: ''
                },
                users: [],
                resource: {}
            };
        },
        methods: {
            submit() {
                // this.$http.post('data.json', this.user)
                //     .then(Response => {
                //         console.log(Response);
                //     }, error => {
                //         console.log(error);
                //     });  //uses vue resource

                // this.resource.save({}, this.user);
                this.resource.saveAlt(this.user);
            },
            fetchData() {
                this.$http.get('data.json')
                    .then(response => {
                        return response.json();    
                    })
                    .then(data => {
                        const resultArray = [];
                        for (let key in data) {
                            resultArray.push(data[key]);
                        }
                        this.users = resultArray;
                    });
            }
        },
        created() {
            const customActions = {
                saveAlt: {method: 'POST', url: 'alternative.json'}
            };
            // this.resource = this.$resource('data.json');
            this.resource = this.$resource('data.json', {}, customActions);
        }
    }
</script>

<style>

</style>
