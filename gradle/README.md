## Gradle 파일 작성하기

[메인으로](https://github.com/juneyoung/DEV-INFOS)

### 개요

이하는 spring-boot 를 사용하면서 만나게 될 `*.gradle` 문서를 작성하는 방식에 대해 다루고 있음. `gradle` 은 기본적으로 [Groovy](http://www.groovy-lang.org/index.html) 라는 언어를 사용하는데 굳이 다 알 필요는 없어보임.:+1:

### `gradle` 빌드 순서

아래는 [spring-boot 공식 가이드](https://spring.io/guides/gs/spring-boot/) 에서 제공되는 `build.gradle` 파일임 - 2017.06.11.
```
buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:1.5.2.RELEASE")
    }
}

apply plugin: 'java'
apply plugin: 'eclipse'
apply plugin: 'idea'
apply plugin: 'org.springframework.boot'

jar {
    baseName = 'gs-spring-boot'
    version =  '0.1.0'
}

repositories {
    mavenCentral()
}

sourceCompatibility = 1.8
targetCompatibility = 1.8

dependencies {
    compile("org.springframework.boot:spring-boot-starter-web") {
        exclude module: "spring-boot-starter-tomcat"
    }
    compile("org.springframework.boot:spring-boot-starter-jetty")
    compile("org.springframework.boot:spring-boot-starter-actuator")
    testCompile("junit:junit")
}
```



### 옵션

- `-X {테스크 명}` : 빌드시 해당 task 를 건너 뛴다. 예시 `gradle build -X test`
- `--refresh-dependencies` : 빌드시 dependencies 캐시를 갱신. 예시 `gradle build --refresh-dependencies`


### 기타

- intellij 에서는 dependencies 에 라이브러리 추가에 실패해도 `BUILD SUCCESS` 가 난다. 항상 Maven repositories 를 최신으로 update 해야 함


### History

- 2017.06.11 : 초안 작성
