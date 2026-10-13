# Canyon Finder — 캐년 투어 가격 비교

한국어 정적 웹사이트 + Vercel Serverless API 프로젝트입니다.

## 포함 파일
- `index.html`: 검색 화면과 정렬/계산 기능
- `api/tours.js`: 투어 후보 10개와 원본 링크를 반환하는 API
- `vercel.json`: Vercel 설정

## 중요한 가격 안내
현재 포함된 후보는 가격과 후기 점수를 실시간으로 제공하는 공식 API 연결이 확인되지 않았습니다. 따라서 가격과 평점/후기 수는 `null`로 설정하고, 사이트에서 실제 가격인 것처럼 꾸며 표시하지 않습니다. 원본 사이트 링크에서 가격, 여행 날짜, 불포함 비용, 후기 정보를 확인할 수 있습니다.

API 또는 제휴 데이터 공급자가 제공하는 합법적인 가격 데이터가 확보되면 `api/tours.js`에서 해당 공급자의 공식 API를 서버 측으로 연결하세요. API 키가 생기면 브라우저 코드에 넣지 말고 Vercel의 Project Settings → Environment Variables에 저장하세요.

## GitHub에 올리는 방법
1. GitHub에서 새 저장소를 만듭니다. 예: `canyon-price-finder`
2. 이 ZIP을 컴퓨터에 풀어 파일/폴더를 저장소 최상위에 업로드합니다.
3. `index.html`, `api` 폴더, `vercel.json`이 저장소 첫 화면에 보여야 합니다.
4. Commit changes를 누릅니다.

## Vercel 배포 방법
1. Vercel에 로그인하고 Add New → Project를 누릅니다.
2. 방금 만든 GitHub 저장소를 Import합니다.
3. Framework Preset은 Other로 둡니다.
4. Build Command와 Output Directory는 비워두고 Deploy를 누릅니다.
5. 배포가 끝나면 사이트 주소 뒤에 `/api/tours`를 붙여 JSON이 열리는지 확인합니다.

## 가격과 후기 정보 수정
`api/tours.js`의 각 상품 객체에서 `price`, `originalPrice`, `rating`, `reviews`를 수정할 수 있습니다.
- 가격을 확인하지 못했다면 `price: null` 그대로 둡니다.
- `price`와 `originalPrice`는 `currency`에 적힌 통화 단위로 입력합니다.
- `rating`은 5점 만점, `reviews`는 해당 상품/판매자 후기 수입니다.
- 후기 정보가 판매자 평점인지 상품별 평점인지 `conditions`에 명확히 적으세요.
- 가격이 실제로 확인된 시각이 있다면 `updatedAt` 필드를 상품 객체에 추가할 수 있도록 코드에 확장하세요. 현재 응답의 `updatedAt`은 API 응답 시각이며 각 여행사의 가격 갱신 시각이 아닙니다.

## 현재 구현된 기능
- 날짜 입력 UI, 인원 선택
- 추가 비용 입력 및 1인/그룹 예상 금액 계산
- 환율 수동 입력
- 가격순, 추천순, 평점순, 후기 수순, 할인율순 정렬
- 후보 10개와 원본 예약 링크
- 모바일 대응
- 가격 미확인 상품에 대한 명확한 안내

## 현재 구현되지 않은 기능
- 여행사 사이트의 실시간 가격/날짜별 재고 자동 조회
- 후기 점수의 자동 동기화
- 실제 예약/결제
- 가격이 확인되지 않은 상품의 최저가 계산

이 기능들은 각 사이트의 공식 API 또는 사용 허가가 있는 데이터 공급원과 연결해야 합니다.
