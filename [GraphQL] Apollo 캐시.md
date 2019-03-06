

Cash
=
Apollo GraphQL 클라이언트를 사용하면 응답을 캐시 할 수 있으므로 오프라인 상태에서도 사용하기 적합합니다. 클라이언트는 3 단계의 캐싱으로 구성 될 수 있습니다.

-   **HTTP 응답 캐시** : http 응답을 캐싱합니다.
-   **정규화 된 디스크 캐시** : 노드에서 응답을 SQL로 캐싱합니다. 디스크에서 정규화 된 응답을 유지하므로 프로세스가 종료 된 후에도 사용할 수 있습니다.
-   **Normalized InMemory Cache** : App / Process가 아직 살아있는 한 메모리 캐싱을 위해 최적화 된 Guava 메모리 캐시.

HTTP 응답 캐시
=
**중요 :** 캐싱은 `query`작업 에만 제공됩니다 . `mutation`조작 에는 사용할 수 없습니다 .

사용 가능한 캐시 정책에는 4 가지가 있습니다 `HttpCachePolicy`.

-   `CACHE_ONLY`- 네트워크를 무시하고 캐시에서만 응답을 가져옵니다. 캐시 된 응답이 없거나 만기 된 경우, 오류를 리턴합니다.
-   `NETWORK_ONLY` - 캐시 된 응답을 무시하고 네트워크에서 응답 만 가져옵니다.
-   `CACHE_FIRST`- 먼저 캐시에서 응답을 가져옵니다. 응답이 없거나 만료 된 경우 네트워크에서 응답을 가져옵니다.
-   `NETWORK_FIRST`- 먼저 네트워크에서 응답을 가져옵니다. 네트워크가 실패하고 캐시 된 응답이 만료되지 않은 경우 캐시 된 데이터를 반환합니다.
-   `CACHE_AND_NETWORK` - 캐시와 네트워크에서 응답을 가져옵니다.

또한, 타임 아웃을 정의 할 수 있습니다 `expireAfter(expireTimeout, timeUnit)`



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExOTAwODM4MSwxMDg0MDg1OTA1XX0=
-->