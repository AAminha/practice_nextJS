## 웹 접근성

- 접근성이란 장애가 있는 사용자를 포함하여 모든 사람이 사용할 수 있는 웹 애플리케이션을 설계하고 구현하는 것을 의미함.
- 키보드 탐색, 의미론적 HTML, 이미지, 색상, 비디오 등과 같은 많은 영역을 다루는 광범위한 주제.
- `eslint-plugin-jsx-ally`: 접근성 문제를 조기에 발견하는데 도움이 되는 플러그인으로, Next.js에 기본적으로 포함됨.
  - 예시: alt 텍스트가 없는 이미지가 있는 경우 / `aria-*` 혹은 `role` 속성을 잘못 사용하는 경우 등 경고

## form 접근성 개선

- 시맨틱 HTML 사용: `<div>`대신 `<input>`이나 `<option>`같이 시맨틱 태그를 사용하면 AT(assistive technologies, 보조 기술) 입력 요소에 집중하고 사용자에게 적절한 상황 정보를 제공하여 양식을 더 쉽게 탐색하고 이해할 수 있게 할 수 있음.
- 라벨링: `<label>` 혹은 `<htmlFor>` 속성을 포함하면 각 양식 필드에 설명 텍스트 레이블이 포함되며, 이는 컨텍스트를 제공하여 AT 지원을 향상시키고 사용자가 레이블을 클릭하여 해당 입력 필드에 집중할 수 있게 함으로써 유용성을 향상시킴.
- focus 아웃라인: 입력 필드에 focus가 잡히면 아웃라인을 표시하도록 필드의 스타일이 적절하게 지정됨. 이는 페이지의 활성 요소를 시각적으로 표시하여 키보드와 화면 판독기 사용자 모두가 양식의 위치를 이해하는데 도움이 되므로 접근성에 매우 중요함.

## 검증

- 클라이언트 측 유효성 검사
  - 필수 입력을 위해 `required` 속성 추가
- 서버 측 유효성 검사
