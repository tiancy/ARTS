# Tip

## [Make the application executable](https://spring.io/guides/gs/rest-service-cors/#_make_the_application_executable)

@SpringBootApplication is a convenience annotation that adds all of the following:

* `@Configuration` tags the class as a source of bean definitions for the application context.
* `@EnableAutoConfiguration` tells Spring Boot to start adding beans based on classpath settings, other beans, and various property settings.
Normally you would add `@EnableWebMvc` for a Spring MVC app, but Spring Boot adds it automatically when it sees spring-webmvc on the classpath. This flags the application as a web application and activates key behaviors such as setting up a `DispatcherServlet`.
* `@ComponentScan` tells Spring to look for other components, configurations, and services in the same package, allowing it to find the controllers.

The main() method uses Spring Boot’s SpringApplication.run() method to launch an application. Did you notice that there wasn’t a single line of XML? No web.xml file either. This web application is 100% pure Java and you didn’t have to deal with configuring any plumbing or infrastructure.

## [VSCode Clean the workspace directory](https://github.com/redhat-developer/vscode-java/wiki/Troubleshooting#clean-the-workspace-directory)

In some occasions, deleting the Java Language Server workspace directory is helpful to go back to a clean slate.

MacOS : $HOME/Library/Application Support/Code[ - Variant]/User/workspaceStorage/

Build failed, do you want to continue?
Problem solved I resolved this issue by clearing the workspace cache in VS code.

# Share

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
