 난 우분투 7.4 를 쓰다가 7.10 을 쓰게 된 유저이다. 7.4 에서는 외부 저장소에서 virtualbox 를 쓰다가 이제 7.10 에 오면서 기본 저장소의 virtualbox 를 쓰기 시작했다.
 그런데 이상하게 우분투 7.10 에서 자꾸 VirtualBox 로 작동 중인 윈도우 클라이언트가 수시로 크래시되었다. 그래서 혹시나하고 홈페이지에 가서 확인을 해보니 현재 우분투 7.10 의 공식 저장소의 버젼은 1.5.0 인데  공식 홈페이지의 버젼은 1.5.2 였다. 그래서 업그레이드를 하기로 결정하고, 현재 버젼을 삭제하고, virtualbox 쪽의 apt 소스를 추가하고 설치했다. 그런데 새로운 버젼으로 기존의 이미지를 읽으니 다음과 같은 에러를 내면서 시작을 할 수 없는 것이었다.
----
00:00:01.506 VirtualBox 1.5.2 r25433 linux.x86 (Oct 18 2007 08:59:10) release log
00:00:01.506 Log opened 2007-11-28T11:36:23.348399000Z
00:00:01.507 Support driver version/Cookie negotiations error: rc=VERR\_VERSION\_MISMATCH
00:00:01.507 ERROR \[COM\]: aRC=0x80004005 aIID={1dea5c4b-0753-4193-b909-22330f64ec45} aComponent={Console} aText={The VirtualBox support driver which is running is from a different version of VirtualBox.  You can correct this by stopping all running instances of VirtualBox and reinstalling the software..
----
 그래서 VDI(Hdd image)는 놓아두고 이미지 설정만 새로 만들어도 같은 현상. 그래서 구글링해보니 위의 메시지로 된 글들은 모두 문제해결이 안된 상태고, 혹시나 'virtualbox 설정' 을 눌렀을 때 에러가 나서 그런가 해서 virtualbox usb error 로 찾아보니, 이런 저런 많은 내용이 나오는 사이트에서 다음과 같은 방법으로 해결할 수 있었다.
 
 http://doc.gwos.org/doku.php/doc:office:virtualbox 에서 알아냄.
 결과적으로는  sudo /etc/init.d/vboxdrv setup 을 실행 하면 내부적으로 커널 모듈 관련 컴파일을 하면서 이번 버젼 때문에 새로 설치하라는 메시지 에러가 사라진다!!
<img src="virtualbox.png" width="500" height="369" />

