<template>
    <div class="col-lg-12">
        <card>
             <form @submit.prevent>
                
                <label >{{title}}</label>
                <p >{{content}}</p>
                
                <base-button native-type="submit" type="primary" @click="doSegment">Segment word</base-button> &nbsp;
                <base-button native-type="reset" type="cancel" @click="back">
                <i class="tim-icons icon-double-left"></i>
                Back</base-button> 
                </form>
                
        </card>
        <div>
        <card v-show="showResult">
            
                <div class="col-12">
                    <h4>Result </h4>
                    <div class="row">
            <result-box v-for=" (result,key) in segmentResult" v-bind:key="key"
                v-bind:title="key"
                v-bind:words="result.words"
                v-bind:total-error="result.errorCount"
                v-bind:total-word="result.tottal"
                v-bind:error-rate="result.errorRate"
            ></result-box>
                </div>
            </div>
        </card>
        </div>
        

    </div>
</template>
<script>
import ResultBox from './ResultBox';
import { truncate } from 'fs';
const SampleResult = {
    forward:{
        words:[
            "yes","No","Hello","World"
        ],
        errorCount : 10,
        total:20,
        errorRate : 0.5,
        errors :[
            "dkdkd"
        ]
    },
    backward:{
         words:[
            "yes","No","Hello","World"
        ],
        errorCount : 10,
        total:20,
        errorRate : 0.5,
        errors :[
            "dkdkd"
        ]
    },
    bidirectional:{
        words:[
            "yes","No","Hello","World","test","ask","demo","this"
        ],
        errorCount : 10,
        total:20,
        errorRate : 0.5,
        errors :[
            "dkdkd"
        ]
    }
}
export default {
     components: {
         ResultBox
     },
    props:{
        title:{
            type:String,
            required:false,
            default:"Hello world"
        },
        content:{
            type:String,
            required:false,
            default:"This is the demo content"
        },
        showResult:{
            type:Boolean,
            required:false,
            default:false
        }
    },
    data (){
        let segmentResult = SampleResult;
    return {
            segmentResult:segmentResult,
    };
        
        
    }
    ,methods:{
        doSegment(){
            console.log('yes');
            this.showResult = true;
        },
        back(){
            this.$emit('content-back');
        }
    }
}
</script>
<style scoped>

</style>