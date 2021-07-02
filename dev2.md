# 메소드 패치
모든 모드들은 메소드(함수)를 패치(수정) 하기 위해서 `0Harmony.dll`을 사용합니다      
이전 페이지에서 이미 하모니를 참조했으니 `import 대충하모니`로 임포트 해줍시다

## 1. HarmonyPatch 
보통 모드들은 패치할때 `HarmonyPatch` 라는 애트리뷰트를 사용합니다.    
```c#
[HarmonyPatch(typeof(클래스_이름),"메소드_이름")]
```

## 2. Prefix? Postfix??
다른 모더분의 모드 코드를 한번쯤 봤다면 보섰을만한 애들입니다     
`Prefix`는 해당 메소드가 실행되기 전에 밑 코드를 실행하게 해줍니다.     
반대로 `Postfix`는 해당 메소드가 실행되고 난 후 밑 코드를 실행합니다.

```c#
[HarmonyPatch(typeof(클래스_이름),"메소드_이름")]
public static class Test {
  public static void Prefix() {
  }
}
```
위에 Test같은 클래스는 이름은 아무렇게나 막 지으셔도 상관없습니다.
