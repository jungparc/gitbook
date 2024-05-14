# API Guide(Title)

알림을(Heading 1) 제목 1

&#x20;(Paragraphs) 해당 API에 대한 개요, 설명을 작성합니다.

### (Heading 2) 제목 2

(Paragraphs) 제목 2에 대한 개요, 설명을 작성합니다.

(Paragraphs) 설명을 이어 작성합니다.

### (Heading 2) API 사용 준비

OOO API를 사용하기 전 **API 사용 준비**를 참고하여 API 사용에 필요한 정보를 준비합니다.

{% content-ref url="api.md" %}
[api.md](api.md)
{% endcontent-ref %}

## (Heading 1) 제목 1

### (Heading 2) 제목 2

제목 2(API)에 대한 설명을 작성합니다.

```
GET /v1/clusters
Accept: application/json
Content-Type: application/json
OpenStack-API-Version: container-infra latest
X-Auth-Token: {tokenId}
```

#### (Heading 3) 요청

제목 3에 대한 설명을 작성합니다.

| 이름      | 종류     | 형식     | 필수 | 설명    |
| ------- | ------ | ------ | -- | ----- |
| tokenId | Header | String | O  | 토큰 ID |

#### (Heading 3) 응답

| 이름         | 종류   | 형식     | 설명                     |
| ---------- | ---- | ------ | ---------------------- |
| uuid       | Body | UUID   | 클러스터 UUID              |
| name       | Body | String | 클러스터 이름                |
| flavor\_id | Body | UUID   | 기본 워커 노드의 인스턴스 타입 UUID |

(Paragraphs) 설명을 이어 작성합니다.

{% hint style="info" %}
**알림/알아두기 (Info Hint)**

참고 사항이나 추가 정보를 제공할 때 **알림** 힌트를 사용합니다.
{% endhint %}

(Paragraphs) 설명을 이어 작성합니다.



