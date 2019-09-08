# 项目开发规范（Java）
> @Author：ZhaoJian，@Date 2019-09-08

## 项目包结构规范
基础包       |模块名|子模块名                |子模块名       |子模块名
-----------:|:-----|:----------------------|:-------------|
com.Project.|common|constant               |              |常量包
            |      |util                   |              |工具包
            |config|properties             |              |properties初始化包
            |      |RestTemplateConfig.java|              |RestTemplate配置类
            |      |SwaggerConfig.java     |              |Swagger配置类
            |      |WebMvcConfig.java      |              |Mvc配置类
            |enums |ValidationEnum.java    |              |校验枚举类
            |error |exception              |              |异常处理包
            |      |handler                |              |异常handler包
            |interceptor|LoginInterceptor.java|           |拦截器
            |mvc   |common                 |              |mvc公共包
            |      |app                    |              |App端模块         
            |      |                       |controller    |         
            |      |                       |entity        |
            |      |                       |mapper        |
            |      |                       |service       |
            |      |sys                    |              |管理端模块
            |      |                       |controller    |         
            |      |                       |entity        |
            |      |                       |mapper        |
            |      |                       |service       |
            |ProjectApplication.java|      |              |spring boot 启动类

                  

## endpoint 规范



## 命名规范

### 类命名规范


### 方法命名规范

### 包命名规范

##  swagger api规范

##  日志规范

##  实体类规范

##  注释规范

##  类内部规范

##  


