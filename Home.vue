
<template>
<div>
<div class="heading" :class=" isDataPresent ? 'side':'bottom' " > Link Viewer </div>
<div class="contentHolder" :class=" isDataPresent ? 'side':'bottom' " >
  
 
  <div class="searchForm" :class="{'side' : isDataPresent  , 'collapsed' : isDataPresent && isCollapsed}" >   
    <div class="inputHolder">
      <input type="text" class="inputTxt"  v-model="schemaName" placeholder="Schema name">
    </div>   
    <div class="inputHolder">
      <input type="text" class="inputTxt" v-model="tableName" placeholder="Table name">
    </div>    
    <div class="inputHolder btnHolder">  
      <button type="button" class="btn-slide-line center" v-on:click="formSubmit">
        <span>Ask Wolverine!</span>
      </button>
    </div>
 </div>
 
  <div class="togglerHolder" :class=" isCollapsed ? 'collapsed':'open' " v-on:click="toggleCollapse">
    <button v-if="isDataPresent" class="toggler" ></button>
  </div>

 <div class="treeViewer"> 
   <vo-basic  v-if="isDataPresent" :key="componentKey" :data="chartDataJSON" :pan="true" :zoom="true"></vo-basic>
 </div>

</div>
</div> 
</template>


<script>
import { VoBasic } from 'vue-orgchart'

