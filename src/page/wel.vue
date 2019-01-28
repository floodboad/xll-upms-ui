<!--
  -    Copyright (c) 2018-2025, lengleng All rights reserved.
  -
  - Redistribution and use in source and binary forms, with or without
  - modification, are permitted provided that the following conditions are met:
  -
  - Redistributions of source code must retain the above copyright notice,
  - this list of conditions and the following disclaimer.
  - Redistributions in binary form must reproduce the above copyright
  - notice, this list of conditions and the following disclaimer in the
  - documentation and/or other materials provided with the distribution.
  - Neither the name of the pig4cloud.com developer nor the names of its
  - contributors may be used to endorse or promote products derived from
  - this software without specific prior written permission.
  - Author: lengleng (wangiegie@gmail.com)
  -->

<template>
  <div class="pull-chheight wel-contailer">
    <div class="banner-text">
      <h2>XLL Microservice Architecture</h2>
      <span align="center">
       <img src="https://img.shields.io/badge/Avue-1.5.4.RC1-green.svg" alt="Build Status">
        <img src="https://img.shields.io/badge/Spring%20Cloud-EdgwareSR4-orange.svg" alt="Coverage Status">
        <img src="https://img.shields.io/badge/Spring%20Boot-1.5.15-blue.svg" alt="Downloads">
        <img src="https://img.shields.io/npm/v/npm.svg" alt="Version">
        <img src="https://img.shields.io/npm/l/vue.svg" alt="License">
      </span>
      <br/>
      <span>
          <el-collapse v-model="activeNames">
            <el-collapse-item title="Spring 学习官网" name="1">
              <div>
                <a href="https://spring.io/" target="_blank">
                  <p>Spring</p>
                </a>
              </div>
              <div>
                <a href="https://www.springall.com.cn/" target="_blank">
                  <P>Spring中文网</P>
                </a>
              </div>
              <div>
                <a href="https://spring.io/projects/spring-boot/" target="_blank">
                  <p>Spring Boot</p>
                </a>
              </div>
              <div>
                <a href="http://springboot.fun/" target="_blank">
                  <p>Spring Boot中文网</p>
                </a>
              </div>
              <div>
                <a href="https://spring.io/projects/spring-cloud" target="_blank">
                  <p>Spring Cloud</p>
                </a>
              </div>
              <div>
                <a href="https://springcloud.cc/" target="_blank">
                  <p>Spring Cloud中文网</p>
                </a>
              </div>
            </el-collapse-item>
            <el-collapse-item title="参考资料" name="2">
              <div>
                <a href="https://mp.baomidou.com/guide/" target="_blank">
                  <p>MyBatis Plus</p>
                </a>
              </div>
              <div>
                <a href="http://www.mybatis.org/mybatis-3/zh/index.html" target="_blank">
                  <p>MyBatis</p>
                </a>
              </div>
              <div>
                <a href="https://martinfowler.com/articles/microservices.html" target="_blank">
                  <p>Martin Fowler blog</p>
                </a>
              </div>
              <div>
                <a href="https://docs.oracle.com/javase/8/docs/api/index.html" target="_blank">
                  <p>Java SE 1.8文档</p>
                </a>
              </div>
            </el-collapse-item>
            <el-collapse-item title="其他文档" name="3">
              <div>
                <a href="http://www.redis.net.cn/" target="_blank">
                  <p>Redis中文网</p>
                </a>
              </div>
              <div>
                <a href="https://www.elastic.co/guide/cn/elasticsearch/guide/current/index.html" target="_blank">
                  <p>Elasticsearch 2.x文档</p>
                </a>
              </div>
              <div>
                <a href="https://zookeeper.apache.org/doc/r3.4.13/" target="_blank">
                  <p>Zookeeper官方文档</p>
                </a>
              </div>
              <div>
                <a href="http://www.rabbitmq.com/documentation.html" target="_blank">
                  <p>RabbitMQ官方文档</p>
                </a>
              </div>
              <div>
                <a href="https://www.jianshu.com/p/218913cccc95" target="_blank">
                  <p>Fdfs学习博客</p>
                </a>
              </div>
            </el-collapse-item>
            <el-collapse-item title="前端框架" name="4">
              <div>
                <a href="https://cn.vuejs.org/" target="_blank">
                  <p>Vue学习官网</p>
                </a>
              </div>
              <div>
                <a href="http://www.runoob.com/js/js-tutorial.html" target="_blank">
                  <p>JavaScript学习网站</p>
                </a>
              </div>
              <div>
                <a href="http://www.runoob.com/nodejs/nodejs-tutorial.html" target="_blank">
                  <p>Node.js学习网站</p>
                </a>
              </div>
            </el-collapse-item>
          </el-collapse>
        </span>
      <span>
        </span><br>
      <span :class="['actor',{typeing:isText}]">{{text}}</span>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  name: 'wel',
  data() {
    return {
      activeNames: ['1', '2', '3', '4'],
      DATA: [],
      text: '',
      actor: '',
      count: 0,
      isText: false
    }
  },
  computed: {
    ...mapGetters(['website'])
  },
  created() {
    this.DATA = this.website.wel.list
    this.actor = this.DATA[this.count] || ''
    setTimeout(() => {
      this.isText = true
      this.setData()
    }, 2000)
  },
  methods: {
    getData() {
      if (this.count < this.DATA.length - 1) {
        this.count++
      } else {
        this.count = 0
      }
      this.isText = true
      this.actor = this.DATA[this.count]
    },
    setData() {
      let num = 0
      let count = 0
      let active = false
      const timeoutstart = 5000
      const timeoutend = 1000
      const timespeed = 10
      setInterval(() => {
        if (this.isText) {
          if (count === this.actor.length) {
            active = true
          } else {
            active = false
          }
          if (active) {
            num--
            this.text = this.actor.substr(0, num)
            if (num === 0) {
              this.isText = false
              setTimeout(() => {
                count = 0
                this.getData()
              }, timeoutend)
            }
          } else {
            num++
            this.text = this.actor.substr(0, num)
            if (num === this.actor.length) {
              this.isText = false
              setTimeout(() => {
                this.isText = true
                count = this.actor.length
              }, timeoutstart)
            }
          }
        }
      }, timespeed)
    }
  }
}
</script>

<style scoped="scoped" lang="scss">
.wel-contailer {
  position: relative;
}
.banner-text {
  position: relative;
  padding: 0 20px;
  font-size: 20px;
  text-align: center;
  color: #333;
}
.banner-img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0.8;
  display: none;
}
.actor {
  height: 250px;
  overflow: hidden;
  font-size: 18px;
  color: #333;
}

.actor:after {
  content: "";
  width: 3px;
  height: 25px;
  vertical-align: -5px;
  margin-left: 5px;
  background-color: #333;
  display: inline-block;
  animation: blink 0.4s infinite alternate;
}

.typeing:after {
  animation: none;
}

@keyframes blink {
  to {
    opacity: 0;
  }
}
</style>
