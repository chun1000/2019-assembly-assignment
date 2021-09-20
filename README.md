### 1. 프로젝트에 대해서

---

- 2019년 어셈블리어 개인 과제입니다. 
- 정수의 배열을 받아서 모든 정수에 대해 소인수분해를 진행하는 과제입니다.
-  SIC/XE라는 간략화된 교육용 컴퓨터의 어셈블리어 구조를 따르고 있습니다.
- READEME 파일을 작성하는데 사용한 프로젝트 원본 보고서는 [여기서](https://github.com/chunyunseo/AssemblyAssignment/blob/8041bb611fc74380487f4f0b7874998fc272bf06/%EB%B3%B4%EA%B3%A0%EC%84%9C/A1-%EC%96%B4%EC%85%88%EB%B8%94%EB%A6%AC%EC%96%B4%20%EA%B0%9C%EC%9D%B8.pdf) 다운로드 받을 수 있습니다.

### 2. 의사 코드

---

![image-20210920223533699](https://raw.githubusercontent.com/ChunYS/ImageRepo2021/Image/img/image-20210920223533699.png)

- C스타일로 작성하였으나, 코드는 어셈블리어로 작성되어있습니다.

### 3. 설계 모듈화

---

- 가독성을 높이기 위해서 JSUB, RSUB의 서브루틴 함수를 사용하였습니다. 코드에 사용된 모듈들은 아래와 같습니다.

![image-20210920224502167](https://raw.githubusercontent.com/ChunYS/ImageRepo2021/Image/img/image-20210920224502167.png)

### 4. 실행 스크린샷

---

- 정상 실행

![image-20210920223806901](https://raw.githubusercontent.com/ChunYS/ImageRepo2021/Image/img/image-20210920223806901.png)

- 비정상 실행

![image-20210920223837009](https://raw.githubusercontent.com/ChunYS/ImageRepo2021/Image/img/image-20210920223837009.png)

### 5. 코드의 흐름

---

- 어셈블리어 코드는 아래의 흐름을 따릅니다.

1. SCAN 함수를 통해서 STIN으로 들어온 값을 받아서 숫자로 변환한 뒤, N에 집어넣는다.
2. PARSE함수를 통해서 STDIN에 들어온 값을 N과 개수가 일치하나 검사한 뒤, ARY 배열에 스페이스바로 구분하여 하나 씩 집어넣는다.
3. ARY 배열의 값을 배열 포인터를 하나씩 증가시키면서 NBUF1을 통해서 FACT 함수에서 소인수분해를 하며, 결과를 즉시 출력한다.
4. 나머지 함수들은 정수->문자열 변환 함수 등의 동작을 도와주는 함수나 예외 처리 함수들이다.

### 6. 느낀점

---

- 첫 어셈블리어 프로그램이라 미흡한 점이 많았습니다. NBUF, SBUF 등의 버퍼를 전역으로 선언하고 JSUB 안에서 이를 처리하는 함수로 구현했는데, 이번에 거의 사용하지 않았던 T나 S 레지스터 등에 값을 반환하도록 처리하였으면 효율적인 메모리 사용이 가능했을 것입니다.
- EROVR, ERFOM, ERNUM 등 에러처리 함수를 따로 선언했지만, 이 셋은 전부 ERROR OCCUR!를 출력하고 정지해서 기능상 차이가 없습니다. 그 이유는 String을 출력하는 함수를 전부 따로 구현했기 때문입니다. Error를 출력하는 PRINT 함수와 결과를 출력하는 PRINT 함수가 나누어져있기에 여러 String 함수를 각각 정의하는 것이 큰 부담으로 다가왔습니다. Indirect Addressing을 적절히 활요하면 String의 주소값을 받아서 출력하는 범용적인 함수의 설계가 가능하지 않았을까 싶습니다.