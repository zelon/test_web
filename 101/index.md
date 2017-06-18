 크~~ ㅠ.ㅜ
 우분투에 Sun 의 공식 자바를 GUI 상에서 간단하게 '프로그램 추가/제거' 를 통해서 거의 몇번만 클릭하면 깔아줘서 좋았다고 [생각](http://www.wimy.com/tt/57)했다.
 그런데 이게 조금 낚시성이었다. -\_-;;; 아마 나만 몰랐던게 아니라고 생각한다. 바로 이렇게 설치한 자바 Runtime 은 설치만 될뿐 설정이 제대로 되지 않은 것이었다.
 자바를 설치한 후 console 을 하나 열어서 java 라고 쳐서 실행해보자. Sun 의 java 의 도움말이 나오는게 아니라, gij 의 도움말이 나올 것이다. 그렇다. 설치만 되었을뿐 '설정' 이 안된거다.
 우분투에서 이상하게 기본 설정된 eclipse 가 좀 뻗는거 같아서, 직접 다운받아서 설치했는데, 그래도 계속 VM error 를 내서, 에잇 java 도 직접 깔아보자 하면서 생각해보니... gij 는 공식 Sun 의 JRE 가 아닌데??? 하는 생각이 들었다.
 그래서 따라가보니, /usr/bin/java 는 /etc/alternatives/java 를 가르키고, 이건 역시나 gij 를 가르키고 있었다. 그래서 /etc/alternatives/java 를 /usr/lib/jvm/java-6-sun/bin/java 를 가르키게 변경하고 나니... 두둥... eclipse 속도가 눈에 띄게 빨라지고 이제 뻗지도 않는다.
 난 우분투의 편리함에 낚였던 것인가 ㅠ.ㅜ
 추가로 kldp.org 에서 얻은 답변을 적습니다.

> 별다른 이유가 없다면 update-java-alternative를 쓰시길 권해드립니다.
>
> 예를 들면 위의 작업은 다음 명령 한 줄로 끝납니다.
> sudo update-java-alternative --set java-6-sun
>
> 위에서 하신것처럼 java만 달랑 수동으로 바꾸면 나중에 문제가 될 수 있습니다. javac, javaws, appletviewer, ControlPanel, javaplugin.so 등등 바꿀께 꽤 많거든요...
>
>  - iolo 님으로부터
>
>  - http://kldp.org/node/84800


