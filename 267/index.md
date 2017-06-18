 오늘도 역시나 pop.wimy.com 를 다듬다가 정리하게 된 내용이다.
IE6 에서는 파이어폭스나 크롬과 다른게 "new XMLHttpRequest()" 로 객체를 만들 수 없다. 그래서 이래저래 검색을 하고, pop.wimy.com 에 적용해 가면서 확인한 내용이다.
일단 XMLHttpRequest 는 다음과 같이 객체를 만들면 IE6 를 체크 안하고 사용할 수 있다.

> function newXMLHttpRequest()
> {
>     var ret = null;
>    
>     try
>     {
>         ret = new XMLHttpRequest();
>     }
>     catch ( e )/// ie 6 에서는 exception 발생
>     {
>         try
>         {
>             ret = new ActiveXObject("Microsoft.XMLHTTP");
>         }
>         catch ( e2 )
>         {
>             alert("지원되지 않는 브라우저입니다.");
>         }
>     }
>     return ret;
> }

그리고 실제로 request 할 때는 다음을 주의하자.
 onreadystatechange 콜백을 설정한 후, 콜백 함수 안에서

> if ( this.readyState == 4 && this.status == 200 )

위와 같이 쓰는 경우가 있는데 이렇게 쓰면 IE6 에서 문제를 일으킨다. 그러므로 다음처럼 전역 변수를 하나두고, 이 전역 변수만을 사용해서 코딩하자.

> var musicChartRequest = null;
> function onMusicChartResponse(data)
> {
>    /// ... 여기서 하고 싶은 일하기~
> }
> function musicChartRequestHandler()
> {
>     if ( musicChartRequest.readyState == 4 && musicChartRequest.status == 200)
>     {
>         if ( musicChartRequest.responseXML == null )
>         {
>             onMusicChartResponse(null);
>         }
>        
>         if( musicChartRequest.responseXML.getElementsByTagName('song'))
>         {
>             // success!
>             onMusicChartResponse(musicChartRequest.responseXML);
>         }
>         else
>         {
>             onMusicChartResponse(null);
>         }
>     }
>     else if (musicChartRequest.readyState == 4 && musicChartRequest.status != 200)
>     {
>         onMusicChartResponse(null);
>     }
> }
> function requestMusicChart(listValue)
> {
>     musicChartRequest = newXMLHttpRequest();
>    
>     if ( musicChartRequest == null ) return;
>    
>     musicChartRequest.onreadystatechange = musicChartRequestHandler;
>    
>     musicChartRequest.open("GET", "a.xml");
>     musicChartRequest.send(null);
> }


