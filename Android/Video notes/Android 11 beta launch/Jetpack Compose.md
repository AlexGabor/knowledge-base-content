# Jetpack Compose

## Some code

```kotlin
@Composable // To create an Widget
fun ProductLabel(product: Product) { // accepts some input
    Text("${product.quantity}x ${product.name}") // can call other composable functions
}
```

* `@Composable` changes the type of the function
* Can only be called from other composable functions
* Composable functions take data and transform it into UI
* Advantage is you can use kotlin logic:


```kotlin
@Composable 
fun ProductLabel(product: Product) { 
    Column {
        for (i in product.quantity) {
            Text("${product.name}") 
        }
    }
}
```

* It also supports state:

```kotlin
@Composable 
fun ProductFilter(products: List<Product>) { 
    val filter by state { "" }

    FilledTextField(
        value = filter,
        onValueChange = { filter = it },
        label = { Text("Name:") }
    )

    for (product in products) {
        if (product.name.contains(filter)) {
            ProductLabel(product)
        }
    }
}
```

## Tech Stack

Development Host:
* Android Studio
* Compose Compiler Plugin
* Kotlin Compiler

Device
* Compose UI Material (material design components)
* Compose UI Foundation (standard layouts)
* Compose UI Core (input Management, measurement, drawing, layout)
* Compose Runtime (doesn't know about Android an UI)

## What's new in Developer preview 2

* Interactive preview for composable widgets in Android Studio
* Modifiers: decorate single element to supply layout params and behavior ([code](https://www.youtube.com/watch?v=U5BwfqBpiWU&feature=youtu.be&t=520))
ll
* RecyclerView alternative with support for LiveData, RxJava, Flow:
```kotlin
@Composable
fun ShoppingCart(shoppingCart: LiveData<List<Product>>) {
    val products by shoppingCart.observerAsState(emptyList())
    AdapterList(data = products) { product ->
        ShoppingCartItem(product)
    }
}
```
* ContraintLayout with compose ([code](https://www.youtube.com/watch?v=U5BwfqBpiWU&feature=youtu.be&t=770))
* Animation with compose ([code](https://youtu.be/U5BwfqBpiWU?t=908))
* Interoperability with Views ([code](https://www.youtube.com/watch?v=U5BwfqBpiWU&feature=youtu.be&t=1091))
* Testing ([code](https://youtu.be/U5BwfqBpiWU?t=1202))

## Roadmap

* Alpha in Summer 2020
* 1.0 in 2021

## Resources

* [developer.android.com/jetpack/compose](developer.android.com/jetpack/compose)
* [github.com/android/compose-samples](github.com/android/compose-samples)
* slack.kotlinlang.org (#compose)
* [issues tracker](issueTracker.google.com/issues/new?component=612128)
* Check what's coming [android-review.googlesource.com](android-review.googlesource.com)