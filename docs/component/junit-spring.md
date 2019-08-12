# Junit测试Spring

不同项目获取Spring容器的方式不同，主要有以下三种情况

## 通过xml配置Spring

```xml
<context:component-scan base-package="com"></context:component-scan>
```

通过xml配置Spring的项目，可以用``classPathXmlApplicationContext``获取容器

```java
ClassPathXmlApplicationContext classPathXmlApplicationContext
                = new ClassPathXmlApplicationContext("classpath:spring.xml");
IndexService service = (IndexService) classPathXmlApplicationContext.getBean("service");
service.service();
```

但是这种方式会加载Spring所有的对象，速度相当慢。所以可以针对需要的对象进行注入：

1. 加载配置文件

   ```java
   @RunWith(SpringJUnit4ClassRunner.class)  //使用junit4进行测试
   @ContextConfiguration("classpath:spring/spring-context.xml")
   public class BaseJunit4Test {
   
   }
   ```

2. 继承加载类，直接注入使用

   ```java
   public class SpringJunitTest extends BaseJunit4Test{
   
       @Autowired
       IEdaDenlCollAuditApi edaDenlCollAuditApi;
   
       @Test
       public void testSpring() {
           List<EdaDenlCollAudit> list = edaDenlCollAuditApi.findAllList();
           System.out.println(list.size());
       }
   
   }
   ```

   如果涉及到插入操作，添加回滚事务注解

   ```java
   @Transactional   //标明此方法需使用事务
   @Rollback(false)  //标明使用完此方法后事务不回滚,true时为回滚
   ```

## 通过java文件配置Spring

```java
@Configuration
@ComponentScan("com.liyb.*")
public class SpringConfig {
    
}
```

与xml配置相似，通过java文件配置的，用``AnnotationConfigApplicationContext``获取容器对象

```java
AnnotationConfigApplicationContext annotationConfigApplicationContext = new AnnotationConfigApplicationContext(SpringConfig.class);
IndexService service = (IndexService) annotationConfigApplicationContext.getBean("indexService");
```

## 通过SpringBoot加载配置文件

SpringBoot单元测试，从容器中获取对象的方式：

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class SpringJunitTest {

    @Autowired
    IEdaAcceptApplyService edaAcceptApplyService;

    @Test
    public void selectTest(){
        QueryWrapper<EdaAcceptApply> queryWrapper = new QueryWrapper<>();
        queryWrapper.orderBy(true, false, "SORT");
        IPage<EdaAcceptApply> edaAcceptApplyIPage = edaAcceptApplyService.page(new Page<>(1,5), queryWrapper);
        System.out.println(edaAcceptApplyIPage.getTotal());
    }

}

```







