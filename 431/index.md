뭐 당연한 얘기일 수도 있는데, go언어를 appengine 으로 개발하면서 로컬에서 띄운 서버인데도 1초 정도 걸렸다. 너무 느려서 stackoverflow 에 질문했더니... <a href="http://stackoverflow.com/questions/33942583/too-slow-ttfblatency-with-go-language-in-appengine/" class="uri" class="tx-link">http://stackoverflow.com/questions/33942583/too-slow-ttfblatency-with-go-language-in-appengine/</a> 실서버에서는 괜찮을거라고...

근데 나는 실서버에 올려도 느려서 혹시나 하고 developer console 에서 확인해보니 appengine 의 위치가 us-central 이다. 그래서 azure 를 통해서 가상 컴퓨터를 미국 중부에 만들어서 접속해보니 37ms 안에 응답이 시작되었다. 역시...

appengine 을 쓸 때는 빠른 응답을 기대하고 쓰면 안되겠군.

테스트 사이트 : <a href="http://test-try-go.appspot.com/" class="uri" class="tx-link">http://test-try-go.appspot.com/</a>

소스 코드 : <a href="https://github.com/GoogleCloudPlatform/appengine-try-go" class="uri" class="tx-link">https://github.com/GoogleCloudPlatform/appengine-try-go</a>


