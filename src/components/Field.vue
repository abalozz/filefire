<template>
    <div>
        <label :for="label">{{ label }}</label>
        <input type="text" :id="label" :value="value" @keyup="$emit('change', $event.target.value)">
    </div>
</template>

<script>
    export default {
        name: 'Field',
        props: {
            label: String,
            value: [String, Number],
        },
    };
</script>

<style scoped>
    label {
        display: block;
    }
</style>
