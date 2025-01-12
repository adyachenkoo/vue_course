<template>
    <div class="app">
        <h1>Страница с постами</h1>
        <MyInput
            v-model="searchQuery"
            placeholder="Поиск..."
        />
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
        :posts="sortedAndSearchesPosts"
        @remove="removePost"
        />
        <h2
        v-else=""
        >
        Посты загружаются...
        </h2>
        <div 
        class="page__wrapper">
            <div 
            v-for="pageNumber in totalPage"
            :key="page"
            class="page"
            :class="{
                'current-page' : pageNumber === page
            }"
            @click="changePage(pageNumber)"
            >
                {{ pageNumber }}
            </div>
        </div>
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
            searchQuery: '',
            page: 1,
            limit: 10,
            totalPage: 0,
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
        changePage(pageNumder) {
            this.page = pageNumder;
            this.fetchPosts()
        },
        async fetchPosts() {
            try {
                this.isPostsLoading = true;
                const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
                    params: {
                        _page: this.page,
                        _limit: this.limit,
                    }
                });
                this.totalPage = Math.ceil(response.headers['x-total-count'] / this.limit)
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
            
        },
        sortedAndSearchesPosts(){
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
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
.page__wrapper {
    display: flex;
    margin-top: 15px;
}
.page {
    border: 1px solid black;
    padding: 10px;
}
.current-page {
    border: 2px solid teal;
}
</style>