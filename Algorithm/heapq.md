# heapq

### 🖌 heapq

우선순위 큐 알고리즘. 최댓값과 최솟값을 찾는 연산을 빠르게 하기 위해 사용한다.

- 최소 힙 : 부모 노드의 키값이 자식 노드의 키값보다 항상 작은 힙
- 최대 힙 : 부모 노드의 키값이 자식 노드의 키값보다 항상 큰 힙



```python
heapq.heappush(heap, item)
# heap 불변성 값을 유지하면서 item 값을 heap에 추가한다.

heapq.heappop(heap)
# heap 불변성을 유지하면서, heap에서 가장 작은 항목을 팝하고 반환합니다.

heapq.heappushpop(heap, item)
# heap에 item을 푸시한 다음, heap에서 가장 작은 항목을 팝하고 반환합니다. 

heapq.heapify(x)
# 리스트 x를 선형 시간으로 제자리에서 heap으로 변환합니다.

```

</br>

예시

```python
import heapq

heap = []
heapq.heappush(heap, 60)
heapq.heappush(heap, 10)
heapq.heappush(heap, 20)

print(heap) // [10, 60, 20]
```

