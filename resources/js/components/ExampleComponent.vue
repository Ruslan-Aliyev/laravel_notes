<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">Example Component</div>

                    <div class="card-body">
                        I'm an example component.
                    </div>
                </div>
            </div>
        </div>

        <div v-if="$apollo.loading">Loading..</div>
        <div v-else>
            <div v-for="user in users">
                <h1>Name: {{user.name}}</h1>
                <p>Email: {{user.email }}</p>
            </div>
        </div>
    </div>
</template>

<script>
    import { gql } from "apollo-boost";

    export default {
        mounted() {
            console.log('Component mounted.');

            window.Echo.channel('channel')
                .listen('WSTest', (e) => {
                    console.log(e);
                });
        },
        data: function() {
            return {
                //query data is added
                users: {}
            };
        },
        apollo: {
            //this query will update the `users` data property
            users: {
                query: gql`
                {
                    users {
                        name
                        email
                    }
                }`
            }
        }
    };
</script>