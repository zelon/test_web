 모든 프로그래밍의 시작은 hello world 라지만, plug-in 같은 종류의 프로그래밍은 시작할 수 있는 환경 찾기가 좀 힘들다.
 이번에 해볼 것은  gnome 의 패널에 내가 원하는 프로그램을 얹는 것이다. 1시간여의 삽질 끝에 알아낸 내용은 다음과 같다. 참고로 작업 환경은 우분투 7.10 데스크탑이다.
 우분투의 시냅틱 꾸러미 관리자에서 python 으로 검색 후, python-gnome2-desktop-doc 패키지를 설치했다. 그 후 /usr/share/doc/python-gnome2-desktop/examples/applet 에 가니 멋진 예제가 있었다. README 를 읽어보니, GNOME-PythonAppletSample.server 파일을 /usr/lib/bonobo/server 에 복사하고, applet.py 를 /usr/bin 에 복사하면 된다. 그리고 그렇게 한 후, 패널에서 패널 더하기를 했더니, 'PythonAppletSample' 이라고 떴다. 이 패널을 추가하면 화면 아래에 'Success!' 라는 패널 애플릿이 추가된다. 앞으로 이 2개의 파일을 수정해가면서 자신에 맞게 커스터마이징하면 될 것이다.
<img src="testPanel.png" width="500" height="24" />
 위와 같은 샘플이다.
 

