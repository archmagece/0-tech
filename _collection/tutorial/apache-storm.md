Apache Storm
============

Clojure로 코어를 만들었다는데서관심을 가졌으나
최신버전인 2.0.0에서는 Java로 컨버팅 되어 버렸다는 슬픈 소식

python, clojure, java, shell script 폴리글랏이라고 했으나python코드는 별로 쓸모없는 포인트만 먹고 있다. 빼버리면 좋겠는데
실행 파라미터체크하는 정도 코드만 있다. 스톰 토폴로지를 파이썬으로도 만들 수 있다고되어 있는 것 같은데... 별로 그럴 생각은 없어서..
이 부분을 제외하고 자바와 설정파일을 이용하는게 여러 환경에 배포하는데도 편리하고 좋을 것 같다

intellij로 열려고 하는데 잘 안열린다.
uber-jar 돼지자르를 만들 때 사용하는 shade-deps로 인한 임포트오류가 발생

한개의 실행단위를 topology라고 하는데 이걸 로컬에서 실행테스트도 해보고 디버깅도 해보고 로그도 찍어보고 하고싶은데... 다 쉽지 않다. 
유닛테스트, 로컬실행, 디버깅 환경부터 만들어야 뭘 제대로 쓸 수 있을 것 같다.

문서...
이것저것 써 있기는 한데
고인물파티같은 느낌
한국 커뮤니티도 없다.
Flink만 쓰는건가
인터페이스단위로 분석해놓은 문서조차 없다
튜토리얼이나 예제가 있긴한데 딱 맞는 분석사례만 있는게 아니니까.. 결국 분석해서 써야된다

