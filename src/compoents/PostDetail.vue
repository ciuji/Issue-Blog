<template>
  <div id="pd-window">
    <div id="pd-container">
      <div id="pd-close-btn" @click="close()"></div>
      <div id="pd-content" v-if="true">
        <div id="pd-info">
          <div id="pd-wrap">
            <div id="pd-title">{{post.title}}</div>
            <div id="pd-desc"># {{post.milestone.title}} #</div>
          </div>
        </div>
        <div id="pd-html" v-html="content"></div>
      </div>
    </div>
  </div>
</template>
<script>
import marked from 'marked'

export default {
  props: ['post'],
  data () {
    return {
      comments: []
    }
  },
  computed: {
    content () {
      return this.post && this.post.body && marked(this.post.body)
    }
  },
  methods: {
    close () {
      this.$emit('closePostWindow')
    },
  },
  onCreated () {
    /**Todo:
     * - 加载评论
     */
  }
}
</script>

<style>
@media screen and (max-width: 768px){
  #pd-wrap {
    width: 85%;
    box-sizing: border-box;
  }
  #pd-info {
    width: 100%;
  }
  #pd-content {
    flex-wrap: wrap;
    overflow-y: scroll;
  }
  #pd-html {
    padding: 0px 15px;
    line-height: 24px;
  }
  #pd-html pre {
    overflow-x: scroll;
    width: 100%;
  }
  #pd-container {
    height: 100%;
    width: 100%;
  }
  #pd-list {
    height: 70%;
  }
  #pd-title {
  }
}
@media screen and (min-width: 768px){
  #pd-info {
    height: 100%;
    min-width: 30%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  #pd-container {
    height: 80%;
    width: 80%;
  }
  #pd-list {
    height: 100%;
  }
  #pd-html {
    padding: 40px;
    height: 100%;
    overflow-y: scroll;
  }
  #pd-html pre {
    width: 100%;
  }
}
#pd-window {
  position: fixed;
  /* background-color: rgba(0, 0, 0, 0.5); */
  height: 100%;
  width: 100%;
  top: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}
#pd-container {
  background-color: #fff;
  box-shadow: 0 50px 200px rgba(0, 0, 0, 0.2);
  animation: window-in 0.3s ease-in-out;
  position: relative;
}
#pd-close-btn {
  height: 31px;
  width: 31px;
  position: absolute;
  right: 0;
  top: 0;
  transform: rotate(45deg);
  transition: all ease 0.3s;
  margin: 20px;
  cursor: pointer;
}
#pd-close-btn:hover {
  transform: rotate(45deg) scale(2);
}
#pd-close-btn:before,
#pd-close-btn:after {
  content: ' ';
  display: block;
  background-color: #000;
}
#pd-close-btn:before {
  height: 100%;
  width: 1px;
  transform: translateX(15px);
}
#pd-close-btn:after {
  height: 1px;
  width: 100%;
  transform: translateY(-16px);
}
#pd-content {
  display: flex;
  height: 100%;
}
#pd-info {
  background-color: #eee;
  padding: 20px 15px;
  box-sizing: border-box;
  background-image: url("http://img.zcool.cn/community/012cad59572a46a8012193a3c3048e.jpg@900w_1l_2o_100sh.jpg");
  background-size: cover;
}
#pd-title {
  font-size: 26px;
  margin-bottom: 10px;
}
#pd-list {
  width: 100%;
  overflow-y: scroll;
}
#pd-wrap {
  background-color: rgba(255, 255, 255, 0.8);
  padding: 20px;
}
#pd-html {
  width: 100%;
  box-sizing: border-box;
  color: #444;
}
#pd-html img {
  width: 100%;
}
#pd-html blockquote {
  border-left: 5px solid #eee;
  -webkit-margin-start: 0;
  padding-left: 10px;
}
#pd-html a {
  color: #67aeeb;
}

#pd-html pre {
  background-color: #eee;
  padding: 0px 5px;
  margin: 0 5px;
  border-radius: 5px;
}
#pd-html pre code {
  color: #67aeeb;
  margin: 0;
  padding: 0;
}
#pd-html h1:before,
#pd-html h2:before {
  content: '#';
  margin-right: 5px;
}
#pd-html h1,
#pd-html h2 {
  font-weight: normal;
}
#pd-html ol {
  -webkit-padding-start: 20px;
}
@keyframes window-in {
  from {
    transform: translateY(-1000px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}
</style>