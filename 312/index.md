/home/.fonts 폴더에 ttf 파일을 복사하고,(폴더 없으면 만들고)
/etc/fonts/conf.d/29-language-selector-ko-kr.conf 파일을 편집해서,
&lt;!-- Turn off antialias and autohint for Korean fonts depending on pixelsize --&gt;
밑에 있는
&lt;edit name="antialias" mode="assign"&gt;
        &lt;bool&gt;true&lt;/bool&gt;
    &lt;/edit&gt;
        &lt;edit name="autohint" mode="assign"&gt;
        &lt;bool&gt;true&lt;/bool&gt;
    &lt;/edit&gt;
이렇게 true 로 수정하면 된다. 기본적으로 이렇게 배포되면 좋을텐데 좀 아쉬운 부분이다.

