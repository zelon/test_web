 indigo 의 cdt 부터는 toolchain 에 Microsoft Visual C++ 설정이 포함되어 있다. 그런데 이 설정이 path 가 제대로 설정되지 않아 제대로 컴파일이 되지 않는다(incubation tool 인듯.. 아마 sr1 쯤 나오면 수정될지도?).
 여튼, 빌드 시에 다음과 같은 에러를 낸다면,
 

> MSVCRT.lib(crtexe.obj) : error LNK2019: unresolved external symbol \_\_imp\_\_HeapSetInformation@16 referenced in function \_\_\_tmainCRTStartup
> MSVCRT.lib(crtexe.obj) : error LNK2019: unresolved external symbol \_\_imp\_\_EncodePointer@4 referenced in function \_pre\_c\_init
>
> MSVCRT.lib(atonexit.obj) : error LNK2001: unresolved external symbol \_\_imp\_\_EncodePointer@4
>
> MSVCRT.lib(atonexit.obj) : error LNK2019: unresolved external symbol \_\_imp\_\_DecodePointer@4 referenced in function \_\_onexit

 메뉴의 Project -&gt; Properties 에 가서, C/C++ Build -&gt; Environment 중에서 INCLUDE, LIB 항목을 살펴보자.
만약 VC++ 98, VC++ 2010 등 여러 툴이 깔렸다면, INCLUDE, LIB 를 그 중에서 하나만 참조되도록 맞춰주자. 즉, 경로를 VC++ 2010 만 참조하도록 수정.
 예를 들어 경로에 C:\\Program Files\\VC98;C:\\Program Files\\VC2010 이렇게 98과 2010 이 섞여있다면, VC98 관련은 제거하자.
 이렇게 수정한 후에 다음과 같은 에러가 난다면,
> LINK : fatal error LNK1104: cannot open file 'kernel32.lib'

 LIB 경로에 다음 경로(디렉토리명은 자신의 환경에 따라 다를 수 있음)를 추가(!)해보자.
> C:\\Program Files\\Microsoft SDKs\\Windows\\v7.0A\\Lib

 결론은, 경로 설정을 잘하자. ^^/
ps : eclipse cdt 가 이제 Microsoft Visual Studio toolchain 을 제공해준다. 좋구나 -\_-/
