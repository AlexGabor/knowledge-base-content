Notes on: [It's complicated, but it doesn't have to be: a Dagger journey by Fred Porciuncula](https://www.youtube.com/watch?v=9fn5s8_CYJI)

## Why dagger?

* compile time safety
* scalability 
* performance
* no boilerplate? (apperently started simpler)

It's verbose for small project, but pays off on the long run.

He claims that it can be simplified so smaller projects can benefit.
## Tips

* Tip #1: Use construction injection
* Tip #2: @Singleton is expensive, use @Reusable if possible
* Tip #3: Avoid member injection
* Tip #4: Always go for static @Provide methods (`@JvmStatic` in kotlin)
* Tip #5: Use `@Component.Factory`
* Tip #6: Control scope with ViewModels
* Tip #7: Take advantage of AssisteInject

Two ways for getting things from dagger:
* property in component 
    * pros: you can put the result in a `val`
    * cons: each one must be declared in the component
* `inject()` method
    * pros: only one method per injected class
    * cons: injected fields are now `public lateinit var`

Nice extensions to hide the cast [14:46](https://youtu.be/9fn5s8_CYJI?t=886)

## @Subcomponent
* pros: 
    * encapsulate dependencies the are used only in a specific part of the app
    * scoping ex: `@ActivityScope`, `@FragmentScope` to make dependecies live in their lifecycle 
* cons: 
    * You need to create modules for things you could use constructor injection
    * For every activity you have to create a supcomponent with module 

## dagger-android
* Greate for setup 
* Still verbose
* Real DI (you hide the injector so you don't access it in an activity)
* Member injection
* Decouples injection sites from injector

## ViewModel 
[25:40](https://youtu.be/9fn5s8_CYJI?t=1540)
Scope things with the view model instead of with subcomponent to keep things simple.

Nice extensions to get view models from dagger

Use AssistedInject 

Take #3 and #6 with a grain of salt; opinionated; depends on what you're doing.

[example repo](https://github.com/tfcporciuncula/dagger-journey)