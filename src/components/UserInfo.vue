<template>
    <div class="UserInfo">
      <!--如果正在加载显示此div-->
      <div class="loading" v-if="isLoading">
        <img src="../assets/timg.gif">
      </div>
      <div class="userInfomation" v-else>
        <section>
          <img :src="userinfo.avatar_url">   <!--头像-->
          <span>{{userinfo.loginname}}</span>  <!--名称-->
          <p>{{userinfo.score}}积分</p>   <!--积分-->
          <p>注册时间：{{userinfo.create_at | formatDate}}</p>
        </section>
        <div class="replies">
          <p>回复的主题</p>
          <ul>
            <li v-for="item in userinfo.recent_replies">
              <router-link :to="{
                  name:'post_content',
                  params:{
                     id:item.id
                }
              }">
                 {{item.title}}
              </router-link>
            </li>
          </ul>
        </div>
        <div class="topics">
          <p>创建的主题</p>
          <ul>
            <li v-for="item in userinfo.recent_topics">
              <router-link :to="{
                  name:'post_content',
                  params:{
                     id:item.id
                }
              }">
                {{item.title}}
              </router-link>
            </li>
          </ul>
        </div>
      </div>
    </div>
</template>

<script>
    export default {
        name: "UserInfo",
      data(){
          return{
            isLoading:false,
            userinfo:{}
          }
      },
      methods:{
        getUseData(){
          this.$http.get(`https://cnodejs.org/api/v1/user/${this.$route.params.name}`)
            .then(res=>{
              this.isLoading=false; //加载成功去除动画
              this.userinfo=res.data.data;
            })
            .catch(function (err) {
              //处理返回失败后的问题
              console.log(err);
            })
        }
      },
      beforeMount() {
        this.isLoading=true; //加载成功之前显示加载动画
        this.getUseData(); //在页面加载之前之前加载数据
      }
    }
</script>

<style scoped>
  .UserInfo{
    background-color: #e1e1e1;
    width: 80%;
    min-height: 500px;
    margin: 0 auto;
    padding-bottom:15px;
  }
  .userInfomation {
    background: white;
    width: 75%;
    margin: 0 auto;
  }
  .userInfomation section {
    padding: 5px 12px 12px 12px;
  }
  .userInfomation img {
    width: 30px;
  }
  .userInfomation li {
    list-style:none;
  }
  .userInfomation .replies,
  .userInfomation .topics {
    font-size: 0.72rem;
    border-top: 10px #DDDDDD solid;
  }
  .userInfomation > div > p {
    padding: 10px 0 10px 10px;
    background-color: rgba(212, 205, 205, 0.17);
    font-size: 0.75rem;
    margin: 0;
  }
  .userInfomation > div >ul > li {
    padding: 4px 0 4px 12px;
    white-space: nowrap;
    font-size: 0.72rem;
    text-overflow: ellipsis;
    overflow: hidden;
    line-height: 30px;
    vertical-align: middle;
  }
  .userInfomation > div >ul > li > a {
    color: #094E99;
    text-decoration: none;
  }
</style>
