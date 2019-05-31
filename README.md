消费者服务配置
spring:
  application:
    name: consumer-user
server:
  port: 8200
eureka:
  instance:
    prefer-ip-address: true #注册服务的时候使用服务的ip地址
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
 代码示例：
 @EnableDiscoveryClient //开启发现服务
@SpringBootApplication
public class ConsumerUserApplication {

    public static void main(String[] args) {
        SpringApplication.run(ConsumerUserApplication.class, args);
    }


  /*  @LoadBalanced //使用负载均衡机制
    @Bean
    public RestTemplate restTemplate(){
        return new RestTemplate();
    }*/
}
##注册中心
server:
  port: 8761
eureka:
  instance:
    hostname: eureka-server #eureka-server主机名字
  client:
    register-with-eureka: false #不把自己注册到eureka上
    fetch-registry: false #不从eureka上来获取服务的注册信息
    service-url:
      defaultZone: http://localhost:8761/eureka/
代码示例：
/**
 * @author bitao 
 * 注册中心
 * 1.配置Eureka信息
 * 2.@EnableEurekaServer
 */
@EnableEurekaServer
@SpringBootApplication
public class EurekaServerApplication {

    public static void main(String[] args) {
        SpringApplication.run(EurekaServerApplication.class, args);
    }

}
#消息提供者
server:
  port: 8001
spring:
  application:
    name: provider-ticket #提供者名字
eureka:
  instance:
    prefer-ip-address: true #注册服务的时候使用服务的IP注册
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka
