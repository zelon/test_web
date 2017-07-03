 집에서 종종 unity 만지면서 놀다가, 유니티 클라우드 빌드를 써보기로 하고 간단히 설정해서 써봤는데, 로컬에서 빌드하면 잘 시작되는데, 유니티 클라우드 빌드에서 빌드한 apk 를 받아서 실행하면 유니티 로그 화면에서 멈추는 것이다. 이 문제로 고생하다가 해결하려고 마음 먹고 adb 로 로그를 찍어봐도 별 이상없고 해서 유니티 클라우드 빌드 웹페이지의 설정 화면을 살펴보니, 해결할 수 있었다.

 Config -&gt; Show Advanced Options -&gt; Edit Advanced Options 클릭 -&gt; Scene List 에 본인의 Scene 파일 이름(예를 들면 Default)를 적고 Add 버튼을 누른 후 저장하자. 아마 제대로 된 경로(Assets/Default.unity)를 보여줄 것이다. 

 즉, 클라우드 빌드 시에 기본으로 시작할 scene 을 지정해주지 않아서 발생한 문제였다(사실 이걸 왜 굳이 설정해줘야 하는지는 의아하지만;;). 여튼 이제 다시 빌드를 후 apk 를 설치해보자. 잘 시작된다.

