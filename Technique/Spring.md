## [@Resource vs @Autowired](https://stackoverflow.com/questions/4093504/resource-vs-autowired)

* @Resource allows you to specify a name of the injected bean
* @Resource means get me a known resource by name. The name is extracted from the name of the annotated setter or field, or it is taken from the name-Parameter.

* @Autowired allows you to mark it as non-mandatory.
* @Inject or @Autowired try to wire in a suitable other component by type.

## [spring-boot hotswapping](https://docs.spring.io/spring-boot/docs/current/reference/html/howto-hotswapping.html)

Maven
```
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-devtools</artifactId>
		<optional>true</optional>
	</dependency>
</dependencies>
```

* Developer tools are automatically disabled when running a fully packaged application.
* Repackaged archives do not contain devtools by default.

## spring @RequestBody

```Java
@RequestMapping("/list")
public List<Object> list(@RequestBody Object obj) {
    // data...
    return null;
}
```
Headers Content-Type=application/json <br/>
Body {}, then request params is null, if it were otherwise, would be error HttpMessageNotReadableException: Required request body is missing

## [spring @RestController](https://spring.io/guides/gs/rest-service-cors/#_create_a_resource_controller)

A key difference between a traditional MVC controller and the RESTful web service controller is the way that the HTTP response body is created. Rather than relying on a view technology to perform server-side rendering of the greeting data to HTML, this RESTful web service controller simply populates and returns a Greeting object. The object data will be written directly to the HTTP response as JSON.

To accomplish this, the @ResponseBody annotation on the greeting() method tells Spring MVC that it does not need to render the greeting object through a server-side view layer, but that instead the greeting object returned is the response body, and should be written out directly.

The Greeting object must be converted to JSON. Thanks to Spring’s HTTP message converter support, you don’t need to do this conversion manually. Because Jackson is on the classpath, Spring’s MappingJackson2HttpMessageConverter is automatically chosen to convert the Greeting instance to JSON.

## [Make the application executable](https://spring.io/guides/gs/rest-service-cors/#_make_the_application_executable)

@SpringBootApplication is a convenience annotation that adds all of the following:

* `@Configuration` tags the class as a source of bean definitions for the application context.
* `@EnableAutoConfiguration` tells Spring Boot to start adding beans based on classpath settings, other beans, and various property settings.
Normally you would add `@EnableWebMvc` for a Spring MVC app, but Spring Boot adds it automatically when it sees spring-webmvc on the classpath. This flags the application as a web application and activates key behaviors such as setting up a `DispatcherServlet`.
* `@ComponentScan` tells Spring to look for other components, configurations, and services in the same package, allowing it to find the controllers.

The main() method uses Spring Boot’s SpringApplication.run() method to launch an application. Did you notice that there wasn’t a single line of XML? No web.xml file either. This web application is 100% pure Java and you didn’t have to deal with configuring any plumbing or infrastructure.

## [Cross-Origin Resource Sharing (CORS)](https://spring.io/guides/gs/rest-service-cors/#_enabling_cors)
[blog post](https://spring.io/blog/2015/06/08/cors-support-in-spring-framework)<br/>
Cross-Origin Resource Sharing (CORS) is a technique for relaxing the same-origin policy, allowing Javascript on a web page to consume a REST API served from a different origin.

### Enabling CORS

* Controller method CORS configuration

@CrossOrigin(origins = "http://google.com")

* Global CORS configuration

```Java
@Configuration
public class MyConfiguration {

    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurerAdapter() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/**")
                  .allowedOrigins("http://example.com")
                  .allowedMethods("PUT", "DELETE")
                  .allowedHeaders("header1", "header2", "header3")
                  .exposedHeaders("header1", "header2")
                  .allowCredentials(false).maxAge(3600);
            }
        };
    }
}
```

## Spring boot return html, annotated class is a "Controller", is not "RestController"

## [Scheduling Tasks](https://spring.io/guides/gs/scheduling-tasks/)

* Create a scheduled task

```java
@Component
public class ScheduledTasks {

  private static final Logger log = LoggerFactory.getLogger(ScheduledTasks.class);

  private static final SimpleDateFormat dateFormat = new SimpleDateFormat("HH:mm:ss");

  @Scheduled(fixedRate = 5000)
  public void reportCurrentTime() {
    log.info("The time is now {}", dateFormat.format(new Date()));
  }
}
```
 * Enable Scheduling
 
 ```java
@SpringBootApplication
@EnableScheduling
public class Application {

  public static void main(String[] args) {
    SpringApplication.run(Application.class);
  }
}
 ```

* Cron expression

A Cron expression consists of six sequential fields  
second, minute, hour, day of month, month, day(s) of week

// run every morning at 6 AM  
@Scheduled(cron = "0 0 6 * * ?")

References  
https://riptutorial.com/spring/example/21209/cron-expression  
https://stackoverflow.com/questions/26147044/spring-cron-expression-for-every-day-101am
