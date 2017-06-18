<a href="http://box.wimy.com/" class="uri" class="tx-link">http://box.wimy.com/</a> 을 만들어놓고 많은 시간이 지나서, 한번씩 이런저런 버그들을 고치고는 하지만, 모바일에서 재생이 제대로 안되는 건 정말 골치 아픈 일이다. 특히 작년까지만 해도 대부분의 스마트폰에서는 동영상을 full-frame 으로 보여주지도 못했으니... 이제는 그나마 성능은 어느 정도 받쳐주는 것 같다.

 그런데 최근에 다시 스마트 폰에서 해보니 재생이 안되는 것이다. 이래저래 디버깅을 해보다가 안되어서 구글 공식 문서를 뒤져보니, 이런 내용이 나왔다 : <a href="https://developers.google.com/youtube/iframe_api_reference#Mobile_considerations" class="uri" class="tx-link">https://developers.google.com/youtube/iframe_api_reference#Mobile_considerations</a> 대충 읽어보면, "데이터망에서 원치않은 다운로드를 막기 위해서 임베드된 미디어는 자동으로 재생될 수 없다" 그래서, playVideo() 같은 함수들은 모바일 환경에서 재생이 제대로 되지 않는 것이었다. 그래서 필요한 것은?? 바로 "사용자의 인터랙션" 이다. 즉, 한번 터치해주면 잘 동작한다.

 그래서 html5 모드에서는 기본 재생을 일부러 막고, 사용자의 입력으로 재생이 시작되기를 기다린 후, 재생이 감지되면, 기존의 자동 플레이 모드처럼 동작하도록 수정했다. '한번만 터치되면', 그 다음부터는 playVideo() 등의 함수가 제대로 동작한다. 단 한번의 터치가 필요할 뿐...


