<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                
                <div class="card mb-3 mt-3" v-for="item in list">
                    
            
                    <a class="card-header" v-text="item.title"  v-bind:href="item.slug"></a>
                    
                    
                    <div class="card-body">
                        <span>{{item.id}}</span>
                        <p class="card-text" v-text="item.body"></p>
                    </div>
                </div>

                <infinite-loading @infinite="infiniteHandler">
                    <div slot="no-more">--</div>
                    <div slot="spinner">Cargando...</div>
                    <div slot="no-result">Si resultados</div>
                </infinite-loading>

            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                list:[],
                page:0
            };
        },
        methods: {
            infiniteHandler($state){
                this.page++

                let url = 'http://127.0.0.1:8000/api/posts?page=' + this.page

                axios.get(url)
                .then(response => {
                    let post = response.data.data
                    
                    if(post.length){
                        this.list= this.list.concat(post)
                        $state.loaded()
                    } else {
                        $state.complete()
                    }

                });
                
            }
        }
    }
</script>
