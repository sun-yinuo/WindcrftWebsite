<template>
  <div class="demo-tabs-style2" style="margin-top: 10px">
  <Tabs value="tabs" type="card">
    <TabPane label="封禁" name="ban">
      <Grid :col="6" :hover="true">
        <GridItem>玩家</GridItem>
        <GridItem>来源</GridItem>
        <GridItem>原因</GridItem>
        <GridItem>封禁类型</GridItem>
        <GridItem>封禁时间</GridItem>
        <GridItem>解禁时间</GridItem>
      </Grid>
      <Grid :col="6" :hover="true" v-for="ban in banList">
        <GridItem>{{ban.name}}</GridItem>
        <GridItem>{{ban.source}}</GridItem>
        <GridItem>{{ban.reason}}</GridItem>
        <GridItem>{{ban.banType}}</GridItem>
        <GridItem>{{ban.banTime}}</GridItem>
        <GridItem>{{ban.unBanTime}}</GridItem>
      </Grid>
    </TabPane>
    <TabPane label="警告" name="waring">
      <Grid :col="4" :hover="true">
        <GridItem>玩家</GridItem>
        <GridItem>来源</GridItem>
        <GridItem>原因</GridItem>
        <GridItem>时间</GridItem>
      </Grid>
      <Grid :col="4" :hover="true" v-for="waring in waringList">
        <GridItem>{{waring.name}}</GridItem>
        <GridItem>{{waring.source}}</GridItem>
        <GridItem>{{waring.reason}}</GridItem>
        <GridItem>{{waring.time}}</GridItem>
      </Grid>
    </TabPane>
    <TabPane label="禁言" name="prohibit">
      <Grid :col="5" :hover="true">
        <GridItem>玩家</GridItem>
        <GridItem>来源</GridItem>
        <GridItem>原因</GridItem>
        <GridItem>封禁时间</GridItem>
        <GridItem>解禁时间</GridItem>
      </Grid>
      <Grid :col="5" :hover="true" v-for="prohibit in prohibitList">
        <GridItem>{{prohibit.name}}</GridItem>
        <GridItem>{{prohibit.source}}</GridItem>
        <GridItem>{{prohibit.reason}}</GridItem>
        <GridItem>{{prohibit.banTime}}</GridItem>
        <GridItem>{{prohibit.unBanTime}}</GridItem>
      </Grid>
    </TabPane>
  </Tabs>
  </div>
</template>

<style>
.demo-tabs-style2 > .ivu-tabs.ivu-tabs-card > .ivu-tabs-bar .ivu-tabs-tab{
  border-radius: 0;
  background: #fff;
}
.demo-tabs-style2 > .ivu-tabs.ivu-tabs-card > .ivu-tabs-bar .ivu-tabs-tab-active{
  border-top: 1px solid #3399ff;
}
.demo-tabs-style2 > .ivu-tabs.ivu-tabs-card > .ivu-tabs-bar .ivu-tabs-tab-active:before{
  content: '';
  display: block;
  width: 100%;
  height: 1px;
  background: #3399ff;
  position: fixed;
  top: 0;
  left: 0;
}
</style>

<script>
import request from "@/utils/request";

export default {
  data() {
    return {
      banList: null,
      prohibitList: null,
      waringList: null,
    }
  },
  created() {
    this.getBanList();
    this.getProhibitList()
    this.getWaringList()
  },
  methods: {
    getBanList(){
      request.get("/bancrud/api/getBanList").then(res =>{
        this.banList = res
        console.log(this.banList);
      })
    },
    getProhibitList(){
      request.get("/bancrud/api/getProhibitList").then(res => {
        this.prohibitList = res;
        console.log(this.prohibitList);
      })
    },
    getWaringList(){
      request.get("/bancrud/api/getWaringList").then(res => {
        this.waringList = res;
        console.log(this.waringList);
      })
    }
  }
}
</script>