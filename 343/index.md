LINK : fatal error LNK1201: error writing to program database "D:\\work\\Debug\\myprj.pdb"; check for insufficient disk space

 아직 Visual Studio C++ 6.0 을 쓸 일이 있어서, 이런저런 일을 하다보면, 정말 잘 알 수 없는 오류가 발생한다. 치명적인 내용인데도 6.0 에서는 이제 더 이상 지원이 안되니, 다음 버젼을 사용하라는 것도 있고, 다음 버젼에서는 고쳐졌지만 이런 방법으로 우회하라는 글도 있다.

 아마 이 오류 내용도 그 중의 하나일 것이다. 바로, xxx.pdb 파일의 용량이 65.5 메가를 넘으면, check for insufficient disk space 라는 에러를 낸다. 좀 큰 프로젝트를 만들어서 이런저런 라이브러리도 쓰고 그러면 이 용량이 넘어가는데, 아마 2byte 로 표현할 수 있는 65536 숫자 관련해서 문제가 있는 것 같다. 98년도에 VC++ 6.0 이 나온것으로 아는데, 아마 그 당시에는 저정도의 용량이면 충분했나보다.

 이 오류의 해결방법은 프로젝트 설정에서 C/C++ 탭, General 의 Category 에서 Debug info 를 Program database for Edit and continue 등으로 되어 있는 것을 Program database 로 바꿔서 pdb 파일의 크기를 줄이거나, C7 compatible 로 바꿔서 pdb 파일을 생성하지 않거나 하는 것이다.

관련 링크 : <http://msdn.microsoft.com/en-us/library/aa278576(v=vs.60).aspx>


