<template>
  <div id="app">
    <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
    <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
  </div>
</template>

<script>
  import StyleEditor from './components/StyleEditor'
  import ResumeEditor from './components/ResumeEditor'
  import './assets/reset.css'

  export default {
    name: 'app',
    components: {
      StyleEditor,
      ResumeEditor
    },
    data() {
      return {
        interval:2,
        currentStyle: '',
        enableHtml: false,
        fullStyle: [
          `/*
* Inspired by http://strml.net/
* 大家好，我是余俊瑜，我的花名是蟹老板
* 二月了，好多公司都在招聘，你是不是也在准备简历呀。
* 说做就做，我将用代码来写一份会动的简历！
*/

/* 首先给所有元素加上过渡效果 */
* {
  transition: all .3s;
}
/* 白色背景太单调了，我们来点背景 */
html {
  color: rgb(222,222,222); background: rgb(0,43,54);
}
/* 文字离边框太近了 */
.styleEditor {
  padding: .5em;
  border: 1px solid;
  margin: .5em;
  overflow: auto;
  width: 45vw; height: 90vh;
}
/* 代码高亮 */
.token.selector{ color: rgb(133,153,0); }
.token.property{ color: rgb(187,137,0); }
.token.punctuation{ color: yellow; }
.token.function{ color: rgb(42,161,152); }

/* 加点 3D 效果呗 */
html{
  perspective: 1000px;
}
.styleEditor {
  position: fixed; left: 0; top: 0;
  -webkit-transition: none;
  transition: none;
  -webkit-transform: rotateY(10deg) translateZ(-100px) ;
          transform: rotateY(10deg) translateZ(-100px) ;
}

/* 接下来我给自己准备一个编辑器 */
.resumeEditor{
  position: fixed; right: 0; top: 0;
  padding: .5em;  margin: .5em;
  width: 48vw; height: 90vh;
  border: 1px solid;
  background: white; color: #222;
  overflow: auto;
}
/* 好了，我开始写简历了 */


`,
          `
/* 这个简历好像差点什么
 * 对了，这是 Markdown 格式的，我需要变成对 HR 更友好的格式
 * 简单，用开源工具翻译成 HTML 就行了
 */
`
          ,
          `
/* 再对 HTML 加点样式 */
.resumeEditor{
  padding: 2em;
}
.resumeEditor h2{
  display: inline-block;
  border-bottom: 1px solid;
  margin: 1em 0 .5em;
}
.resumeEditor ul,.resumeEditor ol{
  list-style: none;
}
.resumeEditor ul> li::before{
  content: '•';
  margin-right: .5em;
}
.resumeEditor ol {
  counter-reset: section;
}
.resumeEditor ol li::before {
  counter-increment: section;
  content: counters(section, ".") " ";
  margin-right: .5em;
}
.resumeEditor blockquote {
  margin: 1em;
  padding: .5em;
  background: #ddd;
}
`],
        currentMarkdown: '',
        fullMarkdown: `余俊瑜
----

期望岗位：计算机视觉算法工程师

岗位类别：产品研发

邮箱：im_yujunyu@163.com
电话：177888595485
地址：浙江省杭州市


教育背景
----
2021.09-2024.06——金华职业技术学院——人工智能技术应用
* 核心课程：人工智能数学基础、计算机视觉应用、机器学习、深度学习、人工智能SDK集成应用
* 在校期间智育得分连续三年专业排名第一 ，GPA3.82/4，荣获国家励志奖学金2次

2024.09-至今——湖州学院——计算机科学与技术


荣誉证书
----
* 第十二届“中国软件杯”大学生软件设计大赛全国总决赛一等奖（国家级、破校记录、1/66）
* 一带一路暨金砖国家技能发展与技术创新大赛视频感知技术赛项国内赛一等奖（国家级、2/37）
* 第十四届蓝桥杯全国软件和信息技术专业人才大赛浙江赛区Python程序设计大学C组三等奖（省级）
* 基于ResNet18的垃圾分类识别与预测系统V1.0（第一作者、单独开发）
* 图片采集大师软件V1.0（第一作者、单独开发）
* 图书管理系统V1.0
* NCRE三级网络技术、NCRE二级Python语言程序设计、CET4、浙江省计算机二级MS

实践经历
----
2022.09-至今——软件开发工作室——人工智能方向核心成员
* 大一加入软件开发工作室，自学人工智能技术，并创造性地制定了学习路线，已供3届学生使用
* 大二参与项目开发、竞赛，累计完成50余个校企合作项目，具有丰富的项目开发经验


2023.05-2023.06——OpenMMLab实战营（上海人工智能实验室OpenMMLab主办）——助教
*	与985、211本硕学生同期应聘，成功入选助教名单，表现突出被评为优秀助教（3/16）
*	同步学习MMDetection、MMSegmentation等课程，完成5个算法库的实战项目


项目经历
----
* 2023.03-2023.04——体感互动-基于MediaPipe和LSTM的手势估计——项目负责人
* 2022.08-2022.09——基于ResNet18的垃圾分类识别与预测系统——项目负责人
* 2022.06-2022.07——基于YOLOv5的老人跌倒检测项目——核心开发者


专业技能
----
* 掌握深度学习基础知识，熟练使用Pytorch、TensorFlow深度学习框架进行开发
* 掌握计算机视觉和图像处理基本算法，熟练使用OpenCV进行图像处理和识别
* 掌握机器学习基础知识，了解分类、回归等各大算法，清楚算法核心以及可解决任务类型
* 熟悉人工智能开发的整体流程，了解图像分类、目标检测、语义分割等主流网络
* 熟悉OpenMMLab计算机视觉算法开源体系，具备该算法库的实际项目应用和开发经验
* 熟悉Python的Flask、Django等Web开发框架，了解HTML/CSS等前端技术
* 精通Python开发语言，遵循PEP8规范，有良好的代码习惯和代码风格

自我评价
----
* 热爱人工智能领域，喜欢钻研技术，具备较强的自主学习和解决问题的能力，具有创新思维和创造力
* 注重细节，能够保持高度的专注和精确性，抗压能力强，具有良好的团队合作和沟通协作能力
* 秉持低调做人、高调做事的行为准则，具有良好的职业道德

个人账号
----
GitHub： [点我点我，这是我的GitHub账号！](https://github.com/CrabBoss-lab)

[CSDN](https://www.cnblogs.com/xielaoban/)


> 如果你喜欢这个效果，Fork [这个项目](https://github.com/jirengu-inc/animating-resume)，打造你自己的简历！

`
      }
    },
    created() {
      this.makeResume()
    },

    methods: {
      makeResume: async function () {
        await this.progressivelyShowStyle(0)
        await this.progressivelyShowResume()
        await this.progressivelyShowStyle(1)
        await this.showHtml()
        await this.progressivelyShowStyle(2)
      },
      showHtml: function () {
        return new Promise((resolve, reject) => {
          this.enableHtml = true
          resolve()
        })
      },
      progressivelyShowStyle(n) {
        return new Promise((resolve, reject) => {
          let interval = this.interval
          let showStyle = (async function () {
            let style = this.fullStyle[n]
            if (!style) { return }
            // 计算前 n 个 style 的字符总数
            let length = this.fullStyle.filter((_, index) => index <= n).map((item) => item.length).reduce((p, c) => p + c, 0)
            let prefixLength = length - style.length
            if (this.currentStyle.length < length) {
              let l = this.currentStyle.length - prefixLength
              let char = style.substring(l, l + 1) || ' '
              this.currentStyle += char
              if (style.substring(l - 1, l) === '\n' && this.$refs.styleEditor) {
                this.$nextTick(() => {
                  this.$refs.styleEditor.goBottom()
                })
              }
              setTimeout(showStyle, interval)
            } else {
              resolve()
            }
          }).bind(this)
          showStyle()
        })
      },
      progressivelyShowResume() {
        return new Promise((resolve, reject) => {
          let length = this.fullMarkdown.length
          let interval = this.interval
          let showResume = () => {
            if (this.currentMarkdown.length < length) {
              this.currentMarkdown = this.fullMarkdown.substring(0, this.currentMarkdown.length + 1)
              let lastChar = this.currentMarkdown[this.currentMarkdown.length - 1]
              let prevChar = this.currentMarkdown[this.currentMarkdown.length - 2]
              if (prevChar === '\n' && this.$refs.resumeEditor) {
                this.$nextTick(() => this.$refs.resumeEditor.goBottom())
              }
              setTimeout(showResume, interval)
            } else {
              resolve()
            }
          }
          showResume()
        })
      }
    }
  }

</script>

<style scoped>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  html {
    min-height: 100vh;
  }
  *{
    box-sizing: border-box;
  }
</style>
