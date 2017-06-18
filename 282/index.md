<img src="go-logo-black.png" width="220" height="77" />
<http://googlesystem.blogspot.com/2009/11/go-googles-programming-language.html>
 구글에서 새로운 언어를 발표했다. 오픈소스이다. 재미있는 점은 시스템 프로그래밍이 되고, garbage collection 이 되는 언어라는 점이다.(실제로 내가 써본건 아니지만;;) 그리고 의존성을 줄이기 위해서 정말 간단한 프로그램을 짜도 항상 static link 가 되어서 용량이 1.2mb 정도된다고 한다. 하지만 요즘은 워낙 hdd 가 크기 때문에 임베디드 프로그래밍이 아닌다음에야 이건 단점까지는 안되고, hdd 가 넉넉한 시스템에서는 꽤 각광 받을지도 모른다.(자바, C\# 프로그래밍 배포할 때 VM 신경쓰는거에 비하면 말이다)
 hello world 는 다음과 같다.

``` code
package main


import "fmt"


func main() {

  fmt.Printf("Hello, 世界\n")

}
```

 일단은 저런 새로운 언어가 나왔구나하고 알아두자. 어차피 새로운 언어로 당장 뭘 할 것도 아니고, 간간히 생각나면, 코드 검증이나 빌드 도와주는 프로그램 만들다가(지금의 파이썬이 하는것처럼), 작은 유틸리티 만들어보다보면 익혀지겠지... 라는 생각? ㅋ 사실 eclipse 에 개발환경이라도 갖춰지면 해볼까라는 생각 중 ㅋㅋ
ps : 요즘은 괜히 google app engine 때문에 jsp 에 작은 관심을 갖는 중

