흔히 말하는 장, 단점은 다음과 같이 존재한다.

장점으로

1. 순환 참조로부터 상대적으로 자유로움
2. public API를 통해 재사용되는 코드와 재사용되지 않는 코드 분리 가능
3. 스탠다드에 따라 어느 정도 폴더 구조가 명확해짐
4. 비지니스 네임에 따른 분리가 가능

단점으로는

1. 결국 어떤 파일을 어디에 둘것이냐에 대한 세부적인 룰은 팀에 달려있으므로, 일시적인 생산성 저하가 존재한다.
2. barrel export의 문제점
3. 폴더 구조를 바꾸거나 네이밍을 바꾸는 과정에서 발생하는 오버헤드 (함수 이름 바꾸면 index.ts도 바꿔야함)
4. colocation이 깨진다
