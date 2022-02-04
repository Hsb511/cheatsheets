# Espresso

The following code snippets are in Kotlin

```kotlin
onView(ViewMatcher)
    .perform(ViewAction)
  
onView(ViewMatcher)
    .check(ViewAssertion)
    
onData(ViewMatcher)
    .DataOptions
    .perform(ViewAction)
    .check(ViewAssertion)
```
    
## ViewMatchers

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

fun selectTabAtPostion(tabIndex: Int) = object: ViewAction {
    override fun getDescription() = "with tab at index $tabIndex"
    
    override fun getConstraints() = allOf(isDisplayed(), isAssignableFrom(TabLayout::class.java))
    
    override fun perform(uiController: UiController, view: View) {
        if (view is TabLayout) {
            (view.getTabAt(tabIndex)?: throw PerformException.Builder()
                .withCause(Throwable("No tab at index $tabIndex"))
                .build()
            ).select()
        }
    }
}
```

## ViewAssertions

## DataOptions
```kotlin
inAdapterView(Matcher)
atPosition(Integer)
onChildView(Matcher)
```

## Configuration
