<span class="Apple-style-span" style="font-size: 9pt; line-height: 1.5;"></span>
<span class="Apple-style-span" style="font-size: 9pt; line-height: 1.5;"><img src="Nuvola_mimetypes_java_jar.png" width="128" height="128" />
</span>

eclipse 에서는 java 로 프로그램을 만든 후 export 명령을 통해 쉽게 jar 로 묶을 수 있다. 여러개의 class 파일들을 배포하는 것보다 하나의 파일이 배포하기 쉽고, 압축이기 때문에 용량도 줄고, 단순함은 배포의 오류를 줄일 수도 있다.

 여튼 eclipse 에서는 매우 쉽게 jar 파일을 만들 수 있는데, 이미지 파일이나 사운드 파일등의 리소스 파일을 포함할 경우 경로 지정에 문제가 제법있다. 바로 로컬 파일 시스템과 jar 파일 시스템(?)의 경로 차이 때문에 발생하는데, 이상하게 검색해본 방법이 대부분 제대로 동작하지 않아서 이리저리 해본 결과, 다음과 같이 패키지 이름을 지정해주는 것으로 해결할 수 있었다.

> URL fileStream = getClass().getClassLoader().getResource("com/wimy/clipdic/clipdic.png");

eclipse 에서 getResource 함수를 파싱해서 export 시에 자동으로 해당 파일을 포함해주며, 주의해야할 점은 src/bin 폴더를 따로 관리하는 경우 bin 폴더의 저 위치에 해당 파일을 넣어둬야한다는 점이다. src/bin 을 따로 쓰지 않는다면 가장 좋은 방법인것 같다.


