
## 목차
 - [프로젝트 기본 설정](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev1.md)
 - [메소드 패치](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev2.md)
 - **GUI 띄우기**
 - [모드 설정창](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev4.md)
 - [프로젝트 빌드](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev5.md)
 - [번외. 얼불춤 코드 보기](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev6.md)

## GUI 띄우기
 GUI를 띄우기 위해서는 UnityEngine.dll, UnityEngine-Core.dll, UnityEngine-IMGUI.dll, UnityEngine-UI.dll을 참조해야 합니다

## 1. 새 C# 파일 생성

[MonoBehaviour](https://docs.unity3d.com/ScriptReference/MonoBehaviour.html)를 상속하는 클래스를 하나 만들어야 합니다.    
그리고 안에다가 `OnGUI`라는 메소드를 추가합니다.
```c#
public class TestGUI : MonoBehaviour {
  public void OnGUI() {
  }
}
```

## 2. GUI, GUILayout
`GUI`와 `GUILayout`은 `OnGUI`에서만 가능한 친구들입니다       
`GUI`는 따로 위치를 설정해줘야 하지만 `GUILayout`은 레이아웃에서 위치를 자동으로 설정해줍니다     
     
만약 `GUI`로 텍스트 하나를 추가한다고 치면 `Rect`를 이용해 위치와 크기를 설정해야합니다.    
```cs
//GUI
GUI.Label(new Rect(x, y, 가로크기, 세로크기), 텍스트);
//GUILayout
GUILayout.Label(텍스트);
```
왼쪽위 기준으로 생성됩니다.   
   
버튼과 토글 또는 슬라이더같이 실시간으로 값이 변할수 있는 애들은 리턴값이 변한 값입니다
```cs
//버튼을 누르면 코드 실행
if(GUI.Button(new Rect(x,y,가로,세로), 텍스트) {
  //any code
}

float val = 값; //애는 전역변수로 설정

//슬라이더 값이 변하면 코드 실행
float newVal = GUI.HorizontalSlider(new Rect(x,y,가로,세로),val,최소값,최대값);
if(newVal!=val) {
  val = newVal;
  //any code
}
```
이런식으로 값이 변할때 코드를 실행할 수 있습니다
    
메소드가 너무 많아 하나하나 설명하기 힘들 정도니 궁금하다면 [GUILayout 문서](https://docs.unity3d.com/ScriptReference/GUILayout.html)와 [GUI 문서](https://docs.unity3d.com/ScriptReference/GUI.html)를 참고해주세요

## 3. GUIStyle
꼭 필요는 없지만 해당 UI를 꾸미고 싶다면 써야합니다
 - `<GUIStyle>.normal.textColor`로 텍스트 색상 지정
 - `<GUIStyle>.fontSize`로 텍스트 크기 지정
 - `<GUIStyle>.font`로 텍스트 폰트 지정
```cs
GUIStyle textStyle = new GUIStyle();
textStyle.fontSize = 50;
textStyle.alignment = TextAnchor.UpperCenter;
textStyle.normal.textColor = Color.white;
textStyle.font = RDString.GetFontDataForLanguage(RDString.language).font;
GUI.Label(new Rect(x,y,가로,세로), 텍스트, textStyle);
```

텍스트뿐만 아니라 다른 것도 가능하고 더욱 자세한건 [문서](https://docs.unity3d.com/ScriptReference/GUIStyle.html)를 참고해주세요

[[⬅]](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev2.md) [[➡]](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev4.md) (3/6)
