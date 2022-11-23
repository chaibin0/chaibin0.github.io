---
title: spring open api Server https 설정 문제
tags: spring springdocs swagger
permalink: /spring/openapi/1
---

<!--more-->
로컬은 http로 사용하고 있는데 dev, qa, stg는 https로 구성되어 있지만 Swagger에서 실행하다보면 전부 Http로 나와있는 경우가 있습니다.
SpringDocs 옵션을 통해서 http, https에 구애받지 않는 환경으로 설정이 필요합니다.
Server()를 환경별로 application.yml로 지정해서 property값을 받아서 처리할 수 있지만
url을 "/"으로 설정하여 간단하게 수정할 수 있습니다.

```kotlin
@Configuration
class SpringDocsConfiguration {

  @Bean
  fun customOpenApi(): OpenAPI = OpenAPI().components(
    Components().addSecuritySchemes(
      "TOKEN",
      SecurityScheme()
        .type(SecurityScheme.Type.APIKEY)
        .name("TOKEN")
        .scheme("TOKEN")
        .`in`(SecurityScheme.In.HEADER)
    )
  ).info(
    Info()
      .title("title")
      .version("1")
      .description("description")
  ).addServersItem(Server().apply {
    url = "/"
  }).externalDocs(ExternalDocumentation())
}
```
