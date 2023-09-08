# Spring学习

## 控制反转

## 常用注解

> 声明Bean的注解  

@Component  

注解是一个泛化的概念，仅仅表示一个组件对象（Bean），可以作用在任何层次上，没有明确的角色


@Repository  

将数据访问层（DAO）类标识为Bean，注解数据访问层Bean，功能与Comment相同


@Service  

标注一个业务逻辑组件类（Service层）功能与Component


@Controller  

注解用于标注一个控制器组件类（Spring MVC的controller）,功能与@Component()相同





> //注入Bean的注解

@Autowired  

对类的成员变量、方法、构造方法进行标注，自动装配的工作。通过此方法可以消除setter和getter方法，默认按照Bean的类型进行装配


@Resource

与@Autowired功能一样。区别在于，该注解默认按照名称装配注入，只有当找不到与名称相配的Bean  时才会按类型装配注入，Autowired默认按Bean类型装配，如想按名称装配注入，结合Qualifier注解一起使用

有name和type属性，name指定Bean的实例名称，type指定Bean类型


@Qualifier

与Autowired注解配合使用，Autowired注解需要按照名称装配注入时，结合该注解一起使用，Bean实例名称由Qualifier注解的参数指定


