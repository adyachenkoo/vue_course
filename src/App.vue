<template>
    <div class="app">
        <h1>Страница с постами</h1>
        <div class="app__buttons">
            <MyButton
            @click="dialogVisible = true"
            >
            Создать пост
            </MyButton>
            <MySelect
            v-model="selectedSort"
            :options="options"
            />
        </div>
        <MyDialog
        v-model:show="dialogVisible"
        >
            <PostForm 
            @create="createPost"
            />
        </MyDialog>
        <PostList 
        v-if="!isPostsLoading"
        :posts="sortedPosts"
        @remove="removePost"
        />
        <h2
        v-else=""
        >
        Посты загружаются...
        </h2>
    </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import axios from "axios";
export default {
    components: {
        PostList, PostForm
    },
    data() {
        return {
            posts: [],
            dialogVisible: false,
            isPostsLoading: false,
            selectedSort: '',
            options: [
                {
                    value: 'title',
                    name: 'По заголовку'
                },
                {
                    value: 'body',
                    name: 'По описанию'
                },
            ]
        }
    },
    methods: {
        createPost(post){
            this.posts.push(post);
            this.dialogVisible = false;
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id);
        },
        async fetchPosts() {
            try {
                this.isPostsLoading = true;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10');
                this.posts = response.data;
            } catch (e) {
                alert(e);
            } finally {
                this.isPostsLoading = false;
            }
        } 
    },
    mounted(){
        this.fetchPosts();
    },
    computed: {
        sortedPosts(){
            return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]));
        
        }
    },
    watch: {
        
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
    overflow-x: hidden;
    padding: 20px;
}
.app__buttons {
    margin: 15px 0;
    display: flex;
    justify-content: space-between;
}
</style>