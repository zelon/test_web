[다운로드(영문판)](http://www.microsoft.com/downloads/details.aspx?familyid=69d2219f-ce82-46a5-8aec-072bd4bb955e&displaylang=en)

[다운로드(한글판)](http://www.microsoft.com/downloads/details.aspx?displaylang=ko&FamilyID=69d2219f-ce82-46a5-8aec-072bd4bb955e)

[릴리즈노트](http://support.microsoft.com/default.aspx?scid=kb;en-us;918007)[](http://support.microsoft.com/default.aspx?scid=kb;en-us;918007)

드디어 Visual Studio .NET 2003 서비스팩1 이 발표되었다. 개인적으로는 멀티 쓰레드일 때 무한으로 느려지는 버그와 여러 프로젝트를 동시에 debugger 에 붙였을 때 계속 하나의  프로젝트만 뜨는 버그가 수정되기를 바랬는데 이건 겪어봐야 하는 것이고, 일단 릴리즈 노트를 보니 C++ 에서는 아래와 같은 것들이 눈에 띄인다.

> FIX: The "catch by" reference does not work with the copy constructor that is defined in your Visual C++ .NET 2003 application
> - 복사 생성자가 있는 exception 을 catch 할 때 동작하지 않는 버그가 수정됨
> FIX: If you turn on optimization, your generated code may not be correct
> - 최적화 옵션을 켰을 때 코드가 이상해지는 버그가 수정됨
> FIX: Incorrect code is generated when you compile a Visual C++ .NET 2003 application that contains an inline method that accesses a static variable
> - static 변수에 접근하는 inline 멤버함수가 있을 때 이상한 버그가 수정됨
> FIX: Error message when you try to compile an application that is built by using Visual C++ .NET 2003: "Internal compiler error"
> - 컴파일 중 '컴파일러 내부 오류' 문제가 수정됨
> FIX: The strupr function may not convert strings to uppercase in Visual Studio .NET 2003
> - strupr 함수가 제대로 동작하지 않을 수 있는 버그가 수정됨
> You receive a "C1060: out of heap space" error message when you compile a very large project by using the Visual C++ .NET 2003 compiler
> - 'out of heap space' 문제... 'FIX' 라고 안되어 있는데... 해결되었다는 걸까요 -\_-
> FIX: Error message when you try to compile an application that is built by using Visual C++ .NET 2003: "Internal compiler error"
> - '내부 컴파일러 오류' 문제가 해결됨
> FIX: The IDE may unexpectedly close or crash when you try to copy an error message from the Task List window in Visual Studio .NET 2003
> - Task List 에서 에러 메시지를 복사할 때 crash 되는 문제 해결

ZViewer 다시 컴파일해서 테스트 후 릴리즈 해야겠다 ㅋㅋ

