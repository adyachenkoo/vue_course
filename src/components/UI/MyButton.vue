<template>
    <button class="button"> {{ text }} </button>
</template>
<script>
export default {
    props: {
        text: {
            type: String,
            required: true,
        }
    }
}

</script>
<style scoped>
.button {
    margin-top: 15px;
    align-self: flex-end;
    padding: 10px 15px;
    color: teal;
    border: 1px solid teal;
    background: none;
}
</style>