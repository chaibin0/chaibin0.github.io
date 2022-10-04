---
title: spring + kotest 사용경험 정리
tags: TeXt
permalink: /kotest/1
---


<!--more-->
kotest 사용경험 정리

### 1. gradle 의존성 추가

```kotlin
    /* 기존 mockito 사용 중단 */
dependency {
  testImplementation("org.springframework.boot:spring-boot-starter-test") {
    exclude(module = "mockito-core")
  }

  testImplementation("com.h2database:h2")

  /* mockK + spring Extension */
  testImplementation("io.mockk:mockk:1.13.1")
  testImplementation("com.ninja-squad:springmockk:3.1.1")

  /* kotest + spring Extension */
  testImplementation("io.kotest.extensions:kotest-extensions-spring:1.1.2")
  testImplementation("io.kotest:kotest-assertions-core-jvm:5.5.0")
  testImplementation("io.kotest:kotest-runner-junit5:5.5.0")
}
```

* com.ninja-squad:springmockk:3.1.1는 @MockBean, @SpyBean을 쓰기 위함

### 2. JPA Test

@DataJpaTest 어노테이션을 사용한 테스트

FreeSpec으로 사용
```kotlin
@DataJpaTest
class StudentRepositoryTest(
  @Autowired
  var studentRepository: StudentRepository
) : FreeSpec({
  "저장테스트" - {
    val student =
      Student(1, "이름", LocalDate.now(), LocalDateTime.now(), "ADMIN")

    val savedStudent = studentRepository.save(student)
    savedStudent.id shouldBe 1
  }
})
```

작성중
### 3. Controller Test


### 4. Service Test

### 5. Util test

---

### Reference

https://kotest.io/docs/extensions/spring.html
https://kotest.io/docs/framework/writing-tests.html
