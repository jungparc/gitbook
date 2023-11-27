## Application Service > Maps > 오류 코드

## API 오류 코드
|resultCode|	resultMessage|	설명|	비고|
|:---:|:---:|:---:|:---:|
|0|	|성공|	공통|
|100|Result Not Found|		결과 없음|	검색 전용|
|101|Argument Error|	파라미터 오류|	공통|
|102|Internal Server Error|서버 오류|	검색 전용|
|201|	Searching for Security| POI	보안시설물|	검색 전용|
|202|	Longitude/Latitude |경위도|	검색 전용|
|203|	Mobile Phone Number|휴대폰 전화번호|	검색 전용|
|204|	Invalid Query|기타 입력 범위 오류|	검색 전용
|205|	POI not in given Admin|결과 없음(지역 설정)|	검색 전용|
|206|	POI not in given Area|결과 없음(영역 설정)|	검색 전용|
|207|	POI not in given Category|결과 없음(분류 설정)|	검색 전용|
|208|	Neighbor Search Only|결과 없음(주변 검색만 입력)|	검색 전용|
|209|	Neighbor Search not Found|결과 없음(주변 + 키워드 검색 결과 없음)|	검색 전용|
|300|	AppKey Error|앱키 인증 오류	|공통|
|501|	Unknown Fail|실패(unknown)|탐색 전용|
|502|	Apply Smart Re-navigation|Smart재탐색 적용|탐색 전용|
|503|	Canceled navigation by user | 사용자에 의한 탐색 취소 |탐색 전용|
|504|	Error due to Checksum | 체크섬 오류 |탐색 전용|
|517|	Memory allocation failure | 메모리 할당 실패 |탐색 전용|
|518|	File open failure | 파일 열기 실패 |탐색 전용|
|519|	File read failure|파일 읽기 실패|탐색 전용|
|520|	File write failure|파일 쓰기 실패|탐색 전용|
|521|	Socket connection failure |소켓 연결 실패|탐색 전용|
|532|	Request parameter is invalid | 요청 파라미터가 유효하지 않음 |탐색 전용|
|533|	The starting point is not selected, or the wrong starting point |출발지가 선택되지 않았거나, 잘못된 출발지|탐색 전용|
|534|	Destination is not selected or wrong destination |목적지가 선택되지 않았거나, 잘못된 목적지 |탐색 전용|
|535|	Wrong stopover |잘못된 경유지|탐색 전용|
|536|	Link Projection failure | Link Projection |탐색 전용|
|537|	Exceeding the navigational distance (1000km, walking navigation: 20km) | 탐색 가능 거리 초과(1000km, 도보 탐색 : 20km) |탐색 전용|
|538|	Exceeds the number of expandable nodes | 확장 가능 노드 수 초과 |탐색 전용|
|539|	Expansion failure | 확장 실패 |탐색 전용|
|540|	Expansion failure due to inactivity or traffic control | 특별한 사정이나 교통 통제로 인한 확장 실패 |탐색 전용|
|541|	Expansion failure due to vehicle height/weight restrictions near the starting point | 출발지 근처의 차량 높이/중량 제한으로 확장 실패 |탐색 전용|
|542|	Expansion failed due to a part-time curfew near the departure point | 출발지 근처의 시간제 통행금지로 인해 확장 실패 |탐색 전용|
|543|	The destination is a physical island road, and there are no established ferry routes. | 목적지가 물리적 섬도로이며, 구축된 페리 항로가 없음 |탐색 전용|
|544|	The departure or destination is a logical (transportation) island, and there are more than one destination |출발 또는 목적지가 논리적(교통) 섬이며, 목적지가 2개 이상인 경우 |탐색 전용|
|545| No data requested | 요청한 데이터가 없음 |탐색 전용|
