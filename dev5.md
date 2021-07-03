# 목차
 - [프로젝트 기본 설정](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev1.md)
 - [메소드 패치](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev2.md)
 - [GUI 띄우기](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev3.md)
 - [모드 설정창](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev4.md)
 - **프로젝트 빌드**
 - [얼불춤 코드 보기](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev6.md)

## 프로젝트 빌드
모드를 다 만들었다면 이제 프로젝트를 빌드해야합니다.

## 1. 빌드
![빌드](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/raw/main/img/build.png?raw=true)     
맨 위 탭들에서 `빌드`를 누른 후 `솔루션 빌드`를 누르면 빌드가 됩니다.     
이게 귀찮다면 `Ctrl` + `Shift` + `B`를 누르면 바로 빌드가 됩니다.    
<br>
![성공](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/raw/main/img/comp.png?raw=true)
위 사진처럼    
`성공 1, 실패 0` 뜬다면 빌드 성공, 아니면 빌드 실패입니다   
빌드가 실패되도 문제되는 내용을 보여주니 차근차근 해보길 바랍니다    
<br>
빌드된 dll 파일은 `<프로젝트경로>/bin/Debug/프로젝트이름.dll`로 생깁니다.

## 2. Info.json 작성
UMM이 모드를 읽기 위해서는 Info.json이라는게 필요합니다    
바탕화면에서 우클릭 -> 새로 만들기 -> 텍스트 문서
방금 만든 문서 이름을 Info.json이라고 짓습니다.
|키|설명|
|------|---|
|Id|로그에 표시되는 이름, 모드를 구별하는 Id|
|DisplayName|실제로 표시되는 모드의 이름|
|Author|모드 개발자의 이름|
|Version|표시되는 모드의 버전|
|AssemblyName|불러올 어셈블리의 이름|
|EntryMethod|실행할 어셈블리의 메소드|   

가장 첫페이지에서 했던 Setup이 여기에 들어갑니다.

### 예시
```json
{
  "Id": "TestMOD",
  "DisplayName": "TestMOD",
  "Author": "Flower",
  "Version": "1.0.0",
  "AssemblyName": "Test.dll",
  "EntryMethod": "Test.Main.Setup"
}
```
다 작성했다면 저장합니다.

## 3. 폴더 생성
바탕화면에서 우클릭 -> 새로 만들기 -> 폴더    
이름을 자기가 원하는 모드의 이름으로 해줍시다     
    
만든 폴더안에 들어가고, 우클릭 -> 새로 만들기 -> 폴더    
이번에도 폴더의 이름을 자기가 원하는 모드의 이름으로 해줍니다     
    
그리고 그 폴더 안에다가 아까만든 Info.json 와 빌드한 어셈블리 파일을 여기로 옮깁니다.        
그럼 최종적으로 폴더는   
    
모드이름<br>
├── 모드이름<br>
│  &nbsp; &nbsp; ├── Info.json<br>
│  &nbsp; &nbsp; └── 모드이름.dll <br>
<br>
폴더를 가장 처음만든 바탕화면으로 돌아와 처음만든 폴더를 압축합니다   

## 4. 적용
![적용](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/raw/main/img/apply.png?raw=true)
UMM을 키고 압축한 파일을 모드로 적용하면 끝





[[⬅]](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev4.md) [[➡]](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/dev6.md) (5/6)
