<template>
    <div class="post" >
        <div>
            <div><strong>Id:</strong> {{ post.id }}</div>
            <div><strong>Название: </strong> {{ post.title }} </div>
            <div><strong>Описание: </strong> {{ post.body }} </div>
        </div>
        <div class="post__btns">
            <MyButton
            @click="$emit('remove', post)"
            >
                Удалить
            </MyButton>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        post: {
            type: Object,
            required: true
        }
    },
    methods: {
        deletePost() {
            this.$emit('delete', this.post.id);
        }
    }
}

</script>
<style scoped>
.post {
    padding: 15px;
    border: 2px solid teal;
    margin-top: 15px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
</style>