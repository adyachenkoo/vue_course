<template>
    <button class="button"> 
        <slot></slot>    
    </button>
</template>
<script>
export default {
    name: 'MyButton'
}

</script>
<style scoped>
.button {
    padding: 10px 15px;
    color: teal;
    border: 1px solid teal;
    background: none;
}
</style>