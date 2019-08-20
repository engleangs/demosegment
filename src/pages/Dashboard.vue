<template>
  <div>

    <div class="row">
      <div class="col-12">
        <card >
          <template slot="header">
            
          </template>
          <div class="chart-area">
            <!-- <line-chart style="height: 100%"
                        ref="bigChart"
                        chart-id="big-line-chart"
                        :chart-data="bigLineChart.chartData"
                        :gradient-colors="bigLineChart.gradientColors"
                        :gradient-stops="bigLineChart.gradientStops"
                        :extra-options="bigLineChart.extraOptions">
            </line-chart> -->
             <form @submit.prevent>
               <base-input label="Please choose website link to fetch and crawl">
        <select class="form-control" id="crawlOption" v-model="crawlId">
          <option value="0">https://www.rfa.org/khmer/indepth/RSS</option>
          <option value="1">http://km.rfi.fr/general/rss</option>
          <option value="2">https://khmer.voanews.com/rssfeeds</option>
          
        </select>
        
      </base-input>
     <base-button native-type="submit" type="primary" @click="fetch">Fetch</base-button>
    </form>
          </div>
        </card>
      </div>
    </div>
    <div class="row" v-show="showWebItem">
      <div class="col-lg-12">
        <card type="web-items" :header-classes="{'text-right': isRTL}">
          <template slot="header">
            <h6 class="title d-inline">Found web items : {{count}}</h6>
            <p class="card-category d-inline">   {{$t('dashboard.today')}}</p>
          
          </template>
          <div class="table-full-width ">
            <h6 v-if="fetchingState==1">Fetching web items  .....</h6>
            <task-list  v-bind:items="webItems" ref="taskListRef" v-on:custom="customEvent"></task-list>
          </div>
        </card>
      </div>
     
    </div>
    <div class="row" v-show="showContent">
      <content-segment v-on:content-back="contentBack" v-bind:show-result="showSegmentResult" ></content-segment>
    </div>
  </div>
</template>
<script>
  import LineChart from '@/components/Charts/LineChart';
  import BarChart from '@/components/Charts/BarChart';
  import * as chartConfigs from '@/components/Charts/config';
  import TaskList from './Dashboard/TaskList';
  import UserTable from './Dashboard/UserTable';
  import ContentSegment from './Dashboard/ContentSegment';
  import config from '@/config';
  import axios from 'axios'; 
import { truncate, truncateSync } from 'fs';
  const FETCH_API_URL = 'https://secret-badlands-72461.herokuapp.com/demo/crawls';
  const DEF_HEADER = {
     'Accept': 'application/json',
      'Content-Type': 'application/json',
      'Access-Control-Allow-Origin': '*' 
  };

  export default {
    components: {
      LineChart,
      BarChart,
      TaskList,
      UserTable,
      ContentSegment
    },
    data() {
      return {
        crawlId:1,
        customId:"",
        showWebItem:false,
        webItems:[],
        showPage :false,
        count : 0,
        fetchingState :0,
        showContent :false,
        showSegmentResult:false
      }
       
    },
    computed: {
      enableRTL() {
        return this.$route.query.enableRTL;
      },
      isRTL() {
        return this.$rtl.isRTL;
      },
      bigLineChartCategories() {
        return this.$t('dashboard.chartCategories');
      }
    },
    methods: {
      customEvent(url){
        console.log(' custom event',url,this.crawlId);
        this.showWebItem = false;
        this.showContent = true;
        
      },
      contentBack(){
          this.showContent = false;
          this.showWebItem = true;
          this.showSegmentResult = false;
      },
      fetch() {
      
        this.showWebItem = true;
        this.$refs.taskListRef.fetchData( this.crawlId);
        let url = FETCH_API_URL+"/"+this.crawlId;
        let that = this;
        this.customId = this.crawlId;
        this.fetchingState = 1;
        this.webItems = [];
        this.showContent = false;
        this.count = 0;
      
      axios
      .get( url ,{
        headers: DEF_HEADER
      })
      .then(response => {
          that.webItems = response.data;
          that.count = that.webItems.length;
          this.fetchingState = 0;
      }
    );

       
      },
    },
    mounted() {
    },
    beforeDestroy() {
      if (this.$rtl.isRTL) {
        this.i18n.locale = 'en';
        this.$rtl.disableRTL();
      }
    }
  };
</script>
<style>
</style>
