<template>
    <div class="pagination">
      <button @click="changeBtn(1)">首页</button>
      <button @click="changeBtn(currentPage>1?currentPage-1:1)">上一页</button>
      <button v-if="jduge" class="pagebtn">......</button>
      <button v-for="btn in pagebtns"
              @click="changeBtn(btn)"
              :class="[{currentPage:btn == currentPage},'pagebtn']">
        {{btn}}
      </button>
      <button @click="changeBtn(currentPage+1)">下一页</button>
    </div>
</template>

<script>
  import $ from 'jquery'
    export default {
        name: "Pagination",
      data(){
        return{
          pagebtns:[1,2,3,4,5,'...'],
          currentPage:1,
          jduge:false
        }
      },
      methods:{
        changeBtn(page){
          this.currentPage=page;
          if(page == 1){
            this.pagebtns=[1,2,3,4,5,'...'];
          }
          if(page>4){
            this.jduge = true;
          }else{
            this.jduge = false;
          }
          if(page == this.pagebtns[4] ){
            this.pagebtns.shift();
            this.pagebtns.splice(4,0,this.pagebtns[3]+1);
          }else if(page == this.pagebtns[0] && page !=1){
            //先在第一个位置加一个
            this.pagebtns.unshift(this.pagebtns[0]-1);
            //移除最后一个数字
            this.pagebtns.splice(5,1);
          }
          this.$emit('handleList',this.currentPage);
        }
      }
    }
</script>

<style scoped>
  .pagination {
    margin-top: 5px;
    margin-bottom: 20px;
    background-color: white;
    padding: 6px 20px;
    border-radius: 5px;
    /*box-shadow: 0px 2px 9px #888888;*/
    border: 1px solid #888888;
  }

  button {
    background-color: #fff;
    border: 1px solid #ddd;
    color: #778087;
    border-radius: 3px;
    outline: none;
    height: 21px;
    cursor: pointer;
    padding: 0 2px;
    width: 55px;
    height: 29px;
  }

  .pagebtn {
    position: relative;
    bottom: 1px;
    width: 40px;
    margin: 0 4px;
  }

  .currentPage {
    color: white;
    background-color: #1f1b1b;

  }
</style>
