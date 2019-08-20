<template>
<div>
    <base-table :data="items"
                thead-classes="text-primary" tbody-classes="custom-body" >
      <template slot-scope="{row}" class="custom" >
        
        <td @click="crawlPage(row)">
          <p class="title">{{row.title}}</p>
          <p class="text-muted">{{row.description}}</p>
        </td>
        <td class="td-actions text-right" @click="crawlPage(row)">
          <base-button type="link" aria-label="edit button" @click="crawlPage(row)">
            <i class="tim-icons icon-cloud-download-93"></i>
          </base-button>
        </td>
      </template>
    </base-table>
    
</div>  
</template>

<script>
  import {BaseTable} from '@/components'
  import {Modal} from '@/components'
  import axios from 'axios'
  const CRAWL_URL = 'https://secret-badlands-72461.herokuapp.com/demo/crawls';
  const DEF_HEADER = {
     'Accept': 'application/json',
      'Content-Type': 'application/json',
      'Access-Control-Allow-Origin': '*' 
  };
  

  export default {
    components: {
      BaseTable
    },
    props:{
      data: {
        required:false,
            type:String,
            default: "",
          immediate:true,
          handler(oldVal,newVal){
            console.log("change...");
          }
      },
      items : {
        type:Array
      }
    },
    watch:{
      data(oldVal,newVal){
        console.log(' watch....');
      }
    },
    methods:{
        fetchData(id){
          console.log('fetch ',id);
          
        }
        ,crawlPage( row) {
            let fetchUrl = row.url;
            this.$emit('custom', fetchUrl);
           


        },
        showModal(){
          this.$modal.show("demo-modal");
        },
        hideModal(){
          this.$modal.hide('demo-modal');
        }
    },
    computed: {
      tableData() {
        return [
        
        ]
      },
      modals(){
        return {
          modal0:false
        }
      }
    }
  }
</script>
<style >
  .custom-body tr td:hover {
    cursor: pointer;
    color:white;
  }
  .custom-body tr:hover .text-muted  , .custom-body tr:hover .btn{
    color: #cdcdcd !important;
  }
</style>
