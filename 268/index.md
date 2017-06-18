 다음과 같은 코드를 통해서 현재 웹 브라우져의 플래시 플레이어 버젼을 확인할 수 있다. 특정 버젼 이상(유튜브의 경우 8 이상이어야한다)이 필요할 경우 체크할 때 사용하면 된다.

> <span class="whitespace"> </span><span class="xml-punctuation">&lt;</span><span class="xml-tagname">script </span><span class="xml-attname">src</span><span class="xml-punctuation">=</span><span class="xml-attribute">"http://www.google.com/jsapi" </span><span class="xml-attname">type</span><span class="xml-punctuation">=</span><span class="xml-attribute">"text/javascript"</span><span class="xml-punctuation">&gt;</span><span class="xml-punctuation">&lt;/</span><span class="xml-tagname">script</span><span class="xml-punctuation">&gt;</span>
> <span class="whitespace"> </span><span class="xml-punctuation">&lt;</span><span class="xml-tagname">script </span><span class="xml-attname">type</span><span class="xml-punctuation">=</span><span class="xml-attribute">"text/javascript"</span><span class="xml-punctuation">&gt;</span>
> <span class="whitespace"> </span><span class="js-variable">google</span><span class="js-punctuation">.</span><span class="js-property">load</span><span class="js-punctuation">(</span><span class="js-string">"swfobject"</span><span class="js-punctuation">, </span><span class="js-string">"2.1"</span><span class="js-punctuation">)</span><span class="js-punctuation">;</span>
> google.setOnLoadCallback(onLoad);
> function onLoad()
> {
>     var flashVersion = swfobject.getFlashPlayerVersion();
>   
>     alert("Flash version : " + flashVersion.major + "." + flashVersion.minor);
> }
> <span class="xml-punctuation">&lt;/</span><span class="xml-tagname">script</span><span class="xml-punctuation">&gt;</span>

<span class="xml-punctuation"></span>참고로 IE6 의 경우 기본적으로 버젼 6 이 깔려있다.
<span class="whitespace"></span>

