### ArchUnit
[Official homepage](https://www.archunit.org/getting-started)

#### 개요
ArchUnit 은 자바 프로젝트의 구조를 강제하기 위한 테스트 프레임워크이다. 사용자가 정의한 Rule 을 위배하는 경우 테스트 실패를 출력한다.

#### 설치
maven 이나 gradle 에 dependencies 를 추가하여 설치한다. ex) maven
```xml
<!-- https://mvnrepository.com/artifact/org.springdoc/springdoc-openapi-webmvc-core -->
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-webmvc-core</artifactId>
    <version>${org.springframework.openapi.version}</version>
    <scope>test</scope>
</dependency>
```


#### 라이브러리 구성
<table>
    <thead>
        <tr>
            <td>패키지</td>
            <td>역할</td>
            <td>기타</td>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>core</td>
            <td>기본 자바 객체의 랩핑 객체를 제공한다. 해당 객체는 관계 그래프 정보를 가지고 있음</td>
            <td>JavaClass, JavaMethod, JavaField ...</td>
        </tr>
        <tr>
            <td>lang</td>
            <td>사용자에게  익숙하도록 fluent API 를 제공한다</td>
            <td>ArchRule</td>
        </tr>
        <tr>
            <td>library</td>
            <td>구체적으로 Layer 기반의 Architecture 나 Onion Architecture 의 구현을 적용함</td>
            <td></td>
        </tr>
    </tbody>
</table>

#### 용어
- layer : Layer Architecture 에서 사용되는 개념으로 Controller, Service, Persistence 등의 레이어를 의미
- slice : 패키지 간 관계를 정의하기 위한 개념으로 module 과 비슷한 것으로 느껴짐

#### 샘플 용례 및 설명

