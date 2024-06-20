## Server Action

- 서버에서 비동기 코드를 직접 실행할 수 있는 기능으로, API 엔드포인트 없이도 데이터 변경이 가능.
- 보안이 중요한 웹 애플리케이션에서 POST요청, 암호화된 클로저, 엄격한 입력 검사, 에러 메시지 해싱, 호스트 제한 등의 기술을 통해 데이터를 보호하고, 권한이 있는 접근만 허용하는 효과적인 보안 솔루션.
- form을 사용한 Server Action

  - 추가적인 API 엔드포인트 없이도 데이터를 안전하게 변경할 수 있음.
  - form 제출 시 action 속성에서 서버 액션이 호출되도록 함.
  - 이렇게 하면 클라이언트에서 JS가 비활성화(JS가 로드되지 않거나 로드 실패)되어 있더라도 form 제출이 가능하므로, 애플리케이션의 Progressive Enhancement가 이루어짐.

  ```ts
  // Server Component
  export default function Page() {
    // Action
    async function create(formData: FormData) {
      'use server';

      // Logic to mutate data...
    }

    // Invoke the action using the "action" attribute
    return <form action={create}>...</form>;
  }
  ```
