---
title: 简历
layout: page
description: 个人简历
---
<!--
  这是一个简历页面模板。
  将下方占位内容替换为你自己的真实信息即可。
-->

<style>
  .resume-wrap {
    max-width: 860px;
    margin: 0 auto;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "PingFang SC", "Microsoft YaHei", sans-serif;
    color: #2c3e50;
    line-height: 1.7;
  }
  .resume-header {
    text-align: center;
    padding: 24px 0 8px;
    border-bottom: 2px solid #42b983;
  }
  .resume-header .name {
    font-size: 2rem;
    font-weight: 700;
    letter-spacing: 2px;
    margin: 0;
  }
  .resume-header .job {
    font-size: 1.1rem;
    color: #666;
    margin-top: 4px;
  }
  .resume-avatar {
    width: 120px;
    height: 120px;
    object-fit: cover;
    border-radius: 50%;
    border: 3px solid #fff;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
    margin-bottom: 12px;
  }
  .resume-contact {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 8px 24px;
    margin: 12px 0 0;
    font-size: 0.9rem;
    color: #555;
  }
  .resume-section {
    margin-top: 28px;
  }
  .resume-section h2 {
    font-size: 1.25rem;
    margin: 0 0 12px;
    padding-left: 10px;
    border-left: 4px solid #42b983;
    color: #333;
  }
  .resume-item {
    margin-bottom: 16px;
  }
  .resume-item .head {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    flex-wrap: wrap;
  }
  .resume-item .title {
    font-weight: 600;
    color: #333;
  }
  .resume-item .org {
    color: #42b983;
    font-weight: 600;
  }
  .resume-item .time {
    font-size: 0.85rem;
    color: #999;
  }
  .resume-item .desc {
    margin: 4px 0 0;
    font-size: 0.95rem;
    color: #555;
  }
  .resume-item ul {
    margin: 6px 0 0;
    padding-left: 20px;
    font-size: 0.95rem;
    color: #555;
  }
  .resume-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }
  .resume-tags span {
    background: #f0f7f4;
    color: #2c8a68;
    border: 1px solid #d3e9df;
    border-radius: 14px;
    padding: 2px 12px;
    font-size: 0.88rem;
  }
</style>

<div class="resume-wrap">

<header class="resume-header">
<img class="resume-avatar" src="/resume/照片.jpg" alt="照片">
<h1 class="name">杨明刚</h1>
<div class="job">C++ 软件开发工程师 / 端侧 AI 视觉开发工程师 · 北京市</div>
<div class="resume-contact">
<span>📞 15214423365</span>
<span>✉️ yangminggang1114@163.com</span>
<span>💼 GitHub: https://github.com/NonOmni</span>
<span>🔗 个人博客: https://nonomni.github.io/</span>
</div>
</header>

<section class="resume-section">
<h2>个人简介</h2>
<p class="resume-item desc">
多年 C++ 研发经验，覆盖 Windows 安全与端侧 AI 视觉两大方向。早年在火绒、奇安信从事安全终端研发，熟悉 duilib 界面库、STL/C++11、Windows 消息机制及 WinDbg/spy++ 调试，参与完成病毒库下载提速、问题排查工具等多项功能；目前在荣耀负责 MagicOS 系统级视觉引擎的芯片适配与模型量化，独立完成 20+ AI 模型在多芯片平台的量化部署（GPU/CPU/QNN），熟悉 C++/JNI 开发、TensorRT 模型加速与 Docker 云端测试环境搭建。累计处理 130+ 需求验证与 10+ 缺陷跟踪工单。
</p>
</section>

<section class="resume-section">
<h2>教育经历</h2>
<div class="resume-item">
<div class="head">
<span class="title"><span class="org">哈尔滨师范大学</span> · 电子信息科学与技术（本科）</span>
<span class="time">2017.09 - 2021.06</span>
</div>
<ul>
<li>主修课程：电路分析、数字电路分析、计算机基础、C 语言程序设计、C++ 程序设计、单片机原理、算法与数据结构、通信原理等</li>
</ul>
</div>
</section>

<section class="resume-section">
<h2>工作经历</h2>

<div class="resume-item">
<div class="head">
<span class="title"><span class="org">北京荣耀科技有限公司</span> · 端侧 AI 视觉开发工程师</span>
<span class="time">2025.07 - 至今</span>
</div>
<ul>
<li>负责 MagicOS 系统级视觉引擎的芯片适配、模型量化以及 Native 层开发</li>
</ul>
</div>

<div class="resume-item">
<div class="head">
<span class="title"><span class="org">火绒科技股份有限公司</span> · Windows C/C++ 开发工程师</span>
<span class="time">2024.07 - 2025.06</span>
</div>
<ul>
<li>负责火绒安全软件个人版 5.0 主要功能上层的维护，以及企业版 2.0、1.0 终端的维护与问题排查</li>
<li>参与火绒安全软件个人版 6.0 主要界面的实现，包括主界面、设置界面和基于 duilib VList 的二级虚拟列表实现</li>
<li>主界面中应用商店接口的展示，实现判断已有安装包和是否安装的逻辑，增加应用商店展示隐藏及升级提示功能</li>
<li>天融信企业版本：实现通过 sha2 信息有选择地更新本地病毒库和组件库，以配合系统版本适配</li>
</ul>
</div>

<div class="resume-item">
<div class="head">
<span class="title"><span class="org">奇安信科技股份有限公司</span> · Windows 终端研发工程师</span>
<span class="time">2022.10 - 2024.07</span>
</div>
<ul>
<li>负责天擎安全终端的安装、卸载部分的维护</li>
<li>完成天擎终端病毒库下载提速：线上通过 7zip 打包原有零散病毒库文件，使用 libcurl 通过中心下载用户定制的功能库，在终端安装时解压到原有功能库中，最终提高终端安装效率</li>
<li>服务端配置工具的维护与更新：通过服务端给出的功能开关接口，创建 duilib 为底层的具有界面的工具修改 sqlite 库中对应功能开关，方便同事使用</li>
<li>使用 duilib 库实现一线人员的问题排查工具，获取当前终端的配置信息、功能日志、基本用户属性等，方便一线人员修改中心数据和导出日志</li>
</ul>
</div>
</section>

<section class="resume-section">
<h2>专业技能</h2>
<div class="resume-tags">
<span>C / C++</span>
<span>duilib</span>
<span>STL / C++11</span>
<span>Visual Studio</span>
<span>WinDbg / spy++</span>
<span>Git</span>
<span>jansson / sqlite</span>
<span>C++ / JNI</span>
<span>TensorRT</span>
<span>Docker</span>
</div>
</section>

</div>
