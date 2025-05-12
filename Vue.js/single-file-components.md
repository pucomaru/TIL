
# 📘 Vue.js 강의 정리 노트


## 📌 Component

### ▶ 정의
- 재사용 가능한 코드 블록  
- UI를 독립적이고 재사용 가능한 일부분으로 분할하고 각 부분을 개별적으로 다룰 수 있음


## 📌 Single-File Components (SFC)

### ▶ 정의
- 템플릿, 로직, 스타일을 하나의 `.vue` 파일로 구성하는 특수한 형식

### ▶ 구성 요소

#### 📄 `<template>`
- HTML 구조 정의
- 하나의 `.vue` 파일에 **하나만 포함 가능**

#### 📄 `<script setup>`
- Vue 3에서 권장되는 구성 방식
- `setup()` 함수의 역할을 하며, 변수 및 함수를 템플릿에서 직접 사용 가능
- 일반 `<script>`와 함께 쓸 수는 없음

#### 🎨 `<style scoped>`
- 여러 style 블록 작성 가능
- `scoped` 속성 사용 시 해당 컴포넌트 내부에만 스타일 적용됨
- 사용하지 않으면 전역 스타일로 퍼짐


## 📌 Node.js의 영향

- 기존 JavaScript는 브라우저에서만 동작했음
- Node.js 등장 이후 서버에서도 실행 가능해져, **FE와 BE 모두 JS로 개발 가능**
- NPM을 통해 다양한 오픈 소스 라이브러리 사용 가능  
  → 코드 재사용, 공유, 생산성 향상


## 📌 Module

### ▶ 정의
- 프로그램을 구성하는 독립적인 코드 블록 (`.js` 파일 하나 = 하나의 모듈)

### ▶ 필요성
- 앱이 커지면 하나의 파일에 모든 기능을 담기 어려움
- 기능을 여러 파일로 분리하면서 **모듈** 개념이 생김

### ▶ 한계
- 모듈 수가 많아지면 성능 병목 및 의존성 복잡도 증가
- 어떤 모듈에서 문제가 생겼는지 추적 어려움



## 📌 Bundler

- 여러 모듈/파일을 하나 또는 여러 개의 **번들(bundle)** 로 묶는 도구
- Webpack, Vite 등
- 코드 최적화 + 의존성 처리 + 성능 개선에 핵심

---

## 📦 Vue 프로젝트 구조

### ▶ 기본 구조

```

my-vue-project/
├── public/
│   └── icon.png
├── src/
│   ├── App.vue
│   ├── main.js
│   ├── assets/
│   └── components/

````

---

### 📁 public 디렉토리

- import 없이 직접 경로로 참조해야 하는 정적 파일 저장
- 브라우저가 직접 접근 (`/logo.png`)
- Vue가 빌드 처리하지 않음

#### ✅ 사용 예
- `favicon.ico`, `robots.txt`, `manifest.json`
- `og:image` 이미지, `index.html`에서 쓰는 이미지 등

#### ✅ 사용 이유
- HTML/메타 태그 등 Vue가 개입하지 않는 곳에서 사용
- 경로 유지 필요
- 외부 리소스 참조

---

### 📁 src/assets 디렉토리

- 컴포넌트 내부에서 `import` 해서 사용하는 정적 자원
- Webpack/Vite가 최적화 (압축, 해시 등)

#### ✅ 사용 예
- 버튼 아이콘
- 컴포넌트에서 쓰는 이미지, 폰트, 스타일 등

---

### ✅ public vs src/assets 정리표

| 구분            | public/                   | src/assets/                          |
| --------------- | ------------------------- | ------------------------------------ |
| Vue가 관리?     | ❌ 아님 (Vue 바깥)        | ✅ 맞음 (Vue가 import해서 관리)      |
| 빌드 처리됨?    | ❌ 복사만 됨              | ✅ Webpack/Vite가 최적화             |
| 접근 방법       | `/파일이름` 직접 경로     | `import img from '@/assets/img.png'` |
| 사용 위치       | Vue 외부 (index.html 등)  | Vue 컴포넌트 내부                    |
| 파일명 처리     | 이름 그대로 유지됨        | 해시 처리됨 (`logo.abc123.png`)      |

---

## ❓ 자주 헷갈리는 질문

### Q. 왜 정적 파일을 나눠요?
- Vue에서 다뤄야 하면 `src/assets`,  
  직접 접근만 할 거면 `public/`에 둬야 함

### Q. 다 `src/assets`에 두면 안 돼?
- `index.html`이나 메타 태그 등에서는 `import` 못 씀  
  → 그래서 `public/` 필요

---

## 📁 src/components

- Vue 컴포넌트 파일들이 위치하는 디렉토리
- 예: `Header.vue`, `MovieList.vue`, `Footer.vue` 등

---

## 📁 src/App.vue

- **Vue 앱의 루트 컴포넌트**
- 모든 하위 컴포넌트 포함
- 앱 전체의 레이아웃과 공통 UI 구성 정의

---

## 📁 src/main.js

- Vue 앱의 **시작점 / 진입 파일**
- `App.vue`를 `index.html`의 `<div id="app">`에 마운트
- 전역 설정 및 라이브러리 import

```js
import { createApp } from 'vue'
import App from './App.vue'

createApp(App).mount('#app')
````

---

## 📄 index.html

* 앱의 HTML 기본 골격
* 실제로는 하나의 HTML 페이지 (SPA 구조)
* `main.js`에서 Vue 앱이 마운트됨
* 외부 리소스 로딩 가능 (ex: Bootstrap CDN)

---

## 📄 package.json

* 프로젝트 정보, 스크립트, 의존성 정보 관리
* 개발자가 직접 관리하는 “설계도”

---

## 📄 package-lock.json

* 실제 설치된 패키지들의 정확한 버전 기록
* 프로젝트를 다른 곳에서 재현할 수 있게 보장함

---

## 📁 node\_modules

* 실제 설치된 모든 패키지가 저장되는 폴더
* 자동 생성되며, 버전별 라이브러리 포함

---

## ⚙️ Composition API vs Option API

### ▶ Composition API

* Vue 3에서의 권장 방식
* `import`한 함수들(`ref`, `computed`, `onMounted` 등)을 활용해 로직 정의

### ▶ Option API

* Vue 2에서 사용되던 방식
* `data`, `methods`, `mounted` 등의 속성으로 정의

---

## 🎨 `style scoped` 속성

* 해당 컴포넌트 안에만 스타일을 적용하도록 **범위를 제한**
* 전역 스타일 오염을 막을 수 있음
* 사용하지 않으면 모든 컴포넌트에 적용될 수 있음 (전역)

---
