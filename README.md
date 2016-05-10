## Why?
Android 개발 환경에서 테스트 주도 개발을 효과적으로 하기 위해서 정리

##Mockito
- 현재 가장 많이 쓰고 있는 Mock object 기반의 라이브러리
- testCompile "org.mockito:mockito-core:1.+"
- http://mockito.org

```java
import static org.mockito.Mockito.*;

// mock creation
List mockedList = mock(List.class);

// using mock object - it does not throw any "unexpected interaction" exception
mockedList.add("one");
mockedList.clear();

// selective, explicit, highly readable verification
verify(mockedList).add("one");
verify(mockedList).clear();
```

```java
// you can mock concrete classes, not only interfaces
LinkedList mockedList = mock(LinkedList.class);

// stubbing appears before the actual execution
when(mockedList.get(0)).thenReturn("first");

// the following prints "first"
System.out.println(mockedList.get(0));

// the following prints "null" because get(999) was not stubbed
System.out.println(mockedList.get(999));
```


##Espresso

- 2013. 10월부터 구글이 발표한 Testing Fraemwork 라이브러리
- 2.0 버전 이후로 Android Support Respository 에 추가 됨
- https://google.github.io/android-testing-support-library/docs/espresso/

## ActivityRule
- 기존에 ActivityInstrumentationTestCase2 대신 사용하는 방식 인듯 
- https://github.com/googlesamples/android-testing/blob/a90b01825cd0e8ef182e2fa676847ae5545368f9/runner/AndroidJunitRunnerSample/app/src/androidTest/java/com/example/android/testing/androidjunitrunnersample/OperationHintLegacyInstrumentationTest.java
- http://developer.android.com/intl/ko/reference/android/support/test/rule/ActivityTestRule.html

``` java
@RunWith(AndroidJUnit4.class)
@LargeTest
public class HelloWorldEspressoTest {

    @Rule
    public ActivityTestRule<MainActivity> mActivityRule = new ActivityTestRule(MainActivity.class);

    @Test
    public void listGoesOverTheFold() {
        onView(withText("Hello world!")).check(matches(isDisplayed()));
    }
}
```

 