export default {
  name: 'HelloWorld',
  props: {
    msg: String,
    children:Object,
    chartDataFromAjax:Object
  },
  computed : {
      chartDataJSON: function(){
          console.log("hello")
          console.log(this.chartDataFromAjax)
          this.$forceUpdate();
          return (this.chartDataFromAjax);
      }
  },
  components: {
    VoBasic
  },
  created () {
    
  },
  data: function(){
  return{
      schemaName: '',
      tableName: '',
      isDataPresent:false,
      isCollapsed: false,
      componentKey: 0,
      output: ''
    }
  },
  methods:{
      
      forceRerender() {
       this.componentKey += 1;  
      },
      toggleCollapse(){
        this.isCollapsed = !this.isCollapsed;
      },
      formSubmit(e) {
          e.preventDefault();
         /* let currentObj = this; */

          this.isDataPresent = true;
          this.chartDataFromAjax = {
              name: 'Master_table',
                children: [
                  { name: 'table1' },
                  {
                    name: 'table1.1',
                    children: [{ name: 'table1.1.1' }]
                  },
                  {

                    name: 'table2',
                    children: [{ name: 'table2.1' },{ name: 'table2.1' }]
                  },{   

                    name: 'table2',
                    children: [{ name: 'table2.1' },{ name: 'table2.1' }]
                  },{

                    name: 'table2',
                    children: [{ name: 'table2.1' },{ name: 'table2.1' }]
                  }
                ]
          }
          this.forceRerender();
          console.log(this.chartDataFromAjax);
          /*this.axios.post('http://localhost:8000/yourPostApi', {
              schemaName: this.schemaName,
              tableName: this.tableName
          })
          .then(function (response) {
              currentObj.output = response.data;
          })
          .catch(function (error) {
              currentObj.output = error;
          });*/
      }
  },
  mounted() {

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

#parentChildHolder{
  display:flex;
}
.toggler{
    width: 23px;
    height: 48px;
    cursor: pointer;
    background: rgba(255,255,255,0.9) url('../../assets/toggle.png') 7px center/7px 10px no-repeat;
    border-left: 1px solid #D4D4D4;
    box-shadow: 0px 1px 4px rgba(0, 0, 0, 0.3);
}
.toggler:focus{
  outline:none;
}
.togglerHolder.collapsed{
  transform: scaleX(-1);
}
.togglerHolder{
      margin-top: 30px;
    margin-right: 26px;
}
.panHolder{
  display:none;
}
.contentHolder.side{
  display:flex;
}
.panBtn{
      width: 50px;
    background: grey;
    color: white;
}
.searchForm{
  margin-top:30px;
  transition: 1s all;
  width:370px;
  margin: 30px auto;

}
.node{
  cursor:pointer;
}
.searchForm div{
    width: 100%;
    overflow: hidden;
}
.searchForm.side{
       box-shadow: 2px -1px 19px 14px #00800094;
      padding: 120px 0px;
}
.searchForm.collapsed{     
    width: 0px;
}
.inputTxt{
    border: none;
    border-bottom: 1px solid grey;
    padding: 10px 0px;
    text-align: center;
    width: 350px;
}
.inputTxt:focus{
  outline:none !important;
  border-bottom: 2px solid green !important;
}
.heading.side{
    font-size: 20px;
    font-style: italic;
    color: #254b19d6;
    margin-bottom: 13px;
    text-align: left;
}
.heading{
    font-size: 40px;
    font-style: italic;
    color: #254b19d6;
    margin-bottom: 37px
}
/* button css */


 .btnHolder {
   display: flex;
   align-items: center;
   justify-content: space-between;
}
 button.btn-slide-line {
  position: relative;
    margin: 35px auto;
    padding: 5px 12px;
    height: 38px;
    width: 200px;
    outline: none;
    text-decoration: none;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-pack: center;
    -ms-flex-pack: center;
    justify-content: center;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    cursor: pointer;
    text-transform: uppercase;
    background-color: #fff;
    border: 1px solid rgb(4, 143, 27);
    border-radius: 10px;
    color: #214f32;
    font-weight: 400;
    font-size: 20px;
    font-family: inherit;
    z-index: 0;
    overflow: hidden;
    -webkit-transition: all 0.3s cubic-bezier(0.02, 0.01, 0.47, 1);
    transition: all 0.3s cubic-bezier(0.02, 0.01, 0.47, 1);
}
 button span {
    color: #629d3f;
    font-size: 12px;
    font-weight: 500;
    letter-spacing: 0.7px;
    font-weight: bold;
}
 button:hover {
   animation: rotate 0.7s ease-in-out both;
}
 button:hover span {
   animation: storm 0.7s ease-in-out both;
   animation-delay: 0.06s;
}
 @keyframes rotate {
   0% {
     transform: rotate(0deg) translate3d(0, 0, 0);
  }
   25% {
     transform: rotate(3deg) translate3d(0, 0, 0);
  }
   50% {
     transform: rotate(-3deg) translate3d(0, 0, 0);
  }
   75% {
     transform: rotate(1deg) translate3d(0, 0, 0);
  }
   100% {
     transform: rotate(0deg) translate3d(0, 0, 0);
  }
}
 @keyframes storm {
   0% {
     transform: translate3d(0, 0, 0) translateZ(0);
  }
   25% {
     transform: translate3d(4px, 0, 0) translateZ(0);
  }
   50% {
     transform: translate3d(-3px, 0, 0) translateZ(0);
  }
   75% {
     transform: translate3d(2px, 0, 0) translateZ(0);
  }
   100% {
     transform: translate3d(0, 0, 0) translateZ(0);
  }
}
 .btn-pill:before, .btn-pill:after {
   position: absolute;
   right: 0;
   bottom: 0;
   width: 100px;
   height: 100px;
   border-radius: 50%;
   background: #1d89ff;
   content: '';
   opacity: 0;
   transition: transform 0.15s cubic-bezier(0.02, 0.01, 0.47, 1), opacity 0.15s cubic-bezier(0.02, 0.01, 0.47, 1);
   z-index: -1;
   transform: translate(100%, -25%) translate3d(0, 0, 0);
}
 .btn-pill:hover:before, .btn-pill:hover:after {
   opacity: 0.15;
   transition: transform 0.2s cubic-bezier(0.02, 0.01, 0.47, 1), opacity 0.2s cubic-bezier(0.02, 0.01, 0.47, 1);
}
 .btn-pill:hover:before {
   transform: translate3d(50%, 0, 0) scale(0.9);
}
 .btn-pill:hover:after {
   transform: translate(50%, 0) scale(1.1);
}
 .btn-shine {
   border: 1px solid;
   overflow: hidden;
   position: relative;
}
 .btn-shine span {
   z-index: 20;
}
 .btn-shine:after {
   background: #38ef7d;
   content: "";
   height: 155px;
   left: -75px;
   opacity: 0.4;
   position: absolute;
   top: -50px;
   transform: rotate(35deg);
   transition: all 550ms cubic-bezier(0.19, 1, 0.22, 1);
   width: 50px;
   z-index: -10;
}
 .btn-shine:hover:after {
   left: 120%;
   transition: all 550ms cubic-bezier(0.19, 1, 0.22, 1);
}
 .btn-slide-line.center:after {
   left: 50%;
}
 .btn-slide-line:after {
   position: absolute;
   right: 0;
   left: auto;
   transition: 0.3s;
   content: '';
   width: 0;
   bottom: 0;
   height: 3px;
   background: green;
}
 .btn-slide-line:hover {
   cursor: pointer;
}
 .btn-slide-line:hover:after {
   width: 100%;
   left: 0;
}
 .inspire a {
   text-decoration: none;
}
 
/*button css end*/
</style>
