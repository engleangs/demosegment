<template>
    <base-table :data="tableData"
                thead-classes="text-primary">
      <template slot-scope="{row}">
        <td>
          <base-checkbox v-model="row.done">
          </base-checkbox>
        </td>
        <td>
          <p class="title">{{row.title}}</p>
          <p class="text-muted">{{row.description}}</p>
        </td>
        <td class="td-actions text-right">
          <base-button type="link" aria-label="edit button">
            <i class="tim-icons icon-pencil"></i>
          </base-button>
        </td>
      </template>
    </base-table>
</template>
<script>
  import {BaseTable} from '@/components'

  export default {
    components: {
      BaseTable
    },
    events:{
      idChange(id) {
          console.log( 'id ', id);
      }
    },
    methods:{
      idChange() {
        console.log('id change');
      }
    },
    props:{
      customId: {
        required:true,
            type:Number,
            default:-1
      }
    },
    watch:{
      customId(oldVal,newVal){
        // let newValue = newVal?newVal:null;
           console.log( oldVal, newValue);
      }
    },
    computed: {
      tableData() {
        return [
          {
            id:1,
            title:'hello world'
          }
        ]
      }
    }
  }
</script>
<style>
</style>
