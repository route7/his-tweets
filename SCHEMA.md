# 필드 정의

대한민국 대통령 이재명(@Jaemyung_Lee)의 공개 X 게시물 아카이브입니다. 취임일 2025-06-04 이후 수집된 게시물의 원문 텍스트와 수집 시점의 공개 지표를 담습니다. 지표(좋아요·재게시·답글·조회)는 확정값이 아니라 metrics.observed_at 시점의 관측값이며, 이후 계속 변합니다. 일반인 계정 보호를 위해 공적 계정을 제외한 모든 멘션은 '@[비공개]'로 마스킹되어 있습니다. 분야 분류(category)는 키워드 규칙과 사람의 검토를 결합한 결과이며 편집상의 판단이 포함됩니다. classification.needs_review 가 true 인 항목은 아직 검토 대기 상태이므로 통계에 인용할 때 유의하십시오. 원본의 시각적 표현은 재현하지 않으며 각 항목의 url 이 정본입니다. 비영리 기록 목적으로 제작되었고 대통령실·정부·X Corp.과 무관합니다.

| 필드 | 설명 |
|---|---|
| `tweet_id` | 게시물 고유 ID (문자열. 정수로 파싱하면 정밀도가 손실된다) |
| `published_at_utc` | 게시 시각, ISO 8601 UTC |
| `published_at_kst` | 게시 시각, 한국 표준시(UTC+9) 사람이 읽는 형식 |
| `text` | 게시물 원문. 공적 계정 외 멘션은 '@[비공개]'로 마스킹됨 |
| `text_complete` | false 이면 본문이 잘려 있다(웹 검색 시드). 전문은 url 에서 확인할 것 |
| `language` | 게시물 언어 코드 |
| `category` | 분야 코드 |
| `category_label` | 분야 이름(한국어) |
| `classification` | 분류 근거 — method(rule|llm|human), confidence(0~1), needs_review |
| `post_type` | original(직접 작성) | reply(답글) | retweet(리트윗) | quote(인용) |
| `metrics` | 관측 지표 — like_count, retweet_count, reply_count, quote_count, view_count, observed_at. view_count 는 null 일 수 있다 |
| `hashtags` | 해시태그 목록(# 제외) |
| `mentions` | 허용목록에 등재된 공적 계정 멘션만 남는다 |
| `masked_mention_count` | 마스킹된 멘션 개수 |
| `media_count` | 첨부 미디어 개수 (원본 파일은 보관하지 않음) |
| `url` | 원본 게시물 영구 링크 |
| `url_resolves` | false 이면 대응하는 실제 게시물이 없다(합성 샘플). 링크를 따라가지 말 것 |
| `related` | 이 게시물과 연결된 자료 목록. type: news(보도) | speech(연설문) | briefing(정책브리핑) | mirror(대통령실이 보관한 같은 메시지의 공식 사본) | doc. mirror 는 독립적 근거가 아니라 동일 내용의 사본임에 유의 |

## 분야 코드

| 코드 | 이름 |
|---|---|
| `politics` | 정치·국정 |
| `diplomacy` | 외교·통상 |
| `defense` | 국방·안보 |
| `economy` | 경제·민생 |
| `society` | 사회 |
| `safety` | 재난·안전 |
| `tech` | 과학기술·AI |
| `culture` | 문화·체육 |
| `greeting` | 일상·인사 |
| `unclassified` | 미분류 |

## 주의

- `tweet_id` 는 64비트를 넘는 값이므로 **반드시 문자열로 다룰 것**. JavaScript 의 `JSON.parse` 는 정밀도를 잃지 않지만 정수로 변환하면 손실된다.
- `view_count` 는 게시물에 따라 제공되지 않는다. `null` 을 0 으로 치환하지 말 것.
- 모든 지표는 `observed_at` 시점의 관측값이다. 서로 다른 시점의 값을 비교할 때 주의.
- 통계는 `post_type == "original"` 만으로 내는 것을 기본으로 한다.