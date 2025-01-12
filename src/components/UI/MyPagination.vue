<template>
    <div 
    class="page__wrapper"
    >
        <div 
        v-for="pageNumber in totalPage"
        class="page"
        :class="{
            'current-page' : pageNumber === page
        }"
        :key="page"
        @click="changePage(pageNumber)"
        >
            {{ pageNumber }}
        </div>
    </div>
</template>
<script>
export default {
    name: 'MyPagination',
    props: {
        page: 1,
        totalPage: 0,
    },
    methods: {
        changePage(pageNumber) {
            this.$emit('update:page', pageNumber)
        }
    }
}
</script>
<style scoped>
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