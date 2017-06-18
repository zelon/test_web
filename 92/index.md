http://www.wimy.com/tt/91 의 글에서 nvidia 를 제대로 설정했는데 이제 듀얼 모니터가 문제였다 -\_-;
 nvidia 드라이버를 설치하고 나면 프로그램 -&gt; 시스템 도구 -&gt; NVIDIA X Server Settings 라는 메뉴가 생기는 데 이 프로그램을 통해서 설정하고 나면, 리부팅을 했을 때 다시 원점으로 돌아가버리는 것이다. 중간에 'Save to X Configuration File' 버튼을 눌러도 같은 현상이 생기기에 혹시나해서
 sudo /usr/bin/nvidia-settings
 라는 명령으로 root 권한을 줘서 설정해보았다. 잘 되었다. 아마 nvidia 에서 root 권한에 대한 이해(?)가 잘 안되었는지, 아니면 우분투에서 해보질 않았는지... 여튼 위와 같이 해결해서, 2번째 모니터를 TwinView 로 잡고, Position 을 Right of 로 해주니, 일반적으로 윈도우에서 처럼 쓰는 듀얼 모니터 환경을 구성할 수 있었다.

