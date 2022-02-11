# Espresso examples

The following code snippets are in Kotlin

## ViewMatchers

```kotlin
fun withBackground(@DrawableRes id: Int) = object: TypeSafeMatcher<View>() {
    override fun describeTo(description: Description) {
        description.appendText("View with background with id $id")
    }
    
    override fun matchesSafely(view: View) = view.background.sameBitmap(view.context,id)
}

// Should be put in a DrawableExtensions
fun Drawable.sameBitmap(context: Context, resourceId: Int): Boolean {
    var currentDrawable: Drawable = this
    var expectedDrawable = ContextCompat.getDrawable(context, resourceId)

    if (currentDrawable is StateListDrawable && expectedDrawable is StateListDrawable) {
        currentDrawable = this.current
        expectedDrawable = expectedDrawable.getCurrent()
    }
    if (currentDrawable is BitmapDrawable) {
        val bitmap = currentDrawable.bitmap
        val otherBitmap = (expectedDrawable as BitmapDrawable).bitmap
        return bitmap.sameAs(otherBitmap)
    }

    if ((currentDrawable is VectorDrawable && expectedDrawable is VectorDrawable) ||
        (currentDrawable is VectorDrawableCompat && expectedDrawable is VectorDrawableCompat) ||
        (currentDrawable is GradientDrawable && expectedDrawable is GradientDrawable)) {
        return this.current.drawableToBitmap()!!.sameAs(expectedDrawable.current.drawableToBitmap())
    }
    return false
}


fun Drawable.drawableToBitmap(): Bitmap? {
    if (this is BitmapDrawable && this.bitmap != null) {
        return this.bitmap
    }
    val bitmap: Bitmap = if (this.intrinsicWidth <= 0 || this.intrinsicHeight <= 0) {
        Bitmap.createBitmap(1, 1, Bitmap.Config.ARGB_8888) // Single color bitmap will be created of 1x1 pixel
    } else {
        Bitmap.createBitmap(this.intrinsicWidth, this.intrinsicHeight, Bitmap.Config.ARGB_8888)
    }
    val canvas = Canvas(bitmap)
    this.setBounds(0, 0, canvas.width, canvas.height)
    this.draw(canvas)
    return bitmap
}

```

## ViewActions

```kotlin
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
