# 流程

## 启动流程
> 通过cobra构建init、run、upgrade命令
>
### init
在init中配置系统参数，涉及db、cache、storage、国际化进行初始化，这一过程是启动一个gin web服务在完成配置信息后退出。
### upgrade
获取init中配置的信息；检查是否需要升级(主要是数据库约束)，如果需要升级则正常升级
### run
核心服务启动，获取配置参数、初始化db、cache等。
* 启动前每个service将自己所需要的repo注册到自己内部；
* 每个controller将自己需要的service注册到自己内部
* 注册基本路由/静态资源路由

## 组件
* gin
* xorm
* cobra
* validator
* mysql
* i18n

## 插件
暂未体验

## 二次开发规范
* 每一层需要依赖的底层服务都需要手动注册到需要的层级中
* handler包下封装有数据校验、统一返回等
* controller层接口的校验统一封装BindAndCheck进行校验，这个BindAndCheck主要是使用validator组件进行约束性校验。
* repo层通过xorm进行持久层维护

## 优点
* 简洁明了
* 短小精悍
* 规范完善
* 文档齐全

## 缺点
* xorm框架硬编码的地方较多
* 需要手动注册依赖的底层服务,项目规模大的时候容易混乱
