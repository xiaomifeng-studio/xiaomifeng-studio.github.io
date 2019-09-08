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
1. 一个endpoint 尽量只用一种请求方式，并且禁止在方法上编写@RequestMapping；

    注解       |使用场景
    ---------:|:-----
    @PostMapping    | 添加操作、登录、上传文件、h5支付
    @DeleteMapping  | 删除操作
    @PutMapping     | 修改操作
    @GetMapping     | 查询操作

2. 大于等于5个入参必须使用实体，小于5个可以写成实际参数，也可以实体，看情况

3. endpoint 接口尽量采用


## 命名规范

### 1.类命名规范

序号  |    类别 | 规则 | 示例
:----:|:---------------|:---------------|:----
1     |controller 入参类命名规则|模块+Param+List+业务模块+ByColumn  | AppParamListUserByColumn
2     |controller 返回类命名规则|模块+Result+List+业务模块+ByColumn  | AppResultListUserByColumn
3     |controller、service、mapper命名规则|模块+业务模块+Controller、Service、Mapper  | AppUserController、AppUserService、AppUserMapper
4     | 实体类  | 表名驼峰  |  User


### 2.方法命名规范


### 3.包命名规范
除公共包外，所有的

##  swagger api规范
1. 由于不同版本之间存在差异，暂定使用swagger 2.7.0版本；

2. 每一个endpoint 需要都加上如下注解；
    ```
    @ApiResponses({ @ApiResponse(code = 200, message = "SUCCESS 响应报文", response = ResultLogin.class),
         @ApiResponse(code = 500, message = "ERROR 响应报文", response = ApiError.class)
    })
    ```

3. endpoint 参数较少，未采用实体接收，需要在方法上写对应的参数描述；
    ```
    @ApiOperation(value = "登录", notes = "login endpoint", httpMethod = "POST", produces="application/json")
    @ApiImplicitParams({
         @ApiImplicitParam(name = "userName", value = "*帐号", required = true, readOnly=true),
         @ApiImplicitParam(name = "passWord", value = "*密码", required = true, readOnly=true)
    })
    @ApiResponses({ @ApiResponse(code = 200, message = "SUCCESS 响应报文", response = ResultLogin.class),
         @ApiResponse(code = 500, message = "ERROR 响应报文", response = ApiError.class)
    })
    @PostMapping("login")
    public ResponseEntity<ResultLogin> login(String userName, String passWord,  HttpSession session) {
     
    }
    ```
4. endpoint 入参是一个实体，不用在方法上写@ApiImplicitParams，直接在入参实体中编写@ApiModel和@ApiModelProperty即可；
    ```
    @ApiModel
    @Data
    public class ParamLogin {
    
        @ApiModelProperty(value = "账号", required = false)
        String username;
    
    }
    ```
5. 同理endpoint 入参实体，返回实体也必须在实体中编写@ApiModel和@ApiModelProperty，便于前端对接；
    ```
    @ApiModel
    @Data
    public class ResultLogin {
    
        @ApiModelProperty(value = "账号", required = false)
        String username;
    
    }
    ```

##  日志规范
1. 所有的service包下所有类上都必须加上lombok 的日志注解@Slf4j
    ```
    @Slf4j
    @Service
    public class LoginService {
    
        @Autowired
        private LoginMapper loginMapper;
    
        public ResponseEntity<ResultLogin> login(ParamLogin paramLogin) {
            // log 使用方式
            log.info("LoginService | login | param paramLogin：{}",paramLogin); 
            ResultLogin loginVo = new ResultLogin();
            return new ResponseEntity<ResultLogin>(loginVo, HttpStatus.OK);
        }
    }
    ```

##  实体类规范
1. 所有的实体类都必须加上lombok 的@Data注解，包括：接收前端的实体类、返回给前端的实体类、和数据库交互的实体类、其他情况自己构造的实体类；
    ```
    @ApiModel
    @Data
    public class ResultLogin {
    
        @ApiModelProperty(value = "账号", required = false)
        String username;
    
    }
    ```


##  注释规范
1. 每一个类或方法都需要清楚标明如下注释信息；

    ```
    /**
     * @Zuozhe ZhaoJian   @Date 2019-09-08
     *
     * @Desciption 登录
     *
     * @param paramLogin 登录参数
     * @param session 请求 session信息
     * @return ResponseEntity<ResultLogin>
     *
     */
    public ResponseEntity<ResultLogin> login(@Valid @RequestBody ParamLogin paramLogin, HttpSession session) {
        // 业务
    }
    ```

##  类内部规范
1. 类名与类成员变量之间空一行
2. 类成员变量之间空一行
3. 类成员变量与方法之间空二行
4. 方法参数之间必须要有一个空格

##  


