<img src="nsis.png" width="100" height="100" />
 갑자기 ZViewer 새버젼을 설치할 때 이전 버젼 위치에 항상 덮어써서 '업그레이드' 를 하게 하고 싶어졌다. 어느날 문득 갑자기 ㅋ
 해야할 일은

1.  현재 설치된 디렉토리를 찾아서 넣고
2.  디렉토리를 선택할 때 텍스트 입력창 비활성화
3.  Browse(찾아보기) 버튼을 비활성화

 이렇게 인데, 생각보다 도움말을 뒤져봤는데 원하는 명령을 찾을 수 없었다. 현재 설치된 디렉토리를 찾는건 [이전 글](http://wimy.com/tt/208)에서 특정 레지스트리를 찾으면 되어 금방이었는데, MUI 기반이라서 관련 매크로와 NSIS 의 Contrib 디렉토리를 뒤져보았는데 Resource 와 ControlID 처럼 보이는 것까지는 찾을 수 있었는데, 원하는 내용을 찾지 못했다.
 그래서 검색을 시작했는데, 처음에는 한글로 검색. 주옥같은 [게으른 엔지니어님의 NSIS 글](http://www.cipher.pe.kr/tt/cipher/category/6)을 찾을 수 있었지만 원하는 내용으로의 단서만 찾을 수 있었다. 그래서 다시 NSIS 도움말에서 대충 원하는 내용을 찾아서 일단 대충 만들었는데, 실제 코드가 분명있을거라는 생각이 (또 갑자기) 들어서, 'nsis disable browse button' 이라고 구글로 검색. 제일 처음에 [원하는 내용](http://forums.winamp.com/showthread.php?threadid=166727) 발견 -\_-;;; 코드까지 나와 있어서 정말... 좀 허무했지만, 내가 만들어본 코드랑 거의 비슷했다. 하지만 '찾아보기 버튼' 까지는 나와있지 않아서 좀 더 내용을 덧붙여서 완성~
 관련 코드는 다음과 같다.

> ...
> !define MUI\_PAGE\_CUSTOMFUNCTION\_SHOW onDirectoryShow
> !insertmacro MUI\_PAGE\_DIRECTORY
> ...
> ; 디렉토리 선택 화면이 보여질 때 실행되는 함수. 이미 설치된 경우 디렉토리 선택을 할 수 없게 한다.
> Function onDirectoryShow
>   push $R0
>   push $R1
>   ReadRegStr $0 HKLM "SOFTWARE\\Microsoft\\Windows\\CurrentVersion\\Uninstall\\ZViewer" "UninstallString"
>   IfErrors onDirectoryShowEnd onDirectoryShowDisableBrowse
> onDirectoryShowDisableBrowse:
>   FindWindow $R0 "\#32770" "" $HWNDPARENT
>   GetDlgItem $R1 $R0 1019
>   EnableWindow $R1 0
>   GetDlgItem $R1 $R0 1001
>   EnableWindow $R1 0
> ; '기존의 설치될 디렉토리를 고르세요' 라는 메시지를 '다시 설치합니다' 라는 내용으로 바꿈
>   GetDlgItem $R1 $R0 1006
>   SendMessage $R1 ${WM\_SETTEXT} 0 "STR:$(TEXT\_REINSTALL)"
> onDirectoryShowEnd:
>   pop $R1
>   pop $R0
> FunctionEnd

 코드를 조금 설명해보자면,
- MUI\_PAGE\_DIRECTORY 앞 문장에 define 을 해서 callback 을 등록하는게 일단 중요하다.
- ReadRegStr 에서 읽어오는 것은 '프로그램 추가/제거' 에서 쓰이는 레지스트리이다.([참고](http://wimy.com/tt/208))
- FindWindow 로 Directory 선택창을 읽어오고, GetDlgItem(win처럼) 로 Control handle 을 얻어온 후 EnableWindow 로 disble 시킨다.
- SendMessage 에 ${WM\_SETTEXT} 를 써서 기존의 글자를 바꾼다.

