<template>
  <div id="app">
    <FileSelector :files="files" :visibleFileKey="visibleFileKey" />
    <Form :file="file" />
    <TableResult :file="file" />
  </div>
</template>

<script>
    import FileSelector from './components/FileSelector.vue';
    import Form from './components/Form.vue';
    import TableResult from './components/TableResult.vue';

    export default {
        name: 'app',
        computed: {
            files() {
                return this.$store.state.files;
            },
            visibleFileKey() {
                return this.$store.state.visibleFileKey;
            },
            file() {
                return this.files[this.visibleFileKey];
            },
        },
        created() {
            if (this.$store.state.files.length === 0) {
                this.$store.commit('createFile');
            }
        },
        components: {
            FileSelector,
            Form,
            TableResult,
        },
    };
</script>

<style>
body {
    margin: 0;
    width: max-content;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
