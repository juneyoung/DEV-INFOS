# Spring5 기본 예제 분석

[상위항목으로](https://github.com/juneyoung/DEV-INFOS/tree/master/Spring)

Spring5 스펙이 새로 공개되었음. 새로운 특징의 나열도 나열이지만 실무자로서 가장 잘 접할 수 있는 방법은 예제를 분석하는 것이라 생각이 들어 분석함. 예상대로 예제 하나 공부하는 것만으로 새로운 부분을 많이 알게 되었음.

## 00. 구성
- (I) MessageService.java : 할 행위를 정의
- (C) MessagePrinter.java : MessageService 인터페이스를 감싸는 Component
- (C) Application.java : 시작점

## 01. 소스

#### A. MessageService.java
```
public interface MessageService {
    String getMessage();
}
```
- 상속받은 클래스에서 각각 `getMessage` 메소드를 구현할 것임.

#### B. MessagePrinter.java

```
@Component
public class MessagePrinter {

    final private MessageService service;

    @Autowired
    public MessagePrinter(MessageService service){
        this.service = service;
    }

    public void printMessage(){
        System.out.println(this.service.getMessage());
    }
}
```
- `@Component` 어노테이션에 의해 `componentScan` 의 대상이 됨
- `final private MessageService service` 구문 삽입 시, IDE 가 변수가 초기화되지 않았다는 오류를 출력할 수 있음. 아래 행의 `@Autowired` 메소드 추가시 사라짐
- `@Autowired` 를 생성자에 걸어 인스턴스 생성시에 인자를 `bean` 내에서 찾도록 설정할 수 있음. [링크](https://docs.spring.io/spring/docs/5.0.x/javadoc-api/org/springframework/beans/factory/annotation/Autowired.html)

#### C. Application.java

```
@Configuration
@ComponentScan
public class Application {

    @Bean
    MessageService mockMessageService(){
        return new MessageService() {
            @Override
            public String getMessage() {
                return "Hello, World!";
            }
        };
    }

    public static void main (String[] args) throws Exception {
        ApplicationContext context = new AnnotationConfigApplicationContext(Application.class);
        MessagePrinter printer = context.getBean(MessagePrinter.class);
        printer.printMessage();
    }
}
```
- `@Configuration` 어노테이션을 사용함으로 인해 `mockMessageService` 메소드의 `@Bean` 어노테이션의 결과가 컨텍스트에 빈으로 등록되게 되었다
- `@ComponentScan` 으로 패키지 내 빈을 찾는다. `@ComponentScans` 라는 녀석도 있는데, 예제도 별로 없다(잘 사용되지 않는 듯)
- `AnnotationConfigApplicationContext` 를 이용하여 컨텍스트에 등록된 빈을 찾고, 빈에 등록된 메소드를 수행한다.

아마도 아래 순서대로 되는 듯

1. `Configuration` 어노테이션으로 `mockMessageService` 를 실행해서 `MessageService` 빈을 컨텍스트에 등록
2. `MessagePrinter` 인스턴스 생성시, `MessageService` 빈을 받게 되어있는데 1 에서 생성된 인스턴스 대입
3. 모든 구현체가 갖춰졌으니 수행


## 99. History
- 2017.11.18 : 초안작성
