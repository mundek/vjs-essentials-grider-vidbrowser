<template>
    <div>
        <!-- -->
        <input @input="onInput" />
    </div>
</template>

<script>
export default {
    name: 'SearchBar',
    methods: {
        onInput: function(event) {
            // method called by input in this template;
            // parent component listens for 'termChange' event
            // by setting listener when instantiating component

            this.$emit('termChange', event.target.value);
        }
    }
};
</script>

<style scoped>
    input {
        width: 75%;

    }

    div {
        text-align: center;
        margin: 20px;
    }
</style>
