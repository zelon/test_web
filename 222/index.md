 Makefile 로 빌드에 관심을 가지면서 의존성 문제는 이상하게 해결하기 힘든 것이었다. Visual Studio 에서는 알아서 잘(!) 해주는 데, 리눅스에서 간단한 프로그래밍을 하거나, eclipse 에서 MingW 를 이용해서 뭔가 해보려면 꼭 이 문제가 마음에 걸렸다.
 기숙사에 있을 때 제윤이형과 함께 이 얘기를 하다가 [이 책](http://kangcom.com/common/bookinfo/bookinfo.asp?sku=200204290004)을 보라고 해서 gcc 에 -M 이란 옵션이 있는 것을 알았고, 얼마전에 문득 ZViewer 를 mingw 로 컴파일 해보기로 했고, 다시 Makefile 에 의존성을 넣는 것을 해봤다.
 일단 시작은 [kldp에서의 글](http://kldp.org/node/39429)이다. 잘 만들어진 makefile 을 얻을 수 있다. 하지만 난 환경이 윈도우 환경이라서 약간의 수정이 필요했고, 이것저것 찾아보면서 고쳤다.

>     CC          = gcc
>     CXX         = g++
>     INC         = -I"lib" -I"ZViewer\res" -I"ZViewer" -I"commonSrc"
>     LIBS        =
>     CFLAGS      = -DUNICODE -D_WINDOWS_ -D_UNICODE -D_WIN32_IE=0x0500
>     #CFLAGS      = -Wall -Winline -DDEBUG -ggdb
>
>     # import from cpp list
>     -include srclist.txt
>
>     #RESS        = $(HOME_DIR)\res\ZViewer.rc
>     RESS        =
>     TARGET = ZViewer.exe
>
>     CRES = $(RESS:.rc=.rco)
>     OBJS = $(SRCS:.cpp=.o)
>     DEPS = $(SRCS:.cpp=.d)
>     DEPS += $(PREDEPS)
>
>     PRECOMPILED_HEADER = ZViewer\stdafx.h
>     PRECOMPILED_HEADER_OUTPUT = $(PRECOMPILED_HEADER:.h=.h.gch)
>     PREDEPS = ZViewer\stdafx.h.d
>
>     .PHONY : clean new all $(TARGET)
>
>     all:$(TARGET)
>
>     srclist.txt: ConvertFromVCProj.py
>      @echo Creating source files list...
>      @python ConvertFromVCProj.py > srclist.txt
>
>     $(TARGET):$(PRECOMPILED_HEADER_OUTPUT) srclist.txt $(OBJS) $(CRES)
>      @echo "CREATE [$@]"
>      @$(CXX) -o $@ $(PRECOMPILED_HEADER_OUTPUT) $(OBJS) $(CRES)
>       @echo [OK] Build Completed
>
>     $(PRECOMPILED_HEADER_OUTPUT): $(PRECOMPILED_HEADER) $(PRECOMPILED_HEADER:.h=.d)
>        @echo Compile Precompiled header
>         @$(CXX) -x c++-header $(PRECOMPILED_HEADER) -o $(PRECOMPILED_HEADER_OUTPUT) $(INC) $(CFLAGS)
>
>     clean:
>       @del /Q $(PRECOMPILED_HEADER_OUTPUT) $(OBJS) $(DEPS) $(TARGET) core 2> NUL
>        @echo [OK] cleaned
>
>     new: 
>      @$(MAKE) -s clean
>        @$(MAKE) -s
>
>     %.rco:%.rc
>        @echo Compile RC $< to $@
>         cd $(HOME_DIR)\res
>       windres $< -o $@
>      cd $(HOME_DIR)
>
>     %.o:%.cpp
>      @echo $<
>      @$(CXX) $(INC) $(CFLAGS) -c $< -o $@
>
>     %.d:%.cpp
>         @echo Dependency Reset $<
>         @$(CXX) -MM $(INC) $(CFLAGS) $< > $@.$$$$
>      @sed "s,\($(basename $(notdir $@))\)\.o[ :]*,$(subst \,\\,$(basename $@)).o $(subst \,\\,$@) : ,g" < $@.$$$$ > $@
>      @del /Q $@.$$$$
>
>     # h 면 precompiled header 뿐이다.
>     $(PREDEPS):$(PRECOMPILED_HEADER)
>         @echo Precompiled header Dependency Reset $< to $@
>        @$(CXX) -MM $(INC) $(CFLAGS) $< > $@.$$$$
>      @sed "s,\($(basename $(basename $(notdir $@)))\)\.o[ :]*,$(subst \,\\,$(PRECOMPILED_HEADER_OUTPUT)) $(subst \,\\,$@) : ,g" < $@.$$$$ > $@
>      @del /Q $@.$$$$
>
>     -include $(DEPS)

 소스가 조금 짤리는데, 긁어서 Ctrl+C,V 해서 보거나,  이렇게 만들어진 ZViewer 의 MingW+gcc 윈도우용 버젼은 [\[kldp.net의 ZViewer 소스\]](http://kldp.net/plugins/scmsvn/viewcvs.php/trunk/ZViewer/Makefile?rev=507&root=zviewer&view=markup)에서 볼 수 있다.(하지만 아직 소스 차원의 문제(VC와 gcc 의 함수 지원등) 때문에 빌드는 안된다 ;;)
 ZViewer 의 Makefile 에서 바뀐 것은 -M 옵션을, -MM 으로 바꾸어서, 시스템 헤더 파일들은 의존성에서 뺐다. 시스템 헤더는 보통 다시 수정하지 않기 때문이다.
 precompiled header 를 추가했다. 이 부분은 약간의 최적화가 필요할 듯도 한데, 일단 [gcc 에서의 precompiled header 기능](http://www.wimy.com/wiki/wiki.php/linuxProgramming#s-4)을 활용해보고자 넣어보았다.
 Makefile 에 gcc 외에 sed 라는 프로그램이 실행되는 것을 볼 수 있는데, 이건 정규식을 통해서 치환을 하는 것이다. 관련 내용은 [여기](http://web.cecs.pdx.edu/%7Ekya/wiki/GNUMake#s-1.4.1)에서 찾아볼 수 있다.
 중간에 python [ConvertFromVCProj.py](http://kldp.net/plugins/scmsvn/viewcvs.php/trunk/ZViewer/ConvertFromVCProj.py?rev=507&root=zviewer&view=markup) 라는 부분은, Visual Studio .NET 2005 의 vcproj 에서 cpp 파일들을 뽑아주는 간단한 스크립트이다. 즉 ZViewer 의 Makefile 은 .NET 2005 의 vcproj 에서 cpp 목록을 뽑아서 컴파일을 하게 된다.(아직 주개발 tool 이 Visual Studio이다)
ps : [유능한 후배의 글](http://kkamagui.tistory.com/605)을 보고, 도움이 될까해서 얼마전에 있었던 일을 정리해봄 ^^

