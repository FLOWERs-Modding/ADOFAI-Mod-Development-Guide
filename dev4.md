## 목차
 - [프로젝트 기본 설정](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev1.md)
 - [메소드 패치](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev2.md)
 - [GUI 띄우기](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev3.md)
 - **모드 설정창**
 - [프로젝트 빌드](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev5.md)
 - [얼불춤 코드 보기](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev6.md)

## 모드 설정창 
![설정창](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/img/setting.png?raw=true)   
와 같이 만들 수 있습니다

## 1. OnGUI
[프로젝트 기본 설정](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev1.md)에서 만들었던 Main.cs로 돌아가고 `OnGUI` 를 만들어 줍니다. 
```cs
private static void OnGUI(UnityModManager.ModEntry modEntry)
{
}

```
`OnGUI`안에는 GUI보단 GUILayout을 쓰는 것을 추천합니다.  
나머지는 [앞 페이지](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev3.md)에서 했던거와 같이 해주시면 됩니다.

## 2. OnSaveGUI
`ShowBPM`처럼 뭔가를 저장해야할 때가 생길때 OnSaveGUI를 씁니다.    
마찬가지로 Main.cs에 `OnSaveGUI`를 추가합니다.
```cs
private static void OnSaveGUI(UnityModManager.ModEntry modEntry)
{
}
```
그리고 대충 Setting 이라고 이름짓고 새 클래스를 생성합니다.   
새로 만든 이 클래스를 UnityModManager.ModSettings에 상속하고 아래와 같이 몇개를 추가합니다
```cs
public class Setting : UnityModManager.ModSettings
{

  public override void Save(UnityModManager.ModEntry modEntry) {
    var filepath = GetPath(modEntry);
    try {
      using (var writer = new StreamWriter(filepath)) {
        var serializer = new XmlSerializer(GetType());
        serializer.Serialize(writer, this);
      }
    } catch {
    }
  }
       
  public override string GetPath(UnityModManager.ModEntry modEntry) {
    return Path.Combine(modEntry.Path, GetType().Name + ".xml");
  }
  
}
```

