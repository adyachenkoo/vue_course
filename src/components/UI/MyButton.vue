<template>
    <button class="button"> 
        <slot></slot>    
    </button>
</template>
<script>
export default {

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