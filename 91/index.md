드디어 그래픽 카드 때문에 설치를 제대로 못 했던 우분투를 멤버십 데스크탑에 깔았다. 일단 기본적으로 그래픽 카드를 제대로 인식해서 저번 6 버젼의 우분투에서 설치조차 제대로 할 수 없던 게 해결되었다.
 그런데 기본적으로 설치할 수 있는 NVidia binary 를 설치하니 X-window 가 다운되었다. 그래서 검색해보니 [\[이 곳\]](http://www.ubuntugeek.com/how-to-fix-nvidia-acceleration-in-feisty-nvidia-8800-and-legacy-users.html) 에서 제대로 된 정보를 얻을 수 있었다.
 영어로 되어 있으니 한글로 간단히 요약해 보자.
 먼저 firefox 등의 웹브라우저를 통해서 nvidia.com 에서 리눅스용 드라이버를 다운받아 둔다.
 콘솔을 열어서 다음과 같이 build-essential 을 설치한다. sudo 명령이 암호를 물어오니 암호를 넣어주자.

sudo apt-get install build-essential

sudo apt-get install xserver-xorg-dev

 그 후 아래 파일을 열어서

sudo vi /etc/default/linux-restricted-modules\*

DISABLED\_MODULES=”" 를 DISABLED\_MODULES=”nv”로 고친다.
저장 후 vi 를 종료하고, sudo reboot 를 해서 시스템을 리부팅시킨다.

리부팅된 시스템에서 부팅되기 전에 recovery 모드로 들어와서 아까 다운받아놓은 드라이버를 다음과 같이 실행시킨다.

 sudo sh NV\*
 설치 과정 중 xorg.conf 파일을 업데이트 시킬지를 물어보는데 yes 라고 한다. 그런 후 sudo reboot 를 하면 제대로 설정된 nvidia with 우분투를 만날 수 있다.
