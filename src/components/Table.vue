<template>
   <div>
        <md-table class="md-scrollbar">
            <thead>
                <md-table-row>
                    <md-table-head v-for="column in dataColums" :key="column">{{column}}</md-table-head>
                    <md-table-head>Action</md-table-head>
                </md-table-row>
            </thead>
            <tbody >
                <md-table-row v-for="(row,rowIndex) in datasource" :key="rowIndex">
                    <md-table-cell v-for="(item,key) in format" :key="key">
                        <input v-if="item=='string'" type="text" v-model="row[key]" />
                        <input v-if="item=='string/language'" type="text" v-model="row[key]" />
                        <input v-if="item=='string/url'" type="url" v-model="row[key]" />
                        <input v-if="item=='string/phonenum'" type="tel" v-model="row[key]" />
                        <input v-if="item=='string/email'" type="email" v-model="row[key]" />
                        <!-- not all the type of string/uid should be use to define supervisior, adjust later -->
                        <!-- the performance of this this also not good -->
                        <!-- the unique key is not used now, to use it later, add it in javascript -->
                        <md-select v-if="item=='string/uid'"  v-model="row[key]" name="person_supervisior">
                                <md-option v-for="(rowSele,rowIndexSele) in datasource" :key="rowIndexSele" :value="rowSele.person_name">
                                    {{rowSele.person_name}}
                                </md-option>
                        </md-select>
                    </md-table-cell>
                    <md-table-cell>
                        <md-button class="md-icon-button" v-on:click="deleteRow(rowIndex)">
                            <md-icon >clear</md-icon>
                        </md-button>
                        
                    </md-table-cell>
                </md-table-row>
            </tbody>
        </md-table>
        <md-button class="md-icon-button" v-on:click="addRow">
            <md-icon >add_circle</md-icon>
        </md-button>
        
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
            ],
            format:null,
        }
    },
    methods: {
        
        //add new row when needed
        addRow() {
            this.datasource.push({}) 
        },
        //delete one row
        deleteRow(row) {
            this.datasource.splice( parseInt(row), 1)
        },
    },
    async created() {
  // GET request using fetch with async/await
        const baseURL = 'https://api.staging.vdb.st/public/probetag'
                
        const response = await fetch(baseURL, 
                {method: "POST", body: "{}"});
        const data = await response.json();
        this.format = Object.values(data)[0];
        this.dataColums=Object.keys(this.format);
        console.log(Object.values(this.format));

    },
    
  }
</script>

<style lang="scss" scoped>
  .md-field {
    max-width: 300px;
  }
  input{
    border:none;
    :invalid{
        background-color:red;
        color:white;
    }
  }

 
</style>