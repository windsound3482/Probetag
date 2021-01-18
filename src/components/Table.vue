<template>
   <div>
        <md-table>
            <thead>
                <md-table-row>
                    <md-table-head v-for="column in dataColums" :key="column">{{column}}</md-table-head>
                    <md-table-head>Action</md-table-head>
                </md-table-row>
            </thead>
            <tbody>
                <md-table-row v-for="(row,rowIndex) in datasource" :key="rowIndex">
                    <md-table-cell v-for="key in dataColums" :key="key">
                        <input  v-model="row[key]"/>
                    
                    </md-table-cell>
                    <md-table-cell>
                        <i class="material-icons" v-on:click="deleteRow(rowIndex)">clear</i>
                    </md-table-cell>
                </md-table-row>
            </tbody>
        </md-table>
        <i class="material-icons" v-on:click="addRow">add_circle</i>
    </div>
</template>

<script>
  

  export default {
    name: 'Table',
    props : [],
    data() {
        return {
            dataColums:[
                "id","name","email","gender","title"
            ],
            datasource:[
                {
                id: 1,
                name: 'Shawna Dubbin',
                email: 'sdubbin0@geocities.com',
                gender: 'Male',
                title: 'Assistant Media Planner'
                },
                {
                id: 2,
                name: 'Odette Demageard',
                email: 'odemageard1@spotify.com',
                gender: 'Female',
                title: 'Account Coordinator'
                },
                {
                id: 3,
                name: 'Lonnie Izkovitz',
                email: 'lizkovitz3@youtu.be',
                gender: 'Female',
                title: 'Operator'
                },
                {
                id: 4,
                name: 'Thatcher Stave',
                email: 'tstave4@reference.com',
                gender: 'Male',
                title: 'Software Test Engineer III'
                },
                {
                id: 5,
                name: 'Clarinda Marieton',
                email: 'cmarietonh@theatlantic.com',
                gender: 'Female',
                title: 'Paralegal'
                }
            ]
        }
    },
    methods: {
        

        addRow() {
            this.datasource.push({})
            //appData.updated()       

        },
        deleteRow(row) {
            console.log(row);
            this.datasource.splice( parseInt(row), 1)
            //appData.updated()
        },
    },
    mounted() {
        
    },
  }
</script>

<style lang="scss" scoped>
  .md-field {
    max-width: 300px;
  }
</style>