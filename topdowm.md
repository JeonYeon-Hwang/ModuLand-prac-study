### 톱 다운 방식으로 이해하기  

**User flow**  
*예: 에셋 드래그 → 3D 공간에 최초 좌표 배치*  

드래그 시작  
`onDragStart 이벤트`.. `WebGL`의 "Canvas 영역"이 존재. 

Raycasting  
onDrop → `Raycaster(Three.js)`가 적용 2D → 3D로 좌표 계산.  
이건 가상의 레이저.. 바닥(Mesh)에 부딛히는 곳에 Object 생성.  

백엔드에서 연산  
(asset ID, coordinate)전송 → SQL에 적재  
더 정확히 표현하자면?  
Spring → FastAPI(기하학 연산 수행) → Spring에서 최종 저장  

.. FastAPI에서 하는 일들은?.. 3D 그래픽스 가공 및 공간 연산(후보군)  
1. **3D 파일 경량화**: GLB(웹 표준) 변환.. 자유배치
S3 → Spring → .. 받은 다음, `scipy`등을 사용해 Decimation(폴리곤↓)  
및 `Draco 알고리즘`로 압축 → S3에 재업로드  

2. **Chunk(청크 단위) 공간 인덱싱**: 카메라 범위 한정.. Grid  
Grid 맵을 청크 단위로 쪼갬: 카메라 시야 범위 청크만 서빙(공간 스트리밍)  





