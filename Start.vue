<template>
  <div>
    <div class="messenger-header">
      <div class="messenger-logo">
        <img src="../../../assets/img/logo.png">
        <label><b>{{config.APP_NAME}}</b></label>
      </div>
      <div class="messenger-info">
        <h3 v-if="user.username.length < 20">Hi {{user.username}}!</h3>
        <h3 v-else>Hi {{user.username.substr(0, 17)}}...!</h3>
        <p>
          Hello! What question do you have about {{config.APP_NAME}}? We'd love to help you.
        </p>
      </div>
    </div>
    <div class="conversation-start">
      <div class="start-header">
        <label class="title">Start a conversation</label>
        <label class="description">The team typically replies in a few minutes.</label>
      </div>
      <div class="start-images"></div>
      <div class="start-actions">
        <button class="btn btn-primary" @click="changeConversationStatus('new-conversation')"><i class="fa fa-send"></i> New Conversation</button>
        <label class="text-danger previous pull-right" @click="changeConversationStatus('previous')">See previous</label>
      </div>
    </div>
  </div>
</template>
<style scoped lang="scss">
@import "~assets/style/colors.scss";
.messenger-header{
  width: 100%;
  float: left;
  height: 40vh;
  border-top-right-radius: 10px;
  border-top-left-radius: 10px;
  background-image: linear-gradient(to bottom right, #ffffff, $primary);
}
.messenger-header .messenger-logo{
  height: 50px;
  float: left;
  width: 90%;
  margin-right: 5%;
  margin-left: 5%;
  margin-top: 20px;
}
.messenger-logo img{
  width: 40px;
  height: 40px;
  float: left;
  margin-top: 5px;
}
.messenger-logo label{
  line-height: 40px;
  font-size: 24px;
  margin-top: 5px;
  color: $primary;
}
.messenger-header .messenger-info{
  float: left;
  width: 80%;
  margin-right: 10%;
  margin-left: 10%;
  text-align: justify;
  padding-top: 15px;
}
.messenger-info h3{
  text-transform: capitalize;
  color: #000;
}

.conversation-start{
  height: 25vh;
  margin-right: 5%;
  margin-left: 5%;
  width: 90%;
  float: left;
  background: #fff;
  margin-top: -25px;
  border-radius: 5px;
  border: solid 1px #ddd;
}
.start-header{
  height: 50px;
  width: 90%;
  margin-right: 5%;
  margin-left: 5%;
  margin-top: 10px;
}
.start-actions{
  height: 50px;
  width: 90%;
  margin-right: 5%;
  margin-left: 5%;
}
.start-header .title{
  font-size: 14px;
  line-height: 14px;
  width: 100%;
  float: left;
}
.start-header .description{
  line-height: 12px;
  width: 100%;
  float: left;
  color: #888;
}
.previous{
  line-height: 35px;
}
.previous:hover{
  text-decoration: underline;
  cursor: pointer;
}
@media (max-width: 991px){

}
</style>
<script>
import ROUTER from 'src/router'
import AUTH from 'src/services/auth'
import CONFIG from 'src/config.js'
import axios from 'axios'
export default {
  mounted(){
  },
  data(){
    return {
      user: AUTH.user,
      config: CONFIG,
      data: null
    }
  },
  methods: {
    redirect(parameter){
      ROUTER.push(parameter)
    },
    changeConversationStatus(status){
      if(status === 'new-conversation'){
        AUTH.support.messages = null
      }
      this.$parent.conversationStatus = status
    }
  }
}
</script>
