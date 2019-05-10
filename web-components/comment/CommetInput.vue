<template>
  <div class="comment-part">
    <div class="comment-part-title">
      <div class="my-column-title"><span class="my-column-title-icon"></span><span
        class="my-column-title-text weight-bold">参与评论</span></div>
    </div>
    <div class="comment-input-content">
      <div class="comment-input-wrapper">
          <textarea id="js_comment_input" class="comment-input" @input="descArea" v-model="userCommentItem.commentContent"
                    placeholder="你怎么看...">

          </textarea>
      </div>
      <div class="comment-control" style="height: 30px;">
        <a class="comment-control-user">
        <span class="user-avatar" style=""><img src="/assets/logo.png"/></span>{{userCommentItem.userName}}</a>
        <span class="comment-control-user-reply" v-if="userCommentItem.replyUserId>0">
          回复: {{userCommentItem.replyUserName}}
        </span>
        <span
        class="comment-control-submit" @click="commit">
          <span>提交评论</span>
        </span>
        <span class="length-tip">{{wordLengths}}/1000</span>
      </div>
    </div>
    <p class="comment-input-warn">请回复有价值的信息，无意义的评论将很快被删除，账号将被禁止发言。</p>
  </div>
</template>

<script>
    export default {
      name: "CommetInput",
      props:['userCommentItem'],
      data(){
        return {
          wordLengths:0,
          wordMax:1000
        }
      },
      methods:{
          commit(){
            this.$emit("commentAdd",this.userCommentItem);
          },
        descArea(){
          this.wordLengths = this.userCommentItem.commentContent.length;
          if(this.wordLengths>this.wordMax){
            console.log("超出了限制");
            this.userCommentItem.commentContent=this.userCommentItem.commentContent.substr(0,this.wordMax);
          }
        }
      }
    }
</script>

<style scoped>

  textarea{
    outline: none;
  }

  .my-column-title-text {
    color: #262626;
    font-size: 20px;
    padding-left: 4px;
  }

  .comment-part-title {
    margin-top: 40px;
    padding-bottom: 3px;
  }

  .comment-input-content{
    text-align: left;
    background: rgba(245,247,249,.8);
    border: 1px solid #ddd;
    border-radius: 2px;
  }
  .comment-input-wrapper{
    display: flex;
  }
  .comment-input-content .comment-input-wrapper .comment-input{
    border: 0;
    color: #333;
    flex: 1;
    font-size: 14px;
    height: 110px;
    padding: 10px;
    resize: none;
  }
  .comment-input-content .comment-control{
    /*height: 50px;*/
    line-height: 30px;
    padding: 10px;
  }
  .comment-input-content .comment-control .comment-control-user{
    color: #4285f4;
    float: left;
    height: 30px;
    margin-right: 30px;
    padding-left: 40px;
    position: relative;
  }
  .comment-input-content .comment-controller-user .user-avatar{
    background: no-repeat 50% #787878;
    background-size: cover;
    border-radius: 50%;
    height: 30px;
    left: 0;
    position: absolute;
    top: 0;
    width: 30px;
  }
  .comment-input-content .comment-control-submit{
    -moz-user-select: none;
    -ms-user-select: none;
    -webkit-user-select: none;
    background-color: #4285f4;
    border-radius: 1px;
    color: #fff;
    cursor: pointer;
    float: right;
    height: 30px;
    padding: 0 12px;
    position: relative;
    user-select: none;
  }
  .comment-input-content .length-tip{
    color: #787878;
    float: right;
    font-size: 14px;
    padding-right: 10px;
  }
  .comment-control-user-reply{
    background-color: #e1e9f6;
    border-radius: 2px;
    color: #4285f4;
    float: left;
    height: 30px;
    padding: 0 60px 0 10px;
    position: relative;
    display: block;
  }
</style>
