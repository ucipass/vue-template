<template>
    <b-container fluid>
        <div>
            <b-row align-h="between" class="m-1">
                    <b-form-file
                        v-model="filecsv"
                        placeholder="CSV file..."
                        drop-placeholder="Drop file here..."
                    ></b-form-file>
            </b-row>
            <b-row class="m-1">
                <b-form-textarea
                :value="csvtext"
                @input="csvchange"
                id="textarea-auto-height"
                placeholder="CSV Content..."
                rows="5"
                max-rows="8"
                ></b-form-textarea>
            </b-row>
            <b-row class="m-1">
                <b-form-file
                    v-model="filetmp"
                    placeholder="Template file..."
                    drop-placeholder="Drop file here..."
                ></b-form-file>
            </b-row>
            <b-row class="m-1">
                <b-form-textarea
                :value="template"
                @input="tmpchange"
                id="textarea-auto-height"
                placeholder="Template file with variables enclosed in <>"
                rows="5"
                max-rows="8"
                ></b-form-textarea>
            </b-row>  
        </div>
        <div>
            <result-box 

                :message=results[currentPage-1].result
            ></result-box>    
            <div class="overflow-auto"> 
                <!-- Use text in props -->
                <b-pagination
                v-model="currentPage"
                :total-rows="rows"
                :per-page="perPage"
                first-text="First"
                prev-text="Prev"
                next-text="Next"
                last-text="Last"
                ></b-pagination>
            </div> 
        </div>
    </b-container>
</template>

<script>
const csvj=require('csvtojson/v2')
import ResultBox from './ResultBox.vue'

export default {
  name: 'Generator',
  components: {
    ResultBox
  },
  props: {
    id: {
      default: "GeneratorId",
      type: String
    }
  },
  data: function(){
    return{
      username: 'myuser',
      password: 'mypass',
      csvtext: "index,ip,mask\n1/1,1.1.1.1,255.255.255.0\n1/2,1.1.2.1,255.255.255.0\n1/3,1.1.3.1,255.255.255.0",
      template: "interface Ethernet<index>\n ip address <ip> <mask>",
      filecsv: "",
      filetmp: "",
      rows: 1,
      currentPage: 1,
      perPage: 1,
      results: [{results: ""}]
    }
  },
  methods:{
    csvchange: function(v){
        this.csvtext = v
        this.computeResults()
    },
    tmpchange: function(t){
        this.template = t
        this.computeResults()
    },
    computeResults(){
        return csvj().fromString(this.csvtext)
        .then((array)=>{
            let newresult = []
            this.rows = array.length
            for( let i = 0 ; i< array.length; i++){
                let json = array[i]
                let template = this.template
                console.log("START")
                let result = template
                for( let col in json){
                    let reg = new RegExp("\<"+col+"\>")
                    result = result.replace(reg,json[col])
                }
                console.log(result)
                newresult.push({result: result})
            }
            this.results = newresult
        })   
    }
  },
  mounted: function () {
    this.$nextTick(() => {
      this.computeResults()
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
