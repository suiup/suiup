<template>
    <div class="d-flex flex-wrap">
        <v-card id="card"
                v-for="content in contents"
                :key="content.text"
                class="mx-auto"
                max-width="500"
                max-height="500"

        >

            <v-container fluid
            >
                <v-card-title v-text="content.title"></v-card-title>
                <v-row dense>
                    <v-col
                        :cols="content.flex"
                    >
                        <v-card-text class="content">
                            <vue-markdown :source="content.text" class="card" ></vue-markdown>
                        </v-card-text>
                        <v-card-actions>
                            <v-btn
                                    color="orange lighten-2"
                                    text
                                    @click="open(content.route)"
                            >
                                Check
                            </v-btn>
                        </v-card-actions>
                    </v-col>
                </v-row>
            </v-container>
        </v-card>
    </div>

</template>

<script>
    import axios from "axios";
    import VueMarkdown from 'vue-markdown'
    export default {
        name: "ArticlesList.vue",
        components: {
            VueMarkdown,
        },
        data(){
            return {
                contents:[]
            }
        },
        mounted(){
            const files_test = require.context('../../public/files', true, /.md$/).keys();
            for(let file of files_test){
                new Promise((resolve,reject)=>{
                    // console.log(file)
                    axios.get("./files/" + file).then(res=>{
                        resolve(res)
                    }, err=>{
                        reject(err)
                    })
                }).then(res=>{
                    // console.log(res)
                    this.contents.push({text: res.data, title: file.substring(file.lastIndexOf("/")+1, file.length-3), route: "./files/" + file});
                    // console.log(this.contents)
                })
            }
        },
        methods:{
            open: function (val) {
                console.log(val);
                this.$router.push({
                    path:'/content',
                    query:{val: val}
                })
            }
        }
    }
</script>

<style scoped>
.content{
    max-height: 200px;
    max-width: 400px;
    overflow: hidden;
    /*display: inline-block;*/
    text-overflow: ellipsis;
    /*将对象作为弹性伸缩盒子模型显示*/
    display: -webkit-box;
    -webkit-line-clamp: 5;
    text-align: justify;
    line-height: 2.6em;
    position: relative;
    /*设置子元素排列方式*/
    -webkit-box-orient: vertical;
}

#card{
    margin: 12px;
}


</style>