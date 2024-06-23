## NextAuth.js

- 애플리케이션에 인증을 추가하기 위해 사용
- 세션 관리, 로그인 및 로그아웃, 인증의 다른 측면들을 관리하는 복잡성을 많이 숨겨줌.
  - 해당 기능들은 수동으로 구현 가능하나, 시간이 많이 걸리고 오류가 발생할 수 있음.
  - NextAuth.js는 해당 과정을 간소화하여 Next.js 애플리케이션에서의 인증에 대한 통일된 솔루션을 제공함.

### 설정

1. NextAuth.js 설치

```
npm install next-auth@beta
```

2. 애플리케이션을 위한 비밀키 생성

```
openssl rand -base64 32
```

3. .env 파일에 생성된 키 추가

```
AUTH_SECRET=your-secret-key
```

4. 페이지 옵션 추가

- 루트에 `auth.config.ts` 파일을 생성
  - `signIn: '/login'`을 `pages` 옵션에 추가함으로써 사용자는 NextAuth.js의 기본 페이지 대신, 사용자 지정 로그인 페이지로 리다이렉션

```ts
// /auth.config.ts
import type { NextAuthConfig } from 'next-auth';

export const authConfig = {
  pages: {
    signIn: '/login',
  },
};
```

5. 미들웨어 파일 생성

- `authConfig` 객체를 사용하여 NextAuth.js 초기화 & `auth` 속성 내보냄
- `matcher` 옵션을 사용하여 특정 경로에서 실행되도록 지정
- 보호된 라우트가 미들웨어가 인증을 확인하기 전에 렌더링되지 않음. 이는 애플리케이션의 보안과 성능을 향상시킴.

```ts
// /middleware.ts
import NextAuth from 'next-auth';
import { authConfig } from './auth.config';

export default NextAuth(authConfig).auth;

export const config = {
  // https://nextjs.org/docs/app/building-your-application/routing/middleware#matcher
  matcher: ['/((?!api|_next/static|_next/image|.*\\.png$).*)'],
};
```

### Next.js 미들웨어를 사용하여 라우트 보호

```ts
// /auth.config.ts
import type { NextAuthConfig } from 'next-auth';

export const authConfig = {
  pages: {
    signIn: '/login',
  },
  callbacks: {
    authorized({ auth, request: { nextUrl } }) {
      const isLoggedIn = !!auth?.user;
      const isOnDashboard = nextUrl.pathname.startsWith('/dashboard');
      if (isOnDashboard) {
        if (isLoggedIn) return true;
        return false; // Redirect unauthenticated users to login page
      } else if (isLoggedIn) {
        return Response.redirect(new URL('/dashboard', nextUrl));
      }
      return true;
    },
  },
  providers: [], // Add providers with an empty array for now
} satisfies NextAuthConfig;
```

- 사용자가 로그인하지 않은 경우 대시보드 페이지에 액세스할 수 없음.
- `authorized` 콜백: Next.js 미들웨어를 통해 페이지에 액세스할 권한이 있는지 확인하는 데 사용됨.
  - 요청이 완료되기 전 호출되며, `auth` 및 `request` 속성을 포함하는 객체를 받음
  - `auth` 속성에는 사용자 세션이 포함됨
  - `request` 속성에는 들어오는 요청이 포함됨
- `providers` 옵션: 다른 로그인 옵션을 나열하는 배열

## 비밀번호 해싱

- 데이터베이스에 비밀번호를 저장하기 전에 해싱하는 것이 좋음.
  - 해싱: 비밀번호를 길이가 고정된 문자열로 변환하여 무작위로 보이게 만듦.
  - 사용자 데이터가 노출되더라도 보안 계층을 제공함.
- `bcrypt` 패키지를 사용하여 해싱할 수 있으며, 사용자가 입력한 비밀번호가 데이터베이스의 비밀번호와 일치하는지 확인하기 위해 다시 사용할 예정
  - `bcrypt` 패키지는 Next.js 미들웨어에 사용할 수 없는 Node.js API에 의존하기 때문에 별도의 파일을 만들어야 함.
