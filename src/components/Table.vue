<template>
    <section id="table">
        <h3>Table</h3>
        <table>
            <thead>
                <tr>
                    <th v-for="head in tableHead">
                        {{ head }}
                    </th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="marilyn in marilynTable">
                    <td :id="marilyn['Name']" v-for="item in marilyn">
                       {{ item }}
                    </td>
                </tr>
            </tbody>
        </table>
    </section>
</template>

<script>
export default {
    name: "Table",
    props: ['marilyns'],
    data() {
        return {
            marilynTable: [],
            tableHead: []
        }
    },
    mounted() {
        this.marilynTable = JSON.parse(JSON.stringify(this.marilyns))
        this.tableHead = Object.keys(this.marilynTable[0])
    }
}
</script>