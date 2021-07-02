# 메소드 패치
모든 모드들은 메소드(함수)를 패치(수정) 하기 위해서 `0Harmony.dll`을 사용합니다      
이전 페이지에서 이미 하모니를 참조했으니 `import 대충하모니`로 임포트 해줍시다

## 1. HarmonyPatch 
`Harmony`는 런타임에 닷넷 코드를 수정할 수 있게 도와주는 라이브러리입니다.     
여러 패치의 실행 순서나, 함수 자체의 내부 코드를 수정할 수 있는 기능을 지원합니다.

보통 모드들은 패치할때 `HarmonyPatch` 라는 애트리뷰트를 사용합니다.    
```c#
[HarmonyPatch(typeof(클래스_이름),"메소드_이름")]
```

## 2. Prefix? Postfix??
다른 모더분의 모드 코드를 한번쯤 봤다면 보섰을만한 애들입니다.

`Prefix`는 해당 메소드가 실행되기 전에 밑 코드를 실행하게 해줍니다.     
반대로 `Postfix`는 해당 메소드가 실행되고 난 후 밑 코드를 실행합니다.

```c#
[HarmonyPatch(typeof(클래스_이름),"메소드_이름")]
public static class Test {
  public static void Prefix() {
  }
}
```
위에 Test같은 클래스는 이름을 아무렇게나 막 지으셔도 상관없습니다.

## 3. 하모니 메소드의 리턴타입
일반적으로 모드 개발을 할때는 메소드 리턴타입을 `void`로 합니다    
하지만 원하는 상황에 따라 `bool`이 될 수도 있습니다.    
`false`를 반환하면 거기서 끝, 원본 메소드가 실행되지 않습니다. ( Prefix 일때 )  

```c#
public static class TestClass {
  //패치할 테스트 메소드
  public staic void Test(){
    Console.WriteLine("안녕 세상!");
  }
}

public static class PatchTest {

  [HarmonyPatch(typeof(TestClass),"Test")]
  public static class TestReturn {
    public static bool Prefix() {
      //any code
      return false;
      //원본 메소드 실행을 막음으로써 "안녕 세상!"은 로그에 써지지 않음
    }
  }

}
```
       
그럼 이런 의문이 들수있습니다 "왜 `Prefix`에서 해야되나요?"      
아까도 말했다시피 `Prefix`는 원본 메소드가 실행되기 전입니다. `Postfix`를 사용해봤자 이미 원본 메소드는 실행된 후 이므로 `false`를 반환해도 의미가 없습니다.

## 4. 하모니 메소드의 매개변수(파람미터)
하모니 메소드의 매개변수에는 많은 것들이 들어갈 수 있습니다.    
    
 - 가장 많이 쓰는 `__instance`, 말 그대로 인스턴스를 가져옵니다.  
 - `___필드이름`, `private`이어도 해당 필드를 가져옵니다.  
 - `__원본-메소드의-매개변수-이름`, 인수를 가져옵니다.
```c#
public static class OriginalClass {
  public static int a = 1;
  private static string pri = "private";

  public static void start() {
    Test(1);
  }
  public static void Test(int n){
  }
  public static void ASDF(){
    Console.WriteLine("asdf");
  }
}

public static class PatchClass {

  [HarmonyPatch(typeof(OriginalClass),"Test")]
  public static class Test {
    public static void Prefix(OriginalClass __instance, string ___pri, int __n) {
      __instance.ASDF();
      Console.WriteLine(__instance.a); //result - 1
      Console.WriteLine(___pri); //result - private
      Console.WriteLine(__n); //result - 1
    }
  }
}
```
 - `__result`, 원본 메소드의 리턴값을 바꿀수 있습니다.
```c#
public static class OriginalClass {
  public static int Add(int a, int b){
    return a+b;
  }
}

public static class PatchTest {
  [HarmonyPatch(typeof(OriginalClass),"Add")]
  public static class Test {
    //return false 이용
    public static bool Prefix(ref int __result) {
      __result = 5;
      return false;
    }
    //Postfix를 이용해 이렇게도 가능
    public static void Postfix(ref int __result) {
      __result = 5;
    }
    //둘 중 아무거나 해도 상관없음
  }
}
```
"ref는 왜 사용하나요?" 같은 의문이 들수도 있습니다 그 까닭은 ref 키워드를 사용해야 변경된 값을 전달할수 있습니다



[[⬅]](https://github.com/NoBrain0917/ADOFAI-Mod-Development-Guide/blob/main/README.md) [➡] (2/5)
