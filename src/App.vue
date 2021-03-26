<template>
  <div id="app">
    <div id="content">
      <StyleEditor ref="styleEditor" :code="currentStyle"></StyleEditor>
      <ResumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></ResumeEditor>
    </div>
    <div id="foot">
      <ThankEditor ref="thankEditor" :markdown="currentThankMarkdown" :enableHtml="enableHtml"></ThankEditor>
    </div>
  </div>
</template>

<script>
  import StyleEditor from './components/StyleEditor'
  import ResumeEditor from './components/ResumeEditor'
  import ThankEditor from './components/ThankEditor'
  import './assets/reset.css'

  export default {
    name: 'app',
    components: {
      StyleEditor,
      ResumeEditor,
      ThankEditor
    },
    data() {
      return {
        interval: 5,
        currentStyle: '',
        enableHtml: false,
        fullStyle: [
          `/*
* 大家好，我是李恒
* 我来写一份动态简历！
*/

/* 首先给所有元素加上过渡效果 */
* {
  transition: all .1s;
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
.token.selector{ color: rgb(130,150,0); }
.token.property{ color: rgb(190,140,0); }
.token.punctuation{ color: yellow; }
.token.function{ color: rgb(40,160,150); }

/* 加3D效果 */
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
/* 开始写简历 */
`, `
/*将Markdown格式翻译成HTML
 *再对HTML加点样式
*/
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
        currentThankMarkdown: '',
        fullMarkdown: `李恒
----

JAVA高级开发工程师 。

技能
----
熟悉 Spring、SpringMVC、MyBatis, hibernate,Spring boot 框架的使用。
熟练使用 SVN、Git ,Maven等常用开发管理工具。
熟练使用 Eclipse、Myeclipse、IntellijIDEA，VS2018 等开发工具。
熟悉Mysql、Oracle 等主流数据库和 redis 缓存数据库。
熟悉使用操作 linux 操作系统及常用命令；
熟练使用 docker 搭建开发环境；
熟悉基于ActiveMQ 的消息分发与接收。
熟悉 Shiro 技术。
熟悉RestFul 风格接口设计。
熟悉 Zookeeper、Dubbo 分布式服务。
熟悉 Quartz 作业调度框架的使用。
熟悉C#，有 WPF 的开发经验。
熟练使用第三方工具如： 微信小程序后台支付企业付款开发， 短信平台等；
了解 WebService , struts2技术
能够独立完成项目；
具有良好的编程风格；


工作经历
----

工作名称：郑州飞道科技有限公司
职位名称：Java 开发工程师/C#开发工程师
工作时间：2018.11-2019.06
工作职责：
1. 参与项目需求分析,概要设计和详细设计；
2. 与项目经理和小组成员沟通协商解决分析开发过程中可能出现的问题；
3. 对自己的任务模块进行代码设计并进行基础测试；
工作名称：河南万里科技有限公司
职位名称：java 开发工程师
工作时间：2016/8 -- 2018/10
工作职责：
1. 负责服务端程序的设计、开发、维护工作
2. 负责对管理系统的升级，业务的分析和整理
3. 技术文档编写
项目经验
项目名称：真维斯休闲娱乐项目
项目角色：java工程师
软件环境：SpringMVC + springboot + mybatis + Maven + redis + MyBatis
项目描述：电商类网站，该项目是针对休闲娱乐商铺的一个开放入住平台，项目分为商户端，平台端，用户端，类型分
为休闲娱乐和商务服务，商家入驻平台，内容包括美发，洗浴，运动健身，学习培训等，用户可购买其服务项目，并对
其评论，分享等。
项目职责：
1， 项目采用cookie加redis的方案解决单点登陆问题。用户只需登陆一次，可以访问旗下所有的项目，其他项目
模块通过cookie+redis获得用户信息，避免用户重复登陆，用户访问其他模块时查询cookie里面对应的KEY值
去redis中查询用户信息，如果不存在或者过期将会让用户重新登陆；
2， 商户商务服务端人员技师管理和班次管理模块，商家可以通过该模块添加技师相关信息和班次信息，技师也可
以根据实际情况预订班次；
3， 休闲娱乐平台端角色权限管理，用户角色管理和商品管理，用户匿名浏览商品时，可以将商品加入购物车，此
时的商品信息保存在cookie中，结算时需登陆方可结算，登陆后将cookie中的商品信息拿出同步到该登陆账
户下的购物车。并已存在的商品数量价格相加。选中商品后可以添加物流地址信息并提交订单。使用quartz定
时任务框架检测未付款订单，超时两天自动关闭订单，释放库存。
乐购网
项目角色：java工程师
软件环境：Spring+SpringMVC+mybatis+Shiro
项目描述：适应现金网络发展的需求，公司力求打造一个以手机，电视等电子产品为主的综合性电商超市，乐购电商网
站专注于电子产品，家用电器市场，持续深耕，为客户提供方便快捷的购物体验。该系统包含门户系统，搜索系统，用
户系统和后台系统。
项目职责：
1. 主要负责基础设置模块和商品展示的生成。
2. 商品类别的管理以及商品的上下架。
3. 用户注册、登录功能的实现。
4. 用户搜索商品，查看商品。
5. 下单功能的实现。
项目名称：OA办公
项目角色：java工程师
项目描述：利用网络通信技术实现管理自动化和办公事务处理自动化，以提供现代化的日常办公条件，提高办公效率和
管理水平，旨在为企业、为各个部门提供员工的方便管理。该系统主要针对不同领导层拥有不同的权限级别，管理不同
自我评价
部门级别的 员工，比如员工的绩效考核，请假报销审批。该项目主要有员工管理、人员绩 效信息、员工请假、报
销信息统计等模块。
项目职责：
主要参与系统部分模块化的需求分析与详细分析，批量上传人员列表，二级菜单，人员权限分配，接口的设计
和实现。
1. 系统后台主要采用ssm框架，MySQL数据库；
2. 前台页面采用layui，采用页面动态化；
3. sql优化和tomcat优化作为系统的主要优化；
4. 采用poi技术实现Excel文件批量上传和下载；
项目名：思方 ERP 管理系统
开发环境：VS2018+WPF+MySQL+GIT
项目描述：共分为货品，财务，销售，工程，生产，报价，设备，品质等模块。对工单、配件、财务等相关数据进行
全方位管理，规范化、系统化。家电售后服务的所有相关人员。工单快速下单、及时跟进，配件库存实时管理，保障
售后服务快速及时完成。
责任描述：
1. 负责销售模块，报价模块，财务模块及生产模块的代码开发及测试。
2. 对接相应方案人员，进行需求梳理。
3. 对新员工的教导培训及总结。 

自我评价
----

具有独立开发能力，熟练的专业技能、较强的动手能力，有良好的交际能力和统筹协作能力。能及时反馈并解
决问题，对工作积极主动、认真负责、善于创新、求知欲强，有较强的学习及适应能力。富有工作激情，乐业敬业，
具有良好的组织能力，团队协作精神。

`
      }
    },
    created() {
      this.makeResume()
    },

    methods: {
      makeResume: async function () {
        await this.progressivelyShowStyle(0);
        await this.progressivelyShowResume();
        await this.progressivelyShowStyle(1);
        await this.showHtml();
        await this.progressivelyShowStyle(2);
        await this.progressivelyShowThanks();
        await this.progressivelyShowStyle(3)
      },
      showHtml() {
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
            if (!style) {
              return
            }
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
      },
      progressivelyShowThanks() {
        return new Promise((resolve, reject) => {
          let length = this.thanksMarkdown.length
          let interval = this.interval
          let showThanks = () => {
            if (this.currentThankMarkdown.length < length) {
              this.currentThankMarkdown = this.thanksMarkdown.substring(0, this.currentThankMarkdown.length + 1)
              let lastChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 1]
              let prevChar = this.currentThankMarkdown[this.currentThankMarkdown.length - 2]
              if (prevChar === '\n' && this.$refs.thankEditor) {
                this.$nextTick(() => this.$refs.thankEditor.goBottom())
              }
              setTimeout(showThanks, interval)
            } else {
              resolve()
            }
          }
          showThanks()
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

  * {
    box-sizing: border-box;
  }
</style>
