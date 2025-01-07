<template>
    <div class="app">
        <PostForm 
        @create="createPost"
        />
        <PostList 
        :posts="posts"
        @delete="deletePost"
        />
    </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
export default {
    components: {
        PostList, PostForm
    },
    data() {
        return {
            posts: [
                {id:1, title:"POST 1", body:"Описание поста 1"},
                {id:2, title:"POST 2", body:"Описание поста 2"},
                {id:3, title:"POST 3", body:"Описание поста 3"},
            ],
        }
    },
    methods: {
        createPost(post){
            this.posts.push(post);
        },
        deletePost(id) {
            console.log(this.posts.find((element)=>{
                element.id == id;
            }))
        }
    }
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
.app {
    padding: 20px;
}
</style>