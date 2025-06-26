# Cache

- 웹 캐시: 자주 쓰이는 문서의 사본을 자동으로 보관하는 HTTP 장치
  캐시는 불필요한 데이터 전송을 줄임(비용 감소)
  네트워크 병목 줄임 (대역폭 병목 감소)
  원 서버에 대한 요청 줄임(부하 줄임)
  거리로 인한 지연 감소

![](https://static.toss.im/ipd-tcs/toss_core/live/f33c6cc3-3be0-4db2-a687-e53fcf06e6d6/Untitled.png)

캐시를 이용하면, 첫 번째 서버 응답은 캐시에 보관되고, 캐시된 사본이 뒤이은 요청들에 대한 응답으로 사용됨.

- 캐시 적중(cache hit)과 캐시 부적중(cache miss)
  : 대응하는 캐시 사본이 있다면 이를 이용하여 요청을 처리하고, 대응하는 사본이 없다면 원 서버로 전달됨

- 재검사(Recalidation)
  : 캐시 사본이 여전히 최신인지 서버를 통해 신선도를 검사하는 과정
  전체 데이터를 가져오지 않고도 신선도 검사 가능
  qqq
  ![](https://www.keycdn.com/img/support/if-modified-since.png)
  [캐시 재검사를 위해 사용되는 HTTP 조건부 요청 헤더]
  If-Modified-Since 헤더로 캐시된 시간 이후 변경되었을 경우에만 보내달라고 요청 가능
- 재검사 부적중(200 OK) / 재검사 적중(304 Not Modified)  
  If-None-Match: 마지막 변경된 날짜를 맞춰보는 대신, 특별한 태그(버전)가 다를 때만 요청 처리

걸리는 속도 :(빠름) 캐시 적중 < 재검사(원 서버랑 검사함) < 캐시 부적중(서버로부터 객체 데이터를 받아옴) (느림)

- 개인 전용 캐시: 한 명에게만 할당된 캐시
  - 작고 저렴
  - 대부분의 브라우저는 자주 쓰이는 문서를 개인용 컴퓨터의 디스크와 메모리에 저장함
- 공용 캐시: 사용자 집단에게 자주 쓰이는 페이지(프락시 서버)

- 캐시망

- 캐시 처리 단계

![](https://blog.kakaocdn.net/dn/bjhTnJ/btsH9W1e8bh/KL7jC1YvQjECtKEbAjFkkK/img.png)
![](https://blog.kakaocdn.net/dn/ukAN8/btrJrQAozEe/nLg2Kb0SQaoa8QGhiNmRA1/img.png)

- 캐시 제어
  : HTTP 는 문서가 만료되기 전까지 얼마나 오랫동안 캐시될 수 있게 할 것인지 서버가 설정할 수 있는 여러 가지 방법을 정의함

![](https://cdn.inflearn.com/public/files/posts/741ad8ff-2310-4e05-9a7a-da6ed5759b44/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-12-28%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%204.48.54.png)

- Cache-Control: no-cache
  : 캐시가 그 응답의 사본을 만드는 것을 금지함.

데이터는 캐시해도 되지만 항상 원 서버에 검증하고 사용해야 한다. (max-age=0 과 동일한 뜻)
즉, 서버로부터 304 응답을 받아야 캐시에서 가져온다는 말이다. 비록 네트워크 트래픽이 발생하지만 헤더 메세지만 응답 받기 때문에 네트워크 다운로드량은 적다.
no cache 라는 이름때문에 캐시를 사용안한다고 생각할 수 있는데, 이 단어의 의미는 본래 캐시 유효 기간이 남아있으면 무조건 캐시 저장소를 조회하지만 그리하지말고 무조건 서버에 검증 받으라는 말이다.

Cache-Control: no-store
:
(사실 로컬 캐시 저장소에 저장될 수 있으나, 서버와 재검사를 하지 않고서는 캐시에서 클라이언트로 제공될 수 없다. )

데이터에 민감한 정보가 있기에 저장하면 안된다는 의미
메모리에서 사용하고 최대한 빨리 삭제한다.

Cache-Control: must-revalidate
: 신선하지 않은 사본을 원 서버와의 최초 재검사 없이는 사용 금지
캐시 만료후 최초 조회시 원 서버에 검증해야 할때 설정
원 서버에 접근 실패시 반드시 504(Gateway Timeout) 오류가 발생해야 하도록 한다. 
만일 캐시 유효 시간 내에 있다면 캐시를 사용한다.

Cache-Control: Max-Age
Cache-Control: Expires

출처: https://inpa.tistory.com/entry/HTTP-🌐-웹-브라우저의-캐시-전략-Cache-Headers-다루기 [Inpa Dev 👨‍💻:티스토리]

# Next cache

기본적으로 Next.js는 성능을 향상시키고 비용을 절감하기 위해 가능한 한 많이 캐싱합니다.
![](https://h8dxkfmaphn8o0p3.public.blob.vercel-storage.com/docs/dark/caching-overview.png)

<!--
빌드타임의 캐시 동작

요청타임의 캐시 동작
-->
- RSC Payload는 서버에서 렌더링된 React 컴포넌트의 **"결과"** (구조화된 JSON 트리 상태)
  Next App router에서 클라이언트는 이전에 방문한 페이지에 대한 정보를 메모리에 캐싱해둠
- Full Route Cache: 서버에 저장되는 캐시 계층, 특정 url 경로에 대한 렌더링 결과 캐싱 (RSC Payload/HTML)


## Server Component의 도입으로 데이터 페칭의 방식에 변화가 일어났다!
![](https://velog.velcdn.com/images/skyoffly/post/cc73c988-4536-44da-8951-39a4ab818f0d/image.png)

데이터 페칭을 더 편하게 할 수 있는 것은 장점이지만, 문제는 동일한 요청이 여러 컴포넌트에서 발생하는 경우가 발생할 수 밖에 없다는 단점이 동시에 발현됨

Page Router에서는 Page에서 모든 데이터를 받아서 내려보내주면 그만이었지만, App Router에서는 각 컴포넌트에서 직접 데이터를 페칭할 수 있게 되었기 때문에 중복된 API 요청이 발생할 가능성이 대단히 높아짐

![](https://velog.velcdn.com/images/skyoffly/post/6f2c8342-6416-46cc-9f3f-47fa82dbfa87/image.png)
<!--
https://velog.io/@skyoffly/%ED%95%99%EC%8A%B5-Next.js-Day-15-App-Router-%EB%8D%B0%EC%9D%B4%ED%84%B0-%ED%8E%98%EC%B9%AD-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%BA%90%EC%8B%B1-Request-Memoization
-->


## Request Memoization

![](https://h8dxkfmaphn8o0p3.public.blob.vercel-storage.com/docs/dark/deduplicated-fetch-requests.png)
Next는 [fetch API](https://nextjs-ko.org/docs/app/api-reference/functions/fetch)를 확장하는데, 이는 React 컴포넌트 트리의 여러 곳에서 동일한 데이터를 가져오기 위한 fetch 함수를 호출할 때 한 번만 실행된다는 것을 의미한다.

예를 들어, 경로 전체에서 동일한 데이터를 사용해야 하는 경우(예: Layout, Page 및 여러 컴포넌트에서), 트리 상단에서 데이터를 가져와 컴포넌트 간에 props를 전달할 필요가 없다.
대신, 데이터를 필요로 하는 컴포넌트에서 데이터를 가져와 네트워크를 통해 동일한 데이터에 대해 여러 요청을 하는 성능 문제를 걱정할 필요 없이 데이터를 가져올 수 있다.

```
async function getItem() {
  // `fetch` 함수는 자동으로 메모이제이션되고 결과는
  // 캐싱됩니다.
  const res = await fetch('https://.../item/1')
  return res.json()
}

// 이 함수는 두 번 호출되지만 처음에는 한 번만 실행됩니다.
const item = await getItem() // cache MISS

// 두 번째 호출은 경로 어디에서든 발생할 수 있습니다.
const item = await getItem() // cache HIT
```

- "같은 요청(=같은 서버 사이드 렌더링 컨텍스트)" 내에서만 유효
- 메모이제이션은 fetch 요청의 GET 메서드에만 적용되며, POST 및 DELETE와 같은 다른 메서드는 메모이제이션되지 않음. (이 기본 동작은 React 최적화이며 이를 선택 해제하는 것은 권장하지 않음)

![](https://nextjs.org/_next/image?url=https%3A%2F%2Fh8DxKfmAPhn8O0p3.public.blob.vercel-storage.com%2Fdocs%2Fdark%2Frequest-memoization.png&w=3840&q=75)

## data cache

우리가 일반적으로 생각할 수 있는 API 캐싱입니다.

```
// Revalidate at most every hour
fetch('https://...', { next: { revalidate: 3600 } })
```

Next.js가 확장해놓은 fetch 함수에 next.revalidate 옵션을 넘기면 Data Cache가 동작한다.
성공적으로 데이터를 가져왔다면 그 응답값을 저장해두었다가 동일한 경로로 fetch 함수를 실행할 때 실제 API 호출은 건너뛰고 저장해놓은 응답값을 반환.

![](https://velog.velcdn.com/images/skyoffly/post/946906f9-342c-46f4-8862-56f32a7898ea/image.png)

하나의 요청 동안만 유효한 Request Memoization과 다르게 Data Cache는 일정 시간 동안에 웹 서버로 들어오는 모든 요청에 대해 동작한다.
만약 next.revalidate를 1초로 설정했다면, 1초에 1000명의 사용자가 접속해도 실제 API 요청은 1회 전송

### 재검증 Revalidating

- 시간 기반 재검증: 일정 시간이 경과한 후 새 요청이 있을 때 데이터를 재검증. 이는 데이터가 자주 변경되지 않고 신선도가 그리 중요하지 않은 경우에 유용.
- 온디맨드 재검증: 이벤트(예: 폼 제출)에 따라 데이터를 재검증. 온디맨드 재검증은 태그 기반 또는 경로 기반 접근 방식을 사용하여 데이터를 한 번에 재검증할 수 있다.

## Full Route Cache

Next.js는 빌드 타임에 데이터 호출, 캐싱 등의 작업을 마치고 페이지의 생성 결과를 풀 라우트 캐시Full Route Cache에 저장하게 된다.
실제 접속 요청이 들어오게 되면,풀 라우트 캐시Full Route Cache에 저장된 생성 결과를 HIT해준다. (미리 완성된 결과를 반환해준다는 면에서 SSG와 결과가 흡사하다.)


웹 서버의 성능을 눈에 띄게 향상시키려면 Full Route Cache를 적용해야 한다. 서버 렌더링 과정에서 웹 서버의 리소스(특히 CPU)를 대부분 사용하게 되는데, Full Route Cache는 서버 렌더링 결과를 재사용함으로써 이를 줄일 수 있다.

![](https://velog.velcdn.com/images/skyoffly/post/764c810f-22d1-48ce-9096-67d52659bb9c/image.png)
![](https://h8dxkfmaphn8o0p3.public.blob.vercel-storage.com/docs/dark/full-route-cache.png)

<!--
### Subsequent Navigations

후속 탐색 또는 프리페치 중에 Next.js는 React Server Components Payload가 Router Cache에 저장되어 있는지 확인 후, 있다면 서버에 새 요청을 보내는 것을 건너뛴다.

경로 세그먼트가 캐시에 없으면 Next.js는 서버에서 React Server Components Payload를 가져와 클라이언트의 Router Cache를 채운다.
-->
## Next App의 페이지들의 정적/동적 구분

![](https://h8dxkfmaphn8o0p3.public.blob.vercel-storage.com/docs/dark/static-and-dynamic-routes.png)
![](https://velog.velcdn.com/images/skyoffly/post/e17466cc-2317-4d3a-93b4-1b47f95ea5b6/image.png)
경로가 빌드 시 캐시되는지 여부는 정적으로 렌더링되는지 동적으로 렌더링되는지에 따라 다르다. 정적 경로는 기본적으로 캐시되지만, 동적 경로는 요청 시 렌더링되며 캐시되지 않는다.

=> Full Route Cache는 정적 페이지에서만 동작한다.

## Client-side Router Cache

Next.js의 Client-side Router Cache는 경로 세그먼트(Route Segment)의 RSC 데이터를 클라이언트 메모리에 저장하여 성능을 최적화하는 기능이다.

사용자가 네비게이션할 때, Next.js는 방문한 경로 세그먼트를 캐싱하고 사용자가 이동할 가능성이 높은 경로를 미리 가져온다.

- 즉각적인 뒤로/앞으로 탐색 (Instant Back/Forward Navigation)
- 네비게이션 시 전체 페이지 새로고침 방지
- React 및 브라우저 상태 유지

# Cache Interactions

- Data Cache와 Full Route Cache
  Data Cache를 재검증하거나 옵트아웃하면 Full Route Cache가 무효화된다. 이는 렌더링 출력이 데이터에 의존하기 때문.

# <Link>

기본적으로 <Link> 컴포넌트는 Full Route Cache에서 경로를 자동으로 프리페치하고 React Server Component Payload를 Router Cache에 추가합니다.

# React cache function

React cache 함수는 함수의 반환 값을 메모이제이션하여 동일한 함수를 여러 번 호출할 때 한 번만 실행되도록 합니다.

fetch 요청은 자동으로 메모이제이션되므로 React cache로 감쌀 필요가 없습니다.

```
import { cache } from 'react'
import db from '@/lib/db'

export const getItem = cache(async (id: string) => {
  const item = await db.item.findUnique({ id })
  return item
})
```

그래서 Next cache를 잘 알아두면 좋을까요?

그에 대한 대답은 공식문서에 있습니다.

> 알아두면 좋은 정보: 이 페이지는 Next.js의 내부 작동 방식을 이해하는 데 도움이 되지만, Next.js를 생산적으로 사용하는 데 필수적인 지식은 아닙니다. 대부분의 Next.js 캐싱 휴리스틱은 API 사용에 의해 결정되며, 최소한의 구성으로도 최상의 성능을 발휘하도록 기본값이 설정되어 있습니다.

<!-- # React cache -->