```java
// .. 는 임의의 수의 모든 패키지를 의미함
// accessThat 은 메서드 호출이고 dependOn 은 클래스 의존을 나타냄
// classes.that()에 인수로 Predicate 를 넘겨 대상을 정의할 수 있고
// should 안에 Condition 을 상속받은 ArchCondition 을 넣어 사용자 정의 룰도 만들 수 있다.
// slice 경로 규칙
// p.(*).. - p 패키지 이하 패키지의 클래스를 정렬함
// p.(**) - p 패키지 이하의 모든 서브패키지를 포함함
// p.(**).service.. - p 패키지 이하의 service 패키지 이상의 모든 클래스
@AnalyzeClasses(packages = {"org.owls.archunit"})
public class ArchUnitTest {
 
    private static final String ROOT_PACKAGE_NAME = "org.owls.archunit";
    private static JavaClasses topPackageClasses;
    private static final Logger logger = LoggerFactory.getLogger(ArchUnitTest.class);
 
    private static final ArchCondition noPublicSetterCondition = new ArchCondition<JavaClass>("No public setter for immutable pattern") {
        @Override
        public void check(JavaClass javaClass, ConditionEvents conditionEvents) {
//            for (JavaMethod method: javaClass.getAllMethods()) { // 상위의 모든 메소드 포함
            for (JavaMethod method: javaClass.getMethods()) {
                logger.info("=====> No public setter condition - method: {}, modifier: {}", method.getName(), method.getModifiers());
                if (method.getName().startsWith("set") && method.getModifiers().contains(JavaModifier.PUBLIC)) {
                    conditionEvents.add(SimpleConditionEvent.violated(javaClass, "No public setter allowed"));
                }
            }
        }
    };
 
    private static final String CONTROLLER_LAYER = "Controller",
            SERVICE_LAYER = "Service",
            PERSISTENCE_LAYER = "Persistence";
    private static final DescribedPredicate<JavaClass> controllerLayerDefine = new DescribedPredicate<JavaClass>(CONTROLLER_LAYER) {
        @Override
        public boolean test(JavaClass javaClass) {
            boolean isValidName = javaClass.getName().toLowerCase().contains("controller");
            boolean isAnnotated =  javaClass.isAnnotatedWith(Controller.class) || javaClass.isAnnotatedWith(RestController.class);
            return isValidName || isAnnotated;
        }
    };
 
    private static final DescribedPredicate<JavaClass> serviceLayerDefine = new DescribedPredicate<JavaClass>(SERVICE_LAYER) {
        @Override
        public boolean test(JavaClass javaClass) {
            boolean isValidName = javaClass.getName().toLowerCase().contains("service");
            boolean isAnnotated =  javaClass.isAnnotatedWith(Service.class);
            return isValidName || isAnnotated;
        }
    };
 
 
    private static final DescribedPredicate<JavaClass> persistenceLayerDefine = new DescribedPredicate<JavaClass>(PERSISTENCE_LAYER) {
        @Override
        public boolean test(JavaClass javaClass) {
            boolean isValidName = javaClass.getName().toLowerCase().contains("repository");
            boolean isAnnotated =  javaClass.isAnnotatedWith(Repository.class);
            return isValidName || isAnnotated;
        }
    };
 
    @BeforeAll
    public static void setUp () {
        ImportOption ignoreTestOptions = location -> !location.contains("/test/");
        topPackageClasses = new ClassFileImporter()
                .withImportOption(ignoreTestOptions)
                .withImportOption(ImportOption.Predefined.DO_NOT_INCLUDE_JARS)
                .importPackages(ROOT_PACKAGE_NAME);
    }
 
    /**
     * 순환 참조 금지
     */
    @Test
    public void testNoCycleDependenciesAllowed() {
        // 순환 참조 금지
        slices().matching("org.owls.archunit.(**)")
            .should().beFreeOfCycles();
 
        // 상호 참조 금지
        slices().matching("org.owls.archunit.(**)")
            .should().notDependOnEachOther();
    }
 
    /**
     * web package 외부에는 @Controller, @RestController 가 허용되지 않음
     */
    @Test
    public void testNoWebStereoTypeAllowedOutsideOfWeb() {
        //
        String webPackage = "org.owls.archunit.web..";
        ArchRule noControllerAllowedOutsideWeb = classes().that()
                .areAnnotatedWith(Controller.class)
                .should()
                .resideInAPackage(webPackage);
        noControllerAllowedOutsideWeb
                .allowEmptyShould(true) // @Controller 애노테이션은 실제 존재하지 않기 때문에 search 검사가 비었을 때도 통과  하도록 설정한다
                .check(topPackageClasses);
 
        ArchRule noRestControllerAllowedOutsideWeb = classes().that().areAnnotatedWith(RestController.class)
                .should().resideInAPackage(webPackage);
        noRestControllerAllowedOutsideWeb.check(topPackageClasses);
    }
 
    /**
     * web package 에는 Service 나 Repository 스테레오 타입이 허용되지 않음
     */
    @Test
    public void testNoServiceRepositoryStereoTypeAllowedInWeb() {
        String webPackage = "org.owls.archunit.web..";
        ArchRule noServiceRepositoryAreAllowedInWeb = noClasses().that()
                .areAnnotatedWith(Service.class).or().areAnnotatedWith(Repository.class)
                .should()
                .resideInAPackage(webPackage);
        noServiceRepositoryAreAllowedInWeb
                .allowEmptyShould(true) // @Controller 애노테이션은 실제 존재하지 않기 때문에 search 검사가 비었을 때도 통과  하도록 설정한다
                .check(topPackageClasses);
    }
 
    @Test
    public void testNoServiceRepositoryAccessedByController() {
        ArchRule noServiceRepositoryAccessedByController = noClasses().that()
                .areAnnotatedWith(Service.class)
                .or().areAnnotatedWith(Repository.class)
                .should().dependOnClassesThat()
                .areAnnotatedWith(Controller.class)
                .orShould().dependOnClassesThat()
                .areAnnotatedWith(RestController.class);
        noServiceRepositoryAccessedByController.check(topPackageClasses);
    }
 
    /**
     * Audit package 는 외부 패키지로부터 참조될 수 없음
     */
    @Test
    public void testAuditPackageShouldNotReferredByBidPackage() {
        ArchRule rule = noClasses().that().resideInAnyPackage("..audit..")
                .should().accessClassesThat().resideInAnyPackage("..bid..");
        rule.check(topPackageClasses);
    }
 
    /**
     * 객체는 Immutable 이어야 함
     * immutable 의 정의를 외부에 setter 가 노출되지 않음으로 함
     */
    @Test
    public void testValueObjectShouldBeImmutable () {
        ArchRule noPublicSetterRule = classes().that().belongToAnyOf(BetaDistribution.class)
                .should(noPublicSetterCondition);
        noPublicSetterRule.check(topPackageClasses);
    }
 
    /**
     * 각각의 레이어를 정의하고 레이어 별 접근을 제한함
     */
    @Test
    public void testLayeredArchitecture() {
        layeredArchitecture()
                .consideringAllDependencies()
                .layer(CONTROLLER_LAYER).definedBy(controllerLayerDefine)
                .layer(SERVICE_LAYER).definedBy(serviceLayerDefine)
                .layer(PERSISTENCE_LAYER).definedBy(persistenceLayerDefine)
                .whereLayer(CONTROLLER_LAYER).mayNotAccessAnyLayer()
                .whereLayer(SERVICE_LAYER).mayOnlyAccessLayers(CONTROLLER_LAYER)
                .whereLayer(PERSISTENCE_LAYER).mayOnlyAccessLayers(CONTROLLER_LAYER, SERVICE_LAYER);
    }
}
```
- @AnalyzeClasses: JUnit5 를 지원하는 ArchUnit 의 애노테이션으로 별도의 ExtendWith 가 필요없다
- setUp: 설정 매소드로 withImportOption 메소드를 통해 포함하거나 예외적인 범주를 지정할 수 있다
- Custom 대상 설정
  - classes, noClasses 이후에 나오는 that 메소드에 Predicate 를 던져 대상을 커스텀 할 수 있다
- Custom Rule 설정
  - ArchCondition 을 생성하여 should 에 할당하면 커스텀 룰을 적용 가능하다
- layer architecture test
  - DescribePredicate 를 통하여 Layer 의 범주를 수동으로 정할 수 있다
  - 각각의 지정된 레이어 간의 룰을 정의할 수 있다
- 기본 검증의 경우, ArchRule.check 로 assertion 을 수행한다

#### 곁가지
- 없음
