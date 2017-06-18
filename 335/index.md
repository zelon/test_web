Go 는 google 내부에서 쓰인다는 언어로 한창 개발 중이며, [Ken Thompson(유닉스를 만들고, C 언어의 선배격인 B 언어를 만들고, UTF-8 을 만든) 가 개발](http://en.wikipedia.org/wiki/Ken_Thompson "[http://en.wikipedia.org/wiki/Ken_Thompson]로 이동합니다.")하여 주목받고 있는 언어이다.

 전에도 한번 [간단히 소개](http://blog.wimy.com/282 "[http://blog.wimy.com/282]로 이동합니다.")했었는데, 오늘 다시 한번 둘러보다가 defer 라는 재미있는 동작이 있어서 적어본다. defer 는 쉽게 생각해서 함수의 실행을 예약해두는 것이다. 다음의 예를 보자.

> func CopyFile(dstName, srcName string) (written int64, err os.Error) {
>
>     src, err := os.Open(srcName, os.O\_RDONLY, 0)
>
>     if err != nil {
>
>         return
>
>     }
>
>     defer src.Close()
>
>  
>
>     dst, err := os.Open(dstName, os.O\_WRONLY|os.O\_CREATE, 0644)
>
>     if err != nil {
>
>         return
>
>     }
>
>     defer dst.Close()
>
>  
>
>     return io.Copy(dst, src)
>
> }

한번에 아~~! 라고 하면 이미 천재 프로그래머..... 여튼 defer src.Close() 라고 해두면, 해당 함수 안에서 return 이 될 때 알아서 src.Close() 를 실행해주는 것이다.

 꽤 괜찮은 또다른 예가 바로 mutex 등을 하나의 함수 안에서 get & release 해줄 때이다. get 한 다음에 release 해주지 않고 나온다던지 이러면 골치 아픈 데드락을 만들어주는데 이것을 꽤 방지할 수 있게 해준다.

 메모리, 리소스, 혹은 핸들을 관리할 때 많은 책에서 하는 얘기가, '할당할 때, 언제 해제할지를 고려해라' 라는 내용인데, 이제는 할당이 성공하면 바로 해제할 코드를 바로 밑에 적어주면 되는 것이다.

 C++ 등에서는 이와 비슷한 동작을 위해서 클래스의 생성자 & 소멸자 트릭을 이용해서 하는 경우가 많았지만, 언어 차원에서 제대로 지원해줄 수 있게 되는 것이다.

 [새로운 언어의 멋진 기능](http://blog.golang.org/2010/08/defer-panic-and-recover.html "[http://blog.golang.org/2010/08/defer-panic-and-recover.html]로 이동합니다.")을 봐두는 것은 꽤 재미있는 것 같다.
