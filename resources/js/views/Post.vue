<template>
    <div>
        <div class="jumbotron mb-5 text-center">
            <h1 class="display-4" v-text="post.title"></h1>
        </div>

        <div class="container">
            <div class="row justify-content-center">
                <div class="col-12">
                    <p v-text="post.excerpt"></p>
                    <div v-html="post.body"></div>
                    <hr>
                    <h1>Otros Artilos</h1>
                    <posts></posts>
                </div>
            </div>
        </div>
    </div>
</template>


<script>
    export default {
        props: ['slug'],
        data() {
            return {
                post: {}
            };
        },

        created() {
            console.log('hace peticion')
            let url = 'http://127.0.0.1:8000/api/posts/' + this.slug

            axios.get(url)
                .then(response => {
                    this.post = response.data
                });
        }
    }

</script>