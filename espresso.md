# Espresso

The following code snippets are in Kotlin

```kotlin
onView(ViewMatcher)             // Will try to find the view according to the ViewMatcher
    .perform(ViewAction)        // and then will perform the specified Action   
  
onView(ViewMatcher)             // Will try to find the view according to the ViewMatcher
    .check(ViewAssertion)       // and then will check the specified verification   

onData(ViewMatcher)             // load the data (in a ListView, GridView, Spinner, ...) in the 
    .DataOptions                // with UI options
    .perform(ViewAction)        // and then will perform the specified Action   
    .check(ViewAssertion)       // and then will check the specified verification   
```
    
## ViewMatchers

```kotlin
withId()
withText()
withContentDescription()

withParent(Matcher)
withChild(Matcher)
hasDescendant(Matcher)
isDescendantOf(Matcher)
isRoot()

isDisplayed()
isCompletelyDisplayed()
isEnabled()
isFocusable()
isTouchable()
isClickable()
isChecked()
isSelected()

allOf(Matcher)
anyOf(Matcher)
is(...)
not(...)

isAssignableFrom()
withClassName()

```

## ViewActions

```kotlin
click()
longClick()
pressBack()
closeSoftKeyboard()
openLink()

scrollTo()
swipeUp()

replaceText()
typeText()
clearText()
```

## ViewAssertions

```kotlin
matches(Matcher)
doesNotExist()

isLeftOf(Matcher)
isRightAlignedWith(Matcher)
isAbove(Matcher)
isBottomAlignedWith(Matcher)
```

## DataOptions

```kotlin
inAdapterView(Matcher)
atPosition(Integer)
onChildView(Matcher)
```

## Configuration

In yout app/build.gradle add the following import 
```kotlin
android {
    defaultConfig {
        testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"
    }
}

dependencies {
    androidTestImplementation('androidx.test.espresso:espresso-core:3.4.0')
    androidTestImplementation('androidx.test:runner:1.4.0')
    androidTestImplementation('androidx.test:rules:1.4.0')
}
```

You should have a default AndroidTest in `src/androidTest/java/com.example.package/`
