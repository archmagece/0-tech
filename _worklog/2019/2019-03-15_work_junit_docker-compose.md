# junit docker-compose

plantir 라이브러리를 사용 할 때는 junit4에서만 사용.
@Rule을 써야되는데 junit5에서 쓰도록 만들어놓은 라이브러리가 있긴있다
수동 테스트에서는 돌아가나 gradle test에서 충돌발생


```groovy
testCompile "com.palantir.docker.compose:docker-compose-rule-junit4:${palantir_docker_compose_rule_junit4_version}"
```

```java
import org.junit.jupiter.api.extension.*;


public class DockerComposeExtension implements BeforeAllCallback, AfterAllCallback, ParameterResolver {

    private DockerComposeRule docker;

    public DockerComposeExtension() {
        docker = DockerComposeRule.builder()
                .pullOnStartup(true)
//                .file("src/test/resources/docker-compose.yml")
                .file("../devbox/docker-compose.yml")
                .saveLogsTo("build/test-docker-logs")
                .waitingForService("dev_mysql", toHaveAllPortsOpen())
                .waitingForService("dev_redis", toHaveAllPortsOpen())
                .build();
    }

    public void beforeAll(ExtensionContext extensionContext) throws Exception {
        docker.before();
    }

    public void afterAll(ExtensionContext extensionContext) throws Exception {
        docker.after();
    }

    public boolean supportsParameter(ParameterContext parameterContext, ExtensionContext extensionContext) throws ParameterResolutionException {
        return parameterContext.getParameter().getType().equals(DockerComposeRule.class);
    }

    public Object resolveParameter(ParameterContext parameterContext, ExtensionContext extensionContext) throws ParameterResolutionException {
        return docker;
    }

}
```

유닛테스트 코드
```java
import com.fasterxml.jackson.databind.ObjectMapper
import mapp.DockerComposeExtension
import mapp.app.config.AppConfig
import mapp.app.config.WebConfig
import mapp.config.TestConfig
import org.junit.jupiter.api.BeforeEach
import org.junit.jupiter.api.extension.ExtendWith
import org.springframework.beans.factory.annotation.Autowired
import org.springframework.boot.test.context.SpringBootTest
import org.springframework.context.annotation.Import
import org.springframework.restdocs.RestDocumentationContextProvider
import org.springframework.restdocs.RestDocumentationExtension
import org.springframework.restdocs.mockmvc.MockMvcRestDocumentation
import org.springframework.restdocs.templates.TemplateFormats
import org.springframework.test.context.junit.jupiter.SpringExtension
import org.springframework.test.web.servlet.MockMvc
import org.springframework.test.web.servlet.setup.DefaultMockMvcBuilder
import org.springframework.test.web.servlet.setup.MockMvcBuilders
import org.springframework.web.context.WebApplicationContext

//@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.MOCK, classes = [WebConfig::class])
@SpringBootTest(classes = [AppConfig::class, WebConfig::class])
@ExtendWith(RestDocumentationExtension::class, SpringExtension::class, DockerComposeExtension::class)
//@ExtendWith(RestDocumentationExtension::class, SpringExtension::class)
@Import(TestConfig::class)
class RestTestBase {

	protected lateinit var mockMvc: MockMvc

	@Autowired
	protected lateinit var mapper: ObjectMapper

	@BeforeEach
	fun setUp(webApplicationContext: WebApplicationContext,
			  restDocumentation: RestDocumentationContextProvider){

		this.mockMvc = MockMvcBuilders.webAppContextSetup(webApplicationContext)
				.apply<DefaultMockMvcBuilder>(MockMvcRestDocumentation
						.documentationConfiguration(restDocumentation)
//						.operationPreprocessors()
//						.withRequestDefaults(removeHea)
//						.withResponseDefaults(prettyprint())
						.snippets().withTemplateFormat(TemplateFormats.asciidoctor())
//						.snippets().withTemplateFormat(TemplateFormats.markdown())
				)
				.build()
	}

//	@AfterMethod
//	fun tearDown() {
//		this.restDocumentation.afterTest()
//	}

}
```

유닛 테스트 코드는 여기에
```java
//https://tothepoint.group/blog/spring-rest-docs/
//https://springboot.tistory.com/26
class RestPushkeyTest :RestTestBase(){

	@Test
	fun root() {
		this.mockMvc.perform(MockMvcRequestBuilders.get("/"))
				.andExpect(MockMvcResultMatchers.status().isOk)
				.andDo(MockMvcRestDocumentation.document("root"))
	}

	@Test
	fun pushkey_ios() {
		val requestDto = PushkeyRequestDto(
				appKey = "keykey00000000000000000000",
				enable = true
		)
		mapper.configure(SerializationFeature.WRAP_ROOT_VALUE, false)
		val writer = mapper.writer().withDefaultPrettyPrinter()
		this.mockMvc.perform(MockMvcRequestBuilders.post("/push/ios").contentType(MediaType.APPLICATION_JSON_UTF8).content(writer.writeValueAsBytes(requestDto)))
				.andExpect(MockMvcResultMatchers.status().isOk)
				.andDo(MockMvcRestDocumentation.document("push/ios"))
	}

	@Test
	fun pushkey_android() {
		val requestDto = PushkeyRequestDto(
				appKey = "keykey00000000000000000000",
				enable = true
		)
		mapper.configure(SerializationFeature.WRAP_ROOT_VALUE, false)
		val writer = mapper.writer().withDefaultPrettyPrinter()
		this.mockMvc.perform(MockMvcRequestBuilders.post("/push/android").contentType(MediaType.APPLICATION_JSON_UTF8).content(writer.writeValueAsBytes(requestDto)))
				.andExpect(MockMvcResultMatchers.status().isOk)
				.andDo(
						MockMvcRestDocumentation.document(
								"push/android",
								AsciiDocUtil.documentRequest, AsciiDocUtil.documentResponse,
//								PayloadDocumentation.requestBody(
//										"requestDto",
//										PayloadDocumentation.requestBody()
//										PayloadDocumentation.beneathPath("aaa").withSubsectionId("idid"),
//										mapOf(
//												Pair("app_key", "keyeky000000000"),
//												Pair("enable", true)
//										)
//								),
								PayloadDocumentation.requestFields(
										PayloadDocumentation.fieldWithPath("app_key").type(String).description(""),
										PayloadDocumentation.fieldWithPath("enable").type(Boolean).description("default true").optional()
								),
								PayloadDocumentation.responseFields(
										PayloadDocumentation.fieldWithPath("state").type(JsonFieldType.STRING).description("${PushKeyState.values()} 값 추가")
								)

//								this.document.snippets(
//								responseFields(
//										fieldWithPath("[].id").description("The persons' ID"),
//										fieldWithPath("[].firstName").description("The persons' first name"),
//										fieldWithPath("[].lastName").description("The persons' last name")
//								)
//						);
						)
				)
	}

}
```