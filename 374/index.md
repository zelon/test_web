 AppWidget 은 <http://developer.android.com/guide/topics/appwidgets/index.html> 에 있는 것처럼 꽤 쉽게 개발을 시작할 수 있다. 하지만, 직접 개발하다보면 꽤 개발이 힘든데, 바로 UI 를 설정하지 못하고, RemoteViews 를 써야한다는 점과 몇몇 UI component 는 쓸 수 없다는 점에서 그렇다.
 그리고 개발 중에 계속 뭔가 이상하게 계속 broadcast receiver 가 제대로 동작하지 않아서 좀 고생했는데, 원인은 의외의 곳에 있었다. 바로 AppWidget 에서 처음에 한번 호출되는 onEnabled 함수가 제대로 호출되지 않는 것이다(이 함수 안에서 boradcast receiver 를 등록하고 있었음). 근데 이게 늘 호출안되었으면 바로 알았을건데, 개발 중에, re-install, 즉, 이미 내가 만든 AppWidget 이 떠있을 때 다시 설치(eclipse 에서는 그냥 Run As)를 하면 onEnabled 는 안 불린다는 것이다... -\_-;
 이미 설정되어 있는 AppWidget 을 길게 눌러서 휴지통에 버리고, 다시 AppWidget 을 Home Screen 에 넣어줘야 onEnabled 가 제대로 불린다. re-install 시에 이미 놓여진 AppWidget 을 자동으로 휴지통에 버려줬으면 당연히 다시 넣으면서 onEnabled 가 제대로 불렸을 건데 쩝... 자동으로 화면이 잘 업데이트되길래 제대로 로그 확인을 안해봐서 좀 헤맨듯 ㅠㅜ
**결론 : AppWidget 개발시에는 Run As 후, appwidget 을 휴지통에 넣었다가 다시 설정해줘야 onEnabled 가 제대로 호출된다. **

