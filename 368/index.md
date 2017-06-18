 SWT 를 이용해서 만든 Java 프로그램을 독립적으로(eclipse 없이) 실행하려면 생각보다 잘 안된다 -\_-; 보통은 MOZILLA\_FIVE\_HOME 을 설정하라고 나오는데... 여튼 다음의 방법을 참고하여 실행하자.
 

> sudo apt-get install xulrunner-1.9.2
> export MOZILLA\_FIVE\_HOME=/usr/lib/xulrunner-1.9.2.17/ 
> export LD\_LIBRARY\_PATH="$MOZILLA\_FIVE\_HOME":"$LD\_LIBRARY\_PATH"
> java -jar ClipDic.jar

 웹 검색을 해보면, MOZILLA\_FIVE\_HOME 을 /usr/lib/firefox 등으로 설정하라고 나오는데, 위와 같이 xulrunner 를 설치하여(sudo apt-get install xulrunner-1.9.2) 그 경로를 정해주는 것이 해결책이 될 수 있다(ubuntu 11.04기준). 검색해보면 xulrunner 2.0 도 있는데 이 버젼은 library 가 맞지 않는듯...
 그리고 MOZILLA\_FIVE\_HOME, LD\_LIBRARY\_PATH 를 설정해준다. export 2줄은 ~/.profile 제일 끝에 추가해주면 다시 부팅시에도 잘 동작한다.
 
