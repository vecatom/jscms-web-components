<template>
  <div class="comment-items-parent">
    <v-comment-input :user-comment-item="userCommentItem" @commentAdd="commentAdd"></v-comment-input>
    <div class="comment-part">
      <div class="comment-part-title">
        <div class="my-column-title">
          <span class="my-column-title-icon"></span>
          <span class="my-column-title-text weight-bold">评论区</span>
        </div>
      </div>
      <ul class="comment-list">
        <li class="comment-list-item" v-for="(item,i) in items ">
          <div class="item-left">
				    <span class="item-avatar" style=""><img src="/assets/logo.png"/>	</span>
          </div>
          <div class="item-right" >
            <div class="item-user">
              <span class="item-user-name">{{ item.userName }}</span>
              <span class="item-user-time"> · {{ item.date }}</span>
              <div class="item-user-right">
                <span class="item-user-like" v-if="item.myApplaud" @click="changeApplaud([i],$event)" > 赞 {{item.applaud}}</span>
                <span class="item-user-like item-user-unlike " v-if="!item.myApplaud" @click="changeApplaud([i],$event)" > 赞 {{item.applaud}}</span>
                <a class="item-user-reply" @click="click_repty([i],$event)" >回复</a>
              </div>
            </div>
            <p class="item-text">{{ item.commentContent }}</p>
            <div class="comment-list comment-list-reply" v-for=" (citem,ci) in item.deriveList">
              <ul class="comment-list-ul">
                <li class="comment-list-item">
                  <div class="item-right">
                    <div class="item-user">
                      <span class="item-user-name">{{ citem.userName}}</span>
                      <span class="item-user-time"> · {{citem.date}}</span>
                      <div class="item-user-right">
                        <span class="item-user-like " v-if="citem.myApplaud" @click="changeApplaud([i,ci],$event)"> 赞 {{citem.applaud}}</span>
                        <span class="item-user-like item-user-unlike" v-if="!citem.myApplaud" @click="changeApplaud([i,ci],$event)" > 赞 {{citem.applaud}}</span>
                        <a class="item-user-reply" @click="click_repty([i,ci],$event)">回复</a>
                      </div>
                    </div>
                    <p class="item-text">
                      <span class="item-user-reply" v-if="citem.cl>3">
                        回复 {{citem.replyUserName}} :
                      </span>{{ citem.commentContent }}</p>
                  </div>
                </li>
              </ul>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>

</template>

<script>

  import CommentInput from "./CommetInput.vue";

  export default {
    name: "CommentList",
    components: {
      "v-comment-input": CommentInput
    },
    data() {
      return {
        userCommentItem:{
          "userId": "1",
          "userName": "user123",
          "commentContent": "",
          "docId":123,
          "replyUserId":"",
          "replyUserName":"",
          "rpelyPath":[]
        }
        ,
        items: [{
          "docId":"123", // 文档ID
          "userId": "1",
          "userName": "user123",
          "userImg":"/assets/logo.png",
          "date": "2019-5-1",
          "commentContent": "写得真不错",
          "myApplaud":false,
          "applaud": 5,
          "deriveList": [{            // 第二级以后的评论
            "userId": "2",            // 用户Id
            "userName": "user456",    // 用户名称
            "userImg":"/assets/logo.png",  // 用户头像
            "date": "2019-5-2",    // 评论发生时间，此次接口建议使用时间戳
            "commentContent": "我觉得写的非常好",  // 评论内容
            "applaud": 3,           // 表示赞的个数
            "myApplaud":false,     // 表示本账号是否赞
            "cl":5,                 // 来表示回复层级深度
            "replyUserId":"3",       // 第二级回复的用户Id  (user456 回复的谁）
            "replyUserName":"user798"
          }, {
            "userId": "3",
            "userName": "user789",
            "userImg":"/assets/logo.png",
            "date": "2019-5-3",
            "commentContent": "我觉得写的非常好+1",
            "applaud": 1,
            "myApplaud":false
          }
          ]
        },
          {
            "userId": "1",
            "userName": "user123",
            "userImg":"/assets/logo.png",
            "date": "2019-5-1",
            "commentContent": "写得真不错",
            "applaud": 5,
            "deriveList": [{
              "userId": "2",
              "userName": "user456",
              "userImg":"/assets/logo.png",
              "date": "2019-5-2",
              "commentContent": "我觉得写的非常好",
              "myApplaud":false,
              "applaud": 3
            }, {
              "userId": "3",
              "userName": "user789",
              "userImg":"/assets/logo.png",
              "date": "2019-5-3",
              "commentContent": "我觉得写的非常好+1",
              "myApplaud":false,
              "applaud": 1
            }
            ]
          }
        ]
      }
    },
    methods: {
      click_repty(e) {
        this.userCommentItem.replyPath=e;
        if(e.length==1){
          // 第一层的回复
          this.userCommentItem.replyUserId=this.items[e[0]].userId;
          this.userCommentItem.replyUserName=this.items[e[0]].userName
        }else {
          // 第二层的回复
          this.userCommentItem.replyUserId=this.items[e[0]].deriveList[e[1]].userId;
          this.userCommentItem.replyUserName=this.items[e[0]].deriveList[e[1]].userName
        }
      },
      commentAdd(userCommentItem){
        userCommentItem.date=new Date();
        userCommentItem.applaud=0;

        if(userCommentItem.replyPath.length==0){
          // 直接文档的评论
          this.items.push(userCommentItem);
        }else if(userCommentItem.replyPath.length==1){
          // 对第一层的评论
          this.items[userCommentItem.replyPath[0]].deriveList.push(userCommentItem)
          // 通过参数可以找到replyPath 可以定位到对谁的评论

        }else if(userCommentItem.replyPath.length==2){
          // 多层评论
          this.items[userCommentItem.replyPath[0]].deriveList.push(userCommentItem)
          // 通过参数可以找到replyPath 可以定位到对谁的评论
        }

        // 此处调用接口将数据存入数据库

        this.userCommentItem={
          "userId": "1",
          "userName": "user123",
          "commentContent": "",
          "docId":123,
          "replyUserId":"",
          "replyUserName":"",
          "rpelyPath":[]
        }

      },
      changeApplaud(e){

        this.userCommentItem.replyPath=e;
        if(e.length==1){
          // 第一层的赞
          this.items[e[0]].myApplaud=!this.items[e[0]].myApplaud;
          this.items[e[0]].applaud=this.items[e[0]].applaud+(this.items[e[0]].myApplaud||-1);

        }else {
          // 第二层的赞
          this.items[e[0]].deriveList[e[1]].myApplaud=!this.items[e[0]].deriveList[e[1]].myApplaud;
          this.items[e[0]].deriveList[e[1]].applaud=this.items[e[0]].deriveList[e[1]].applaud+(this.items[e[0]].deriveList[e[1]].myApplaud||-1)
        }
      }
    }
  }
