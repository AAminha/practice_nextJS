## 모든 오류 처리, error.tsx

- `error.tsx` 파일은 예상치 못한 오류에 대한 포괄적인 역할을 하며, 사용자에게 대체 UI를 표시할 수 있음.
- 클라이언트 컴포넌트여야 함. `'use client';`
- props 종류
  - `error`: JS 기본 Error 개체의 인스턴스
  - `reset`: error boundary를 재설정하는 기능. 실행되면 경로 세그먼트를 다시 렌더링 시도

## 404 오류 처리, not-found.tsx

- 존재하지 않는 리소스를 가져오려고 할 때 사용할 수 있음.
- 리소스가 없는 경우 `notFound()`를 호출하면 `not-found.tsx`로 이동함.

```ts
import { notFound } from 'next/navigation';

if (!invoice) {
  notFound();
}
```
