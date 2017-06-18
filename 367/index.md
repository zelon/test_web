 ubuntu 11.04 에서는 unity 덕분에 프로그램 바로가기를 만들기가 쉽지 않다. 하지만 한번 만들어두면, 꽤 편리하게 사용할 수 있기 때문에(윈도우키 후 나타나는 검색 창에서 검색도 가능하다), 자주 쓰게되는 개인적으로 만든 프로그램이라면 아래와 같은 방법을 사용해서 만들자.
~/.local/share/applications/myprogram.desktop 에 아래 내용을 참고해서 만들자.

> \[Desktop Entry\]
>
> Type=Application
>
> Name=ClipDic
>
> Comment=ClipDic
>
> Exec=java -jar /home/zelon/Programs/ClipDic/ClipDic.jar
>
> Icon=/home/zelon/Programs/ClipDic/clipdic.svg

참고로 아이콘은 svg, png, xpm 등 대부분의 형식이 가능하다. 좀더 자세한 항목들은 /usr/share/applications/firefox.desktop 파일을 참고하자.