</script>

<style scoped>

  .comment-items-parent {
    font-size: 12px;
    text-align: left;
    position: absolute;
    display: block;
    width: 95%;
    margin: 0;
  }

  .comment-part {
    font-size: 14px;
    width: 100%;
  }

  .comment-part-title {
    margin-top: 40px;
    padding-bottom: 3px;
  }

  .my-column-title {
    height: 28px;
    line-height: 28px;
  }

  .my-column-title-icon {
    /*background: url("./assets/logo.png") no-repeat;*/
    display: inline-block;
    padding: 7px;
  }

  .my-column-title-text {
    color: #262626;
    font-size: 20px;
    padding-left: 4px;
  }


  ol, ul {
    list-style: none;
  }

  ul li {
    display: block;
  }

  .comment-list-item {
    /*border-bottom: 1px solid #ddd;*/
    margin-left: 50px;
    /*padding: 10px 0 10px;*/
    padding: 0;
  }

  .item-left {
    left: -50px;
    position: absolute;
    top: 17px;
    width: 40px;
  }

  .comment-list-item .item-right{
    border-bottom: 1px solid #ddd;
    padding:14px 0 16px;
  }

  .item-right {
    color: #252525;

  }

  .item-user {
    font-size: 12px;
    line-height: 20px;
    margin: 10px 0;
  }

  .item-user-name {
    font-size: 14px;
  }

  .item-user-time {
    color: #a7a7a7;
  }

  .item-user-right {
    float: right;
  }

  .item-user-like.item-user-unlike {
    color: #787878;
  }

  .item-user-like {
    /*background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAwCAYAAABXAvmHAAAAAXNSR…P4XzYAE+BD5BStpuM85n340Y9mQDOgGdAMaAY0A/8lAz8Bc5fA/BF5WqMAAAAASUVORK5CYII"/assets/logo.png") no-repeat 0;*/
    background-size: 22px;
    color: #f95355;
    cursor: pointer;
    display: inline;
    margin-right: 10px;
    padding-left: 24px;
  }

  .item-user-reply {
    color: #4285f4;
    cursor: pointer;
  }

  .item-text {
    white-space: pre-line;
  }
  .item-text .item-user-reply{
    color: #787878;
    display: inline-block;
  }

  .comment-list-reply {
    background-color: #edf1f4;
    border-radius: 2px;
    margin-top: 15px;
    position: relative;
  }

  .comment-list-ul {
    /*padding:0 15px;*/
  }

  .item-right .comment-list-ul .comment-list-item {
    /*border-bottom: 1px dotted #ddd;*/
    margin-left: 0;
    margin-right: 0;
  }

  .comment-list .comment-list-item {
    /*border-bottom: 1px solid #ddd;*/
    margin-left: 50px;
    padding: 14px 0 16px;
    position: relative;
  }

  comment-list .comment-list-item .item-right{
    padding:0px;
  }

</style>
