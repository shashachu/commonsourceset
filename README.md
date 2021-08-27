When moving from one product flavor to more than one product flavor, the `commonSourceSet$kotlin_gradle_plugin` input file set changes, even if you are building the same flavor.

# Repro
* Run `./gradlew assembleFlavor1Debug`
* Open `app/build.gradle` and uncomment the `flavor2` block
* Run `./gradlew assembleFalvor1Debug`
* Note that `:app:compileFlavor1DebugKotlin` is not up-to-date despite no code changing and running the same flavor.

A build scan reports:
```
The task was not up-to-date because of the following reasons:	
Input property 'commonSourceSet$kotlin_gradle_plugin' file app/src/debug/java has been added.	
Input property 'commonSourceSet$kotlin_gradle_plugin' file app/src/debug/java/com has been added.	
Input property 'commonSourceSet$kotlin_gradle_plugin' file app/src/debug/java/com/pinterest has been added.
```