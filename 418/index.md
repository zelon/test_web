 갑자기 boost 라이브러리의 asio 를 써보고 싶어져서 boost 를 다운받아서 잠깐 매뉴얼을 읽어본 후에 하라는 대로 bootstrap 과 b2 를 실행해서 라이브러리 빌드를 한 다음에 Visual Studio 2013 에서 asioTest 프로젝트를 만든 후 include/lib 디렉토리를 제대로 설정 후 빌드를 걸었더니 다음과 같은 링크 에러가 났다.

> Error    1    error LNK2019: unresolved external symbol "class boost::system::error\_category const & \_\_cdecl boost::system::system\_category(void)" (?system\_category@system@boost@@YAAEBVerror\_category@12@XZ) referenced in function "public: \_\_cdecl boost::system::error\_code::error\_code(void)" (??0error\_code@system@boost@@QEAA@XZ)    E:\\git\\asioTest\\asioTest\\asioTest.obj    asioTest
>
> Error    2    error LNK2019: unresolved external symbol "class boost::system::error\_category const & \_\_cdecl boost::system::generic\_category(void)" (?generic\_category@system@boost@@YAAEBVerror\_category@12@XZ) referenced in function "void \_\_cdecl boost::system::\`dynamic initializer for 'errno\_ecat''(void)" (??\_\_Eerrno\_ecat@system@boost@@YAXXZ)    E:\\git\\asioTest\\asioTest\\asioTest.obj    asioTest

 대충 해석해보면, boost::system::system\_category 를 찾을 수 없다는건데, 강제적으로 라이브러리 파일 링크를 걸어봐도 안되고, 도통 알 수가 없었다. 그러다가 asio 를 사용 중인 지인의 도움을 받아서 이리저리 비교해보다가 그 분도 링크 에러가 난 적이 있다면서, Win32 build 에서는 같은 에러가 나는 것을 보게 되었다...

 그랬다. 나는 요즘 계속 x64 프로그래밍만 하고 있어서 무의식적으로 x64 로 프로젝트를 설정했는데, boost 라이브러리는 win32 로 빌드가 기본이었다.

 b2 address-model=64 로 빌드를 다시 하니 링크 오류 해결~!! 

ps: 왜 boost 라이브러리에는 x86 이니 x64 같은게 lib 파일이름에 없을까라며 괜히 욕해본다;;
