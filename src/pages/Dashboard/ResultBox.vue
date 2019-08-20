<template>    
    <div class="col-4">
        <card>
            <h4 class="card-title">Segment type : {{title}}</h4>
            <div class="card-text">
                <p>Total word : {{totalWord}}</p>
                <p>Total error : {{totalError}} </p>
                <p>Error rate : {{errorRate}} </p>
            <div class="line"></div>
            <div class="words">
                <div class="word-item" v-for="word in words" v-bind:key="word">
                    {{word}}
                </div> 
            </div>
            </div>
        </card>
    </div>    
</template>
<script>
export default {
    props:{
        title:{
            type:String,
            required:false,
            default:"Segmentation",

        },
        totalWord:{
            type:Number,
            required:false,
            default:0
        },
        totalError:{
            type:Number,
            required:false,
            default:0
        },
        errorRate: {
            type:Number,
            required:false,
            default:0
        },
        words:{
            type:Array,
            required:false,
            default:[],
        }
        
    }
}
</script>
<style>
.line {
    height: 1px;
    width: 100%;
    background: #fff;
    margin-bottom: 10px;
}
.word-item {
    max-width: 100px;
    float: left;
    border-radius: 5px;
    border:1px solid #cccccc;
    padding: 10px;
    margin: 2px;
}
</style>