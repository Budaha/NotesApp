<template>
    <div class="message">
        <p> {{ message }}</p>
    </div>
</template>

<script>
export default {
    name: "messageComponent",
    props: {
        message: {
        type: String,
        required: true,
        }
    }
}
</script>

<style scoped>
.message {
    text-align: center;
    padding: 20px;
    color: red;
}
</style>
