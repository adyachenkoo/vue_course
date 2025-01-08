<template>
    <form action="" @submit.prevent>
        <h4>Создание поста</h4>
        <MyInput 
        v-model="post.title"
        @input="post.title = $event.target.value"
        placeholder="Название"
        />
        <MyInput
        v-model="post.body"
        @input="post.body = $event.target.value"
        placeholder="Описание"
        />
        <MyButton 
        style="margin-top: 15px; align-self: flex-end;"
        @click="createPost"
        >
        Создать
        </MyButton>
    </form>
</template>
<script>
export default {
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
</style>