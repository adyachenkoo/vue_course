<template>
    <form action="" @submit.prevent>
        <h4>Создание поста</h4>
        <input 
        v-model="post.title"
        @input="post.title = $event.target.value"
        class="input" 
        type="text" 
        placeholder="Название"
        >
        <input 
        v-model="post.body"
        @input="post.body = $event.target.value"
        class="input" 
        type="text" 
        placeholder="Описание"
        >
        <MyButton 
        class="button" 
        @click="createPost"
        :text="'Создать'"
        />
    </form>
</template>
<script>
import MyButton from '@/components/UI/MyButton.vue';
export default {
    components: {
        MyButton,
    },
    data() {
        return {
            post: {
                title: '',
                body: '',
            }
        }
    },
    methods: {
        createPost() {
            this.post.id = Date.now();
            this.$emit('create', this.post);
            this.post = {
                title: '',
                body: '',
            }
        },
    }
}
</script>
<style>
form {
    display: flex;
    flex-direction: column;
}
.input {
    width: 100%;
    border: 1px solid teal;
    padding: 10px 15px;
    margin-top: 15px;
}
</style>