 Visual Studio 2008 Team System 에서 안전한 문자열 처리를 위해서 strsafe.h 를 사용하면 strsafe.h 안에서 다양한 warning 을 뿜어낸다. 마찬가지로, include &lt;deque&gt; 를 해도 이런저런 복잡한 warning 을 뿜어낸다.
 바로 2008에서의 코드 분석기 때문인데, 다음과 같은 방법으로 특정 헤더 파일에 대해서 무시를 할 수 있다. [\[출처\]](http://social.msdn.microsoft.com/forums/en-US/vstscode/thread/e051f263-c790-44be-8317-5232ce4f239b "[http://social.msdn.microsoft.com/forums/en-US/vstscode/thread/e051f263-c790-44be-8317-5232ce4f239b]로 이동합니다.")

> \#include &lt;CodeAnalysis/warnings.h&gt;
> \#pragma warning(push)
> \#pragma warning(disable: ALL\_CODE\_ANALYSIS\_WARNINGS)
> \#include &lt;strsafe.h&gt;
> \#include &lt;deque&gt;
> \#pragma warning(pop)

 include &lt;strsafe.h&gt;, &lt;deque&gt; 등 원하는 include 앞에 위와 같이 3줄을 적어주고, 마지막 줄을 통해서 '여기까지만!' 이라고 해주면 된다.
 warning 에 민감한 나에겐 무척이나 다행스러운 조치이다...  이 문제의 근본적인 해결방법은 sdk 를 최신 버젼으로 업그레이드하는 것인데... 혹시나 모를 내 소스를 컴파일하는 분들은 바로 warning 없이 컴파일이 되기를 바라는 마음에 소스를 수정해둔다. ㅋ(사실 오픈소스라고 소스를 받아서, 한번에 컴파일 안되는 경우가 대부분인데, 한방에 warning 도 없이 되면 정말 기분이 좋을듯~~ ㅋ)

