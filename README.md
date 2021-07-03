# 얼불춤 모드 개발 가이드

## 잠깐만요!
 혹시 모드 설치 방법을 찾는거라면 [UMM 설치 가이드](https://github.com/CrackThrough/ADOFAI-Mod-Installation-Guide/blob/main/kor/use-1.md) 와 [모드 적용 가이드](https://github.com/CrackThrough/ADOFAI-Mod-Installation-Guide/blob/main/kor/use-2.md)를 참고해주세요
 
## 목차
 - **프로젝트 기본 설정**
 - [메소드 패치](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev2.md)
 - [GUI 띄우기](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev3.md)
 - [모드 설정창](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev4.md)
 - [프로젝트 빌드](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev5.md)
 - [얼불춤 코드 보기](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev6.md)

## 1. 시작 전 준비물
 - [Visual Studio 2019](https://visualstudio.microsoft.com/ko/vs/)
 - 얼불춤 ( UMM이 설치된 상태 )
 - [.NET Framework 4.8](https://go.microsoft.com/fwlink/?linkid=2088517)
 - [dnspy](https://github.com/dnSpy/dnSpy/releases/download/v6.1.8/dnSpy-net-win64.zip)

## 2. 프로젝트 생성
![프로젝트생성](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/img/make.png?raw=true)
새 프로젝트 만들기 클릭     
    <br>
![선택](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/img/select2.png?raw=true)
클래스 라이브러리 (.NET Framework) 선택 후 다음 클릭     
프레임워크는 4.8을 추천합니다     
만약 클래스 라이브러리가 없다면 Visual Studio Installer에서 .NET 데스크톱 개발을 설치해 주세요    

## 3. 레퍼런스 참조
![참조](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/img/add.png?raw=true)      
맨 오른쪽에 있는 탭들중 `참조` 우클릭후 `참조 추가` 클릭    
    
`찾아보기`를 누른 후 아래에 있는 항목들을 모두 참조해주세요.
 - <얼불춤경로>/A Dance of Fire and Ice_Data/Managed/UnityModManager/0Harmony.dll
 - <얼불춤경로>/A Dance of Fire and Ice_Data/Managed/UnityModManager/UnityModManager.dll
 - <얼불춤경로>/A Dance of Fire and Ice_Data/Managed/Assembly-CSharp.dll


## 4. 셋업 만들기
![탭들](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/img/tabs.png?raw=true)     
프로젝트 생성될때 같이 생긴 Class1.cs을 우클릭 후 이름을 바꿔서 Main.cs라고 지정해주고 정적으로 해줍니다.
```cs
public static class Main
{
}
```
그리고 Setup, OnToggle이라는 메소드도 같이 만들어줍니다.      
Setup은 UMM이 이 모드를 실행할때 처음 시작하는 메소드입니다.

```cs
public static class Main
{
  public static UnityModManager.ModEntry.ModLogger Logger;
  public static Harmony harmony;
  public static bool IsEnabled = false;
  
  internal static void Setup(UnityModManager.ModEntry modEntry)
  {
    Logger = modEntry.Logger;
    modEntry.OnToggle = OnToggle;
  }
  
  private static bool OnToggle(UnityModManager.ModEntry modEntry, bool value)
  {
    IsEnabled = value;
    
    if (value)
    {
      //켜질때
      harmony = new Harmony(modEntry.Info.Id);
      harmony.PatchAll(Assembly.GetExecutingAssembly());
    }
    else
    {
      //꺼질때
      harmony.UnpatchAll(modEntry.Info.Id);
    }
  }
}
```

### Setup을 public이 아닌 internal로 하는 이유?
public은 프로젝트 내에서만 접근이 가능합니다, UMM은 외부 프로젝트에서 접근하기 때문에 internal을 사용해야합니다

[X] [[➡]](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev2.md) (1/6)
