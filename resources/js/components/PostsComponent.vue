<template>
    
    <div class="row justify-content-center">
        <div class="col-md-12">
            
            <div class="card mb-3 mt-3" v-for="item in list">
                    
                <!-- <a class="card-header" v-text="item.title"  v-bind:href="item.slug"></a> -->
                
                <router-link 
                    class="card-header"
                    :to="{name:'post', params: {slug: item.slug}}"
                    v-text="item.title"
                ></router-link>
                
                <div class="card-body">
                    <span>{{item.id}}</span>
                    <p class="card-text" v-text="item.excerpt"></p>
                </div>

            </div>

            <infinite-loading @infinite="infiniteHandler">
                <div slot="no-more">--</div>
                <div slot="spinner">Cargando...</div>
                <div slot="no-result">Si resultados</div>
            </infinite-loading>

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
