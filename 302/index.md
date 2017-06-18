 우연히 유뷰브 동영상을 다운받는 프로그램의 소스를 보게 되어서 파이썬으로 직접 코드를 짜면서 따라가보았다. 생각보다 간단하지만, 한단계를 거쳐서 가야해서 조금 번거롭기는 하다. 다음과 같은 과정으로 플래시 동영상 파일인 flv 파일을 다운받을 수 있다.

1.  원하는 video id 를 얻는다. 이건 보통 play 하는 url 에, v=???? 라며 적혀있다.
2.  특정 url 에 원하는 video id 를 넣어서 토큰(token)이라는 걸 얻는다.
3.  다시 특정 url 에 원하는 video id 와 앞에서 얻은 토큰을 얻어서 다운로드를 한다.

 파이썬으로 만들어본 코드는 다음과 같다. 가장 간단한 과정을 모두 보여주므로, win32 나 C\# 으로 이 과정대로 따라 만들면 쉽게 만들 수 있을것 같다.

> import urllib
> import re
> def testmain():
>     videoid = "KIvwdpYII7s"
>     url = u"http://www.youtube.com/get\_video\_info?video\_id=%s&el=embedded&ps=default&eurl=" % videoid
>     f = urllib.urlopen(url)
>     info = urllib.unquote(f.read())
>     r = "token=(.\*?)&"
>     token = re.findall(r, info)\[1\]
>     downloadurl = u"http://www.youtube.com/get\_video?video\_id=%s&t=%s&eurl=&el=embedded&ps=default" % (videoid, token)
>     downloadWebRequest = urllib.urlopen(downloadurl)
>     outfile = open("a.flv", "wb")
>     outfile.write(downloadWebRequest.read())
>     outfile.close()
>    
> if \_\_name\_\_ == "\_\_main\_\_":
>     testmain()

 pop.wimy.com 와 연계하면 재미있는 프로그램이 나올수도 있을것같다 ^^

