http://blogs.unity3d.com/kr/2016/04/25/debugging-memory-corruption-who-the-hell-writes-2-into-my-stack-2/

갑자기 스택에 이상한 값이 쓰여지는 현상을 디버깅하는 과정을 정리한 글. 과정을 따라가는 것이 흥미롭다.

결론은 시스템 콜 안에서 예외가 발생해서 unwinding 되었고, 콜 안에서 사용된 스택 변수의 값이 뒤늦게 세팅되어서 발생되었다.
