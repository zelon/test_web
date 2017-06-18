<img src="openmaru.png" width="179" height="52" />
<http://channy.creation.net/blog/792>
 요약하자면, NC소프트에서 야심차게 추진했던 웹서비스들이 수익이 없다는 이유로 점점 힘을 잃어가며, 몇몇 서비스들은 문을 닫고 있다는 이야기이다. 내가 주로 쓰는 스프링노트도 지금 문닫는건 아니지만, 사실 스프링노트 업데이트 안된지도 오래되었고...([공식 블로그](http://blog.openmaru.com/ "[http://blog.openmaru.com/]로 이동합니다.")에는 약 1년전의 포스팅이 마지막이다)
 나의 많은 위키 문서들이 저장된 스프링노트의 앞날도 사실 불투명하다는 얘기이다. 그래서 결심한게, '구글 문서로 옮겨야겠다.' 이다. 구글 문서는 원래 안되었던 이유가 첨부파일이 안된다는 거였는데, 링크 걸기가 조금 복잡하겠지만 이제 업로드도 잘되고...
 구글 문서는 업로드도 불편하고, 한글 글꼴 제대로 지원 안해주고, 나 아닌 다른 사용자는 검색도 안되지만,
 구글 문서는 프레젠테이션 기능도 제대로 지원해주고, 그림 그리는 기능도 되고 <span style="font-weight: bold;"><span style="font-size: 14pt;">앞으로 발전 가능성이 풍부</span></span>하다. 즉, 앞의 단점들이 해결될 수 있다는 가능성이 있다는 것이다.
 그래서 구글 문서로 옮기기로 했다. 총 200여 페이지를 어떻게 옮길까 고민을 하다가, '백업을 받은 후 html 파일들을 구글 문서의 업로드 기능을 통해 옮기자' 라고 생각했는데, 백업받은 압축 파일을 풀면, 폴더 구조를 그대로 가져서, 결과적으로 여러 폴더에 index.html 이라는 이름으로 있었다. 그래서 다음과 같은 간단한 파이썬 스크립트를 만들어서 한 곳에 '문서 이름.html' 라는 이름으로 옮기고, 빈 폴더들은 지워버렸다. 비어있지 않은 폴더들에는 이미지 파일들과 각종 첨부 파일들이 있어서 이건 수동으로 해결하기로 했다.
 결과적으로 한 곳으로 모든 html 파일들을 구글 문서에 한번에 선택해서 올리고, 이미지 파일과 첨부 파일은 좀 귀찮지만 몇개 안되어서 수동으로 문서에 넣어줬다.

> import os
> def testmain():
>    
>     for root, dirs, files in os.walk("."):
>         print(root)
>        
>         if root != ".":
>             for file in files:
>                
>                 if file == "index.html":
>                     originalFilename = root + os.path.sep + file
>                     newFilename = "." + root\[root.rindex("\\\\"):\] + ".html"
>                     newFilename = newFilename.replace("\_", " ")
>                    
>                     print("Move from %s to %s" % (originalFilename, newFilename))
>                    
>                     os.rename(originalFilename, newFilename)
> def deleteEmptyDir():
>     print("Delete empty dirs")
>     while True:
>         deleteCount = 0
>         for root, dirs, files in os.walk("."):
>             if len(files) == 0 and len(dirs) == 0:
>                 print("To delete dir : " + root)
>                
>                 try:
>                     os.rmdir(root)
>                     deleteCount = deleteCount + 1
>                 except WindowsError, msg:
>                     print(msg)
>                
>                
>         if deleteCount == 0:
>             break
>        
>     print("End of deleting empty dirs")
>  
> if \_\_name\_\_ == "\_\_main\_\_":
>     testmain()
>    
>     deleteEmptyDir()

 꽤 멋진 국내 서비스 하나가 위태로워져서 아쉽지만... 이제 내 자료 백업할 때 (구글 문서 + 스프링노트)를 백업하던게, 구글 문서만 백업하면 되어서 백업하기는 쉬워졌다;;;

