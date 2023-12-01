<template>
    <div class="container py-4" >
        <div class="row justify-content-center">
            <div class="col-md-10">
                <div class="card">
                    <div class="card-header">Posts Component
                        <select v-model="category_id" class="form-control col-md-3 float-right">
                            <option value="">-- choose category --</option>
                            <option v-for="category in categories"  :key="category.id" :value="category.id">
                                {{ category.name }}
                            </option>
                        </select>
                    </div>

                    <div class="card-body">
                        <table class="table">
                            <thead>
                                <tr>
                                    <th>Title</th>
                                    <th>Body</th>
                                    <th>Created</th>
                                    <th></th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="post in posts.data" :key="post.id">
                                    <td>{{ post.title }}</td>
                                    <td>{{ post.body.substring(0, 50) }}</td>
                                    <td>{{ post.created }}</td>
                                    <td></td>
                                </tr>

                            </tbody>
                        </table>
                        <pagination :data="posts" @pagination-change-page="getResults"></pagination>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                posts: {},
                categories: {},
                category_id: ''
            }
        },
        mounted() {
            axios.get('/api/categories')
            .then(response => {
                this.categories = response.data.data;
            });
            this.getResults();
        },
        watch: {
            category_id(value) {this.getResults();}
        },
        methods: {
            // Our method to GET results from a Laravel endpoint
            getResults(page = 1) {
                axios.get('/api/posts?page=' + page + '&category_id=' + this.category_id)
                .then(response => {
                    this.posts = response.data;
                });
            }
        }
    }
</script>
