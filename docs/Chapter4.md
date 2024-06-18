## 중첩 라우팅

- Next.js는 파일 시스템 라우팅을 사용한다.
  - app 폴더 내에서 중첩 라우팅을 구현할 수 있다.
- `layout.tsx`: 각 경로에 대해 별도의 UI를 만들 수 있다.
- `page.tsx`: 특수 Next.js 파일이며 url 경로와 연결된 홈 페이지이다.

```
├─ ...
├─ app
│  ├─ lib/              // 재사용 가능한 유틸리티 함수를 모아두는 폴더
│  ├─ ui/               // UI 구성요소를 모아두는 폴더
│  ├─ dashboard/
│  │  ├─ customers/
│  │  │  ├─ page.tsx    // 대시보드 내 customers 페이지 파일
│  │  ├─ invoices/
│  │  │  ├─ page.tsx    // 대시보드 내 invoices 페이지 파일
│  │  ├─ layout.tsx     // 대시보드 페이지의 레이아웃 파일
│  │  ├─ page.tsx       // 대시보드 페이지 파일
│  ├─ layout.tsx        // 메인 페이지의 레이아웃 파일
│  ├─ page.tsx          // 메인 페이지 파일
```

## 부분 렌더링

- 탐색 시 페이지 구성 요소만 업데이트 되고 레이아웃은 다시 렌더링되지 않는 것
  - Next.js에서의 레이아웃 사용 시 장점
