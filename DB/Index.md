## Cluster / Non-Cluster Index
1. 클러스터 인덱스
   
   ![cluster index](https://github.com/destiny1017/TIL/assets/44860334/aa05b8a0-b267-4ede-af5b-bafe8635382d)

   - PK 설정시 자동으로 만들어지는 인덱스
   - 테이블당 1개만 허용
   - 데이터는 항상 정렬 상태를 유지함
   - 정렬 상태이기 때문에 데이터의 검색 속도는 빠르나 삽입 삭제의 속도는 느림
   - 리프노드가 데이터 페이지를 다이렉트로 바라보고 있다
  
2. 넌클러스터 인덱스
   
   ![non-cluster index](https://github.com/destiny1017/TIL/assets/44860334/0d07ad4d-183b-417b-9804-f932e83eecc0)
   
   - 상황에 따라 사용자가 직접 생성하는 인덱스로, 테이블당 약 240개까지 생성 가능
   - 데이터를 직접 정렬시키는 게 아니라 인덱스 페이지만 정렬하여 삽입 삭제가 비교적 빠름
   - 리프노드 페이지에는 데이터가 아니라 데이터를 바라보는 포인터가 key:value 형태로 들어가있음
