---
title: 롬복 플러그인 설정 쉽게 하기(gradle)
tags: lombok
permalink: /lombok/1
---

<!--more-->
롬복 문서에서는 gradle를 통해 환경구성하는 방법을 2가지 소개하고 있습니다.

## 1. 플러그인 미사용
dependencies에 추가하는 방법으로 아마 가장 많이 사용하지 않을까 생각이 드네요


```groovy
ext {
    lombokVersion = '1.18.24'
}


repositories {
	mavenCentral()
}

dependencies {
	compileOnly 'org.projectlombok:lombok:${lombokVersion}'
	annotationProcessor 'org.projectlombok:lombok:${lombokVersion}'

	testCompileOnly 'org.projectlombok:lombok:${lombokVersion}'
	testAnnotationProcessor 'org.projectlombok:lombok:${lombokVersion}'
}
```

## 2. 플러그인 사용
io.freefair.lombok 플러그인을 이용해서 등록해서 dependencies 양을 줄일 수 있습니다.
```groovy
plugins {
//    ...
    id "io.freefair.lombok" version "4.1.6"
}

lombok {
    version = '1.18.4'
}
```
빌드시에는 gradle lombok 설정을 통해 lombokConfig가 만들어지기 때문에 lombok.config는 gitignore에 등록하시는게 좋습니다.



