---
layout: post-old
title: 서버 응답 시간(TTFB) 단축
description: |2-

  '첫 번째 바이트까지의 시간(TTFB)' 감사에 대해 알아봅니다.
date: 2019-05-02
updated: 2019-10-04
web_lighthouse:
  - 첫 번째 바이트까지의 시간(TTFB)
---

Lighthouse 보고서의 '기회' 섹션은 사용자 브라우저가 페이지 콘텐츠의 첫 번째 바이트를 수신하는 데 걸리는 시간인 '첫 번째 바이트까지의 시간'을 보고합니다.

<figure class="w-figure">   {% Img src="image/tcFciHGuF3MxnTr1y5ue01OGLBn2/V0P3MeqXSwGIL7fJbBRj.png", alt="Lighthouse Server 응답 시간이 짧음(TTFB) 감사의 스크린샷", width="800", height="95", class="w-screenshot" %}</figure>

## 느린 서버 응답 시간이 성능에 영향을 미침

이 감사는 브라우저에서 서버가 기본 문서 요청에 응답할 때까지 600ms 이상 대기하면 실패합니다. 사용자는 페이지 로드 시간이 오래 걸리는 것을 싫어합니다. 느린 서버 응답 시간은 페이지 로드가 오래 걸리는 가능한 원인 중 하나입니다.

사용자가 웹 브라우저에서 URL로 이동할 때 브라우저는 해당 콘텐츠를 가져오기 위해 네트워크 요청을 보냅니다. 그러면 서버가 요청을 수신하고 페이지 콘텐츠를 반환합니다.

서버는 사용자가 원하는 모든 콘텐츠가 포함된 페이지를 반환하기 위해 많은 작업을 수행해야 할 수 있습니다. 예를 들어 사용자가 주문 내역을 보고 있는 경우 서버는 데이터베이스에서 각 사용자의 내역을 가져온 다음 해당 콘텐츠를 페이지에 삽입해야 합니다.

이와 같은 작업을 가능한 한 빨리 수행하도록 서버를 최적화하는 것이 사용자가 페이지 로드에 대기하는 시간을 줄이는 한 가지 방법입니다.

## 서버 응답 시간을 개선하는 방법

서버 응답 시간을 개선하는 첫 번째 단계는 페이지 콘텐츠를 반환하기 위해 서버가 완료해야 하는 핵심 개념 작업을 식별한 다음, 이러한 각 작업에 걸리는 시간을 측정하는 것입니다. 가장 긴 작업을 찾았으면 작업 속도를 높일 방법을 찾아야 합니다.

서버 응답이 느린 가능한 원인은 다양하므로 개선할 수 있는 방법도 다양합니다.

- 서버의 애플리케이션 로직을 최적화하여 페이지를 더 빨리 준비시킵니다. 서버 프레임워크를 사용하는 경우 프레임워크에 이를 수행하는 방법에 대한 권장 사항이 있을 수 있습니다.
- 서버가 데이터베이스를 쿼리하는 방식을 최적화하거나 더 빠른 데이터베이스 시스템으로 마이그레이션합니다.
- 서버 하드웨어를 업그레이드하여 메모리 또는 CPU 사양을 높입니다.

## 스택별 지침

### Drupal

테마, 모듈 및 서버 사양 모두가 서버 응답 시간에 영향을 미칩니다. 더 최적화된 테마를 찾거나 최적화 모듈을 신중하게 선택하거나 서버를 업그레이드하는 방법을 고려하세요. 호스팅 서버는 PHP opcode 캐싱, memcached 또는 Redis와 같은 메모리 캐싱 시스템을 사용하여 데이터베이스 쿼리 시간을 줄이고 최적화된 애플리케이션 로직을 사용하여 페이지를 더 빠르게 준비시켜야 합니다.

### Magento

Magento의 [Varnish 통합](https://devdocs.magento.com/guides/v2.3/config-guide/varnish/config-varnish.html)을 사용합니다.

### React

서버 측에서 React 구성 요소를 렌더링하는 경우 [`renderToNodeStream()`](https://reactjs.org/docs/react-dom-server.html#rendertonodestream) 또는 `renderToStaticNodeStream()`을 사용하여 클라이언트가 한 번에 모두가 아니라 마크업의 여러 부분을 수신하고 수화할 수 있도록 하는 방법을 고려하세요.

### WordPress

테마, 플러그인 및 서버 사양 모두가 서버 응답 시간에 영향을 미칩니다. 더 최적화된 테마를 찾거나 최적화 플러그인을 신중하게 선택하거나 서버를 업그레이드하는 것을 고려하세요.

## 리소스

- [**서버 응답 시간(TTFB) 단축** 감사를 위한 소스 코드](https://github.com/GoogleChrome/lighthouse/blob/master/lighthouse-core/audits/server-response-time.js)
- [네트워크 정보 API를 사용한 적응형 서비스](/adaptive-serving-based-on-network-quality)
