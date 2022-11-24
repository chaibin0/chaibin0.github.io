---
title: WebMvcTest에서 mockMvc 403 에러
tags: mockMvc
permalink: /mockMvc/1
---


<!--more-->
mockMvc 403 에러

GET Method 이외의 POST, PUT, PATCH에서 mockMvc 테스트할 때 403번으로 에러가 발생했습니다.

mockMvc에서 csrf를 추가하여 Security 문제를 해결 했습니다.

SecurityMockMvcRequestPostProcessors

### 1. SecurityMockMvcRequestPostProcessors 추가

```kotlin
   mockMvc.patch("/patch") {
    contentType = MediaType.APPLICATION_JSON
    content = jsonBody
    with(SecurityMockMvcRequestPostProcessors.user(withMockAdminUser()))
    with(SecurityMockMvcRequestPostProcessors.csrf())
  }.andExpect {
    status { isBadRequest() }
  }
```


### 2. 확인중

Security관련 Bean을 테스트코드에서도 반영될 수 있도록 수정
