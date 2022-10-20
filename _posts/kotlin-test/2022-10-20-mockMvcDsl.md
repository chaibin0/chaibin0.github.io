---
title: WebMvcTest에서 mockMvc 403 에러
tags: mockMvc
permalink: /mockMvc/1
---


<!--more-->
mockMvc 403 에러

GET Method 이외의 POST, PUT, PATCH에서 mockMvc 테스트할 때 항상 403으로 나오는 에러가 있다.
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
