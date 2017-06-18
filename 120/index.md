 최근 홈페이지의 인코딩을 euc-kr 에서 utf-8 기반의 유니코드로 변경했습니다. 제 홈페이지가 모니위키 + 태터툴즈의 조합으로 운영되고 있었는데, 태터툴즈는 utf-8 을 쓰고 있었고, 모니위키는 euc-kr 를 쓰고 있었습니다. 그런데 최근 서버를 데비안에서 우분투로 업데이트하면서 기본이 utf-8 이 되어서 ssh 접속을 해도 utf-8 이 기본이 좋고, 위키와 블로그의 공통 메뉴에 '한글' 을 쓰려고 하니 아무래도 utf-8 로 인코딩을 통일하는게 좋을것 같더군요.
 그래서 모니위키를 utf-8 로 변경하게 되었습니다. 기본 작업 과정은
1. 한글 페이지 이름을 영문 페이지 이름으로 변경하기
 일단 url 이 이상해지는 것도 막고, 인코딩이 혹시나 잘못되더라도 영어면 알아보기 쉽죠. -0-
2. euc-kr 한글로 되어 있는 다른 페이지들을 될 수 있는 한 임시로 영어로 변경. 1과 같은 이유
3. 다음과 같은 명령어를 통해 각 페이지의 파일들을 euc-kr 에서 utf-8 로 변경
iconv inFile -f euc-kr -t utf-8 -o outFile
 하지만 위와 같은 것을 전체 파일에 해주기 위해서 다음과 같은 간단한 파이썬 작성.

> import os
> import glob
> def main():
>         files = glob.glob("\*")
>         for file in files:
>                 if os.path.isfile(file):
>                         cmd = "iconv " + file + " -f euc-kr -t utf-8 -o \_\_tmp"
>                         os.system(cmd)
>                         print(cmd)
>                         cmd = "cp \_\_tmp " + file
>                         os.system(cmd)
>                         print(cmd)
>                         os.system("rm \_\_tmp")
> if \_\_name\_\_ == "\_\_main\_\_":
>         main()

 4. 위키 디렉토리의 설정 파일인 config.php 를 열어서 $charset='euc-kr'; 로 되어 있던 것을  $charset='utf-8'; 로 변경
5. 제대로 나오는 지 테스트~
 일단 위의 과정을 거치기 전에 data/text 의 내용을 백업해주는 것을 잊지 말아야 한다. 그리고 RCS 디렉토리의 내용을 변환하지 않아서 지난 버젼은 여전히 인코딩이 다르게 남아있긴 한데, 이 부분은 그냥 패쓰 -0-

