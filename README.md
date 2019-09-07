#  小蜜蜂工作室
该项目用于管理工作室内部的文章





# 新技能
## task
1.redisson client
```
RedisClient.init((RedissonClient)webApplicationContext.getBean(RedissonClient.class));

public static void init(RedissonClient redissonClient) { RedisClient.redissonClient = redissonClient; }
```
2.自定义注解@MyBatisRepository
```
@MyBatisRepository
public interface MchntExtCfgMapper {}
```
```
<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
    <property name="basePackage" value="com.chinanums.yinlian.task.mapper" />
    <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory" />
    <property name="annotationClass" value="com.buybal.yinlian.module.annotation.MyBatisRepository" />
</bean>
```
3.mybatis generator

4.task 模块主要功能
- 日切
- 平台分润开始
- 分润统计
- 统计入网的审核通过的商户数
- 同步支行（T_PLAT_ORG_INF），同步商户
- T1结算单
- T1代付分润

5.与wlk交互的接口有
- juhe-qp-business/addOrg.html（网联客 上送机构接口）
- juhe-qp-business/registMerNew.html（网联客 上送商户接口）
- juhe-qp-business/queryOrg.html（网联客 上送机构查询接口）
- juhe-qp-business/queryMerchant.html（网联客 上送商户查询接口）

6.与wlk信息同步的方式
> http接口方式

7.内部封装的包
> module-2.0.0-SNAPSHOT.jar

8.采用到的技术
- spring 定时任务 scheduled
- mybatis generator
- redis 哨兵 redisson client
- 自定义注解@MyBatisRepository
- oracle/druid/mapper xml/mapper/service/spring scheduled

## buybal-api
1.采用到的技术
- dubbo
- redisson client
- oracle/druid/mapper xml/mapper/service/controller
- task（scheduled）

2.task模块主要功能
- 查询本天3分钟前未支付，发起关闭订单操作。
- 查询订单表中30分钟内（1分钟前）未支付的订单，发起查询操作。

