## URL 검색 매개변수

- 검색 상태 관리
- 장점
  - 북마크 및 공유: 검색 매개변수가 URL에 있으므로 사용자는 검색 쿼리 및 필터를 포함하여 애플리케이션의 현재 상태를 북마크 할 수 있음. 이를 이용해 사용자는 특정 상태로 쉽게 돌아가거나 공유할 수 있음.
  - SSR 및 초기 로드: URL 매개변수를 서버에서 직접 사용하여 초기 상태를 렌더링할 수 있음. 이는 SSR을 처리하기 쉽게 하고 초기 로드 성능을 향상시킴.
  - 분석 및 추적: 검색 쿼리와 필터가 URL에 직접 포함되어 있어 추가적인 클라이언트 측 로직없이 사용자 행동을 추적하기 더 쉬움.

## 쿼리 매개변수 가져오는 방식

- 서버 컴포넌트와 클라이언트 컴포넌트의 쿼리 매개변수를 가져오는 방식이 다름.
- 서버 컴포넌트: 쿼리 매개변수가 자동으로 props로 전달됨.
- 클라이언트 컴포넌트: 직접 `useSearchParams`훅을 사용함.

## 디바운스 사용

- 아니까 패스!

### 디바운스 사용하면서 page query 사용하는 방법

```ts
const searchParams = useSearchParams();
const pathname = usePathname();
const { replace } = useRouter();

  // 사용자가 입력을 중지한 후 300ms가 지나면 검색 시작
const handleSearch = useDebouncedCallback((term) => {
  const params = new URLSearchParams(searchParams);
  params.set('page', '1');
  if (term) {
    params.set('query', term);
  } else {
    params.delete('query');
  }
  replace(`${pathname}?${params.toString()}`);
}, 300);

return (
  ...
  <input
    className="peer block w-full rounded-md border border-gray-200 py-[9px] pl-10 text-sm outline-2 placeholder:text-gray-500"
    placeholder={placeholder}
    onChange={(e) => {
      handleSearch(e.target.value);
    }}
    defaultValue={searchParams.get('query')?.toString()}
  />
  ...
  );
```
