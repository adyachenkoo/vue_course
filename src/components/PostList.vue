<template>
    <div v-if="posts.length > 0" class="postlist">
        <h3>Список постов</h3>
            <TransitionGroup name="post-list">
                <PostItem 
                v-for="post in posts" 
                :post="post"
                :key="post.id"
                @remove="$emit('remove', post)"
                />
            </TransitionGroup>
        </div>
    <h2 v-else style="color: red">
        Список постов пуст
    </h2>
</template>
<script>
import PostItem from '@/components/PostItem.vue';
export default {
    components: {
        PostItem,
    },
    props: {
        posts: {
            type: Array,
            required: true,
        }
    }
}

</script>
<style scoped>
.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.6s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(80px);
}
.post-list-move {
  transition: transform 0.8s ease;
}
</style>