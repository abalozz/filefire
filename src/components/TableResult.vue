<template>
    <table>
        <thead>
            <tr>
                <th v-for="(field, key) in file.lines[0].fields" :key="key">{{ field.name }}</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(line, indexOfLine) in lines" :key="indexOfLine">
                <td v-for="(fieldValue, indexOfField) in line" :key="indexOfField">
                    <span>{{ fieldValue }}</span>
                </td>
            </tr>
        </tbody>
    </table>
</template>

<script>

    export default {
        name: 'TableResult',
        props: {
            file: Object,
        },
        computed: {
            lines() {
                return this.file.content.split('\n')
                    .filter(line => line)
                    .map(line => {
                        return this.file.lines[0].fields.map(field => {
                            return line.substring(
                                field.startPosition - 1,
                                field.startPosition - 1 + field.size
                            );
                        });
                    });
            },
        },
    };

</script>

<style scoped>
    table {
        margin: .5rem;
        border-collapse: collapse;
    }

    th {
        border-bottom: 1px solid black;
    }

    th, td {
        text-align: left;
        padding: .3rem .5rem;
    }

    th:not(:last-child), td:not(:last-child) {
        border-right: 1px solid black;
    }

    span {
        font-family: 'Courier New', Courier, monospace;
        white-space: pre-wrap;
        background-color: #eee;
    }

    tbody tr:hover {
        background-color: #fda;
    }
</style>
