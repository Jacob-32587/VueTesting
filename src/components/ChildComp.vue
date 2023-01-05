<script>
export default {
    emits: ['response'],
    props: {
        msg: String
    },
    created() 
    {
        this.$emit('response','hello from child');
    }
}

</script>

<template>
    <h1>Child Component: {{msg}}</h1>
    <slot>
        Fallback content
    </slot>
</template>

<style scoped>

</style>
