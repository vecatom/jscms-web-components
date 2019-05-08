<template>
  <div id="repty-items">
    <div class="comment-part">
      <div class="comment-part-title">
        <div class="my-column-title"><span class="my-column-title-icon"></span><span
          class="my-column-title-text weight-bold">参与评论</span></div>
      </div>
      <div class="comment-input-content">
        <div class="comment-input-wrapper">
          <textarea id="js_comment_input" class="comment-input"
                                                     placeholder="你怎么看...">

          </textarea>
        </div>
        <div class="comment-control"><a class="comment-control-user">
          <span class="user-avatar" style="background-image: url(&quot;//sta.36krcnd.com/36krx2018-front/static/default_avatar.e19c4635.png&quot;);"></span>新用户11493980</a><span
          class="comment-control-submit">
          <span>提交评论</span>
        </span>
          <span class="length-tip">0/1000</span>
        </div>
      </div>
      <p class="comment-input-warn">请文明发言，否则，账号将被禁止发言。</p>
    </div>
    <div class="comment-part">
      <div class="comment-part-title">
        <div class="my-column-title">
          <span class="my-column-title-icon"></span>
          <span class="my-column-title-text weight-bold">评论区</span>
        </div>
      </div>
      <ul class="comment-list">
        <li class="comment-list-item">
          <div class="item-left">
				<span class="item-avatar"
              style="background-image:s ;"
        >

				</span>
          </div>
          <div class="item-right">
            <div class="item-user">
              <span class="item-user-name">新用户18966820</span>
              <span class="item-user-time"> · 2019-05-06</span>
              <div class="item-user-right">
                <span class="item-user-like item-user-unlike"> 赞 6</span>
                <a class="item-user-reply">回复</a>
              </div>
            </div>
            <p class="item-text">真是非常好</p>
            <div class="comment-list comment-list-reply">
              <ul class="comment-list-ul">
                <li class="comment-list-item">
                  <div class="item-right">
                    <div class="item-user">
                      <span class="item-user-name">新用户11493980</span>
                      <span class="item-user-time"> · 昨天</span>
                      <div class="item-user-right">
                        <span class="item-user-like item-user-like"> 赞 6</span>
                        <a class="item-user-reply">回复</a>
                      </div>
                    </div>
                    <p class="item-text">非常好</p>
                  </div>
                </li>
              </ul>
            </div>
            <div class="comment-list comment-list-reply">
              <ul class="comment-list-ul">
                <li class="comment-list-item">
                  <div class="item-right">
                    <div class="item-user">
                      <span class="item-user-name">新用户11493980</span>
                      <span class="item-user-time"> · 昨天</span>
                      <div class="item-user-right">
                        <span class="item-user-like item-user-like"> 赞 6</span>
                        <a class="item-user-reply">回复</a>
                      </div>
                    </div>
                    <p class="item-text">非常好12321</p>
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
  export default {
    name: "ReptyItems"
  }
</script>

<style scoped>

  #repty-items {
    font-size: 12px;
    text-align: left;
    position: absolute;
    display: block;
    width: 95%;
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
    background: url(/assets/logo.png) no-repeat;
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
    border-bottom: 1px solid #ddd;
    margin-left: 50px;
    padding: 14px 0 16px;
  }

  .comment-list comment-list-item .item-left {
    left: -50px;
    position: absolute;
    top: 17px;
    width: 40px;
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

  .item-user-unlike {
    color: #787878;
  }

  .item-user-like {
    background: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAwCAYAAABXAvmHAAAAAXNSR…P4XzYAE+BD5BStpuM85n340Y9mQDOgGdAMaAY0A/8lAz8Bc5fA/BF5WqMAAAAASUVORK5CYII=) no-repeat 0;
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

  .comment-list-reply {
    background-color: #edf1f4;
    border-radius: 2px;
    margin-top: 15px;
    position: relative;
  }

  .comment-list-ul {
    /*padding:0 15px;*/
  }

  .comment-list-ul .comment-list-item {
    border-bottom: 1px dotted #ddd;
    margin-left: 0;
    margin-right: 0;
  }

  .comment-list .comment-list-item {
    border-bottom: 1px solid #ddd;
    margin-left: 50px;
    padding: 14px 0 16px;
    position: relative;
  }


  .comment-input-content{
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
  .comment-input-comtent .comment-controle-user{
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

</style>
