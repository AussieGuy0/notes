# Spring

## General Notes

- **Spring Development Process**
    1. Configure spring beans
    2. Create spring container (e.g ApplicationContext)
    3. Retrieve beans from spring container

## Spring Container
- Create and manage objects (Inversion of Control)
- Inject object's dependencies (Dependency Injection)
    - 3 common types of injection: Constructor, Setter and Field
    - Constructor: Object is built from constructor
    - Setter: Object has fields added to it via setters
    - Field: Fields added directly 
    - Spring recommends constructor inject for mandatory dependencies, and setter based injection for optional depndencies

## Configuration

### XML configuration file (legacy)
- XML config can be very verbose
- No compiler support

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 
       http://www.springframework.org/schema/beans/spring-beans.xsd">
              
    <bean id="myFortune"
            class="me.anthonybruno.spring.springdemo.fortune.HappyFortuneService"/>
                            
    <bean id="myCoach"
            class="me.anthonybruno.spring.springdemo.coach.TrackCoach"> <!-- Contructor Injection -->
            <constructor-arg  ref="myFortune"/>
    </bean>
                                                      
    <bean id="myCricketCoach"
            class="me.anthonybruno.spring.springdemo.coach.CricketCoach">  <!-- Setter injection -->
             <property name="fortuneService" ref="myFortune"/>
             <property name="emailAddress" value="bla@gmail.com" />
             <property name="team" value="Sunrisers Hyderabad" />
     </bean>
</beans>

```


### Java Annotations
- Allows configuration using Annotations
- Spring will scan java classes for special annoations and automatcally register the beans in Spring
- @Component is the annotation to be used 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 
       http://www.springframework.org/schema/beans/spring-beans.xsd">
       
       <context:component-scan base-package="full.package.name" /> <!-- Spring will recursively scan this package -->
              
</beans>
```

```java
@Component("thatCoach") //Register bean with id 'thatCoach'
public class TennisCoach implements Coach {


}

```

- If bean id not given, bean id will be lower cased class name (e.g class of TennisCoach will have default bean id of tennisCoach)

#### Autowire
- Spring will look for a class that matches the property and inject it automatically
    - Matches by type: class or interface
    - Supports constructor, setter and field injections
- Use @Autowired annotation

```java
@Component 
public class TennisCoach implements Coach { 
    
    private final FortuneService fortuneService;
    
    private Name name;
    
    @Autowired //Field injection, works even for private fields
    private Email email;

    @Autowired
    public TennisCoach(FortuneService fortuneService) { //Constructor injection
        this.fortuneService = fortuneService; 
    }
    
    @Autowired
    public void setName(Name name) {  //Setter injection
        this.name = name; 
    }


}

```

- If multiple Beans match autowire configuration, an exception will be thrown
    - Use @Qualifier("beanId") to define whch bean to use

```java
@Component 
public class TennisCoach implements Coach { 

    private final FortuneService fortuneService;
    
    @Autowired
    @Qualifer("coachEmail")
    private Email email;
    
    
    @Autowired
    public TennisCoach(@Qualifer("HappyFortuneService") FortuneService fortuneService) { //Constructor injection
        this.fortuneService = fortuneService; 
    }

}

```

#### Scope

- Can define scope using @Scope annotation
    - e.g @Scope("prototype")

```java
@Component 
@Scope("prototype")
public class TennisCoach implements Coach { 
}

```

#### Construct/Destroy methods

- Methods with @PostConstruct will run after bean is instatied
- Methods with @PreDestroy will run just before bean is destroyed
- "Protoype" scope beans will not call pre destroy method

### Java Source Code
- Absolutley no XML when configuration using source code
1. Create a class with `@Configuration` annotation
2. Add `@ComponentScan("com.package.name")` annotation (optional)
4. Use `AnnotationConfigApplicationContext` to read config class and use to create beans
	- e.g `new AnnotationConfigApplicationContext(Config.class);`

- Alternative to component scan is to use `@Bean`

```java
@Configuration
public class SportsConfig {

    @Bean
    public FortuneService sadFortuneService() { //Method name is the beanid
        return new SadFortuneService();
    }

    @Bean
    public Coach swimCoach() {
        return new SwimCoach(sadFortuneService());
    }
}

```

#### Properties
- Use `@PropertySource` in configuration class
- Use `@Value("${name.value}")` to inject property values

## Bean Scopes
- Set scope via scope attribute

- Singleton (default)
    - Only one instance is created
    - All requests to bean will return shared reference to same bean
- Prototype
    - Create a new bean instance for each container request

## Bean Lifecycle
1. Bean Instatintiated
2. Dependencies Injected
3. Internal Spring Processing
4. Custom Init Method (set method using 'init-method' attribute)
5. Bean is ready for use
6. Custom destroy method (set method using 'destroy-method' attribute)

- Custom init/destroy methods should be no-args public void methods
- Prototype scoped beans does not call destroy method

## Spring MVC
- Framework for building web applications in java
- Based on model-view-controller design pattern

### Components
- A set of web pages to layout UI components
- A collection of Spring beans (controllers, services)
- Spring configuration (XML, Annotations, Java)

#### Controller
- Contains buisness logic
    - Handle request
    - Store/retrieve data
    - Place data in model

```java
@Controller
public class HomeController {

    @RequestMapping("/")
        public String showMyPage() {
            return "main-menu";
        }

}
```

#### Model
- Contains data
- Can add data to model to be retrieved in the view
- Access the model details using a `HttpServletRequest` or with `@RequestParam("paramName")`


```java
@Controller
public class FormController {

    @RequestMapping("/processForm")
        public String showData(HttpServletRequest request, Model model) {
            String studentName = request.getParameter("studentName");
            String result = "Yo! " + studentName.toUpperCase();
            model.addAttribute("message", result);
                                
            return "processed-form";
        }

}
```


```html
<!-- processed-form.jsp -->
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
    <body>
    
    <h1>Hello World!</h1>
    
    <p>Student name: ${param.studentName}</p>
    
    <p>The message: ${message}</p> <!-- message references message in FormController -->
    
    </body>
</html>
```

### Configuration
1. Add configurations to file: WEB-INF/web.xml
    - Configure Spring MVC Dispatcher Servlet
    - Set up URL mappings to Spring MVC Dispatcher Servlet
2. Add configurations to file: WEB-INF/spring-mvc-demo-servlet.xml
    - Add support for component scanning
    - Add support for conversion, formatting and validation
    - Configure Spring MVC View Resolver
### Annotations
#### Class
- @RestController (Specify that the class  is a controller and it's methods return response bodies)
- @RequestMapping (The base url for all endpoints (methods) in the class)

#### Method
- @RequestMethod (accepts a (GET, POST, etc) to the endpoint defined by it's value)
