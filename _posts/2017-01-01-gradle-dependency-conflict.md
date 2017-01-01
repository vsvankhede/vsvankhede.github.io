---
title: 'Gradle: resolve dependency version conflict'
layout: post
---

While developing android application sometimes you may have faced dependency version conflict error during gradle build. If you are not familiar with the gradle build system and its dependency management then you might get stuck due to this.
![cartoon](http://i.imgur.com/6n24q3l.jpg)

In this blog post, we will see two different methods to resolve this dependency version conflict. But before that, we have to know what’s the “Transitive Dependency”?

### Transitive dependency

In Android app/build.gradle when you declare the dependencies(libraries) of your project, those dependencies themselves have the dependencies which are called as the Transitive dependency. 

Ok, so why we have to worry about transitive dependency? And how you will get to know which transitive dependency causing this problem? 

Version conflict generally occurs due to this transitive dependency. Below picture will help you to understand this problem.

![depedency-tree](http://i.imgur.com/S8Q9P8o.png)

In above picture, you can see the dependency tree of the project. Where Lib A and Lib B having a dependency on Lib C but here both are using the different version of Lib C. Lib C is called the Transitive dependency of your project and this is the one which is creating the version conflict error. 

But how you will get to know which transitive depedency creating the problem in your project?
Well, you find it using ./gradle androidDependencies command. If you are using gradle wrapper then you can use gradlew instead of gradle. 

If you will execute this command then you will find the dependency tree of your project, like as below. 

```java
+--- com.example.pro:LibA:24.2.1
|    |    +--- com.example.api:libC:1.2
+--- com.example.pro:LibB:20.0.1
|    |    +--- com.example.api:libC:1.3
```

From above dependency tree, we can see that Lib A having a dependency on LibC v1.2 and Lib B also having a same dependency on Lib C but different version v1.3. So now it might be clear to you why gradle was failing your build and throwing conflict error.

### How to fix it?

There are two way to resolve this conflict. 

### First solution: force
You can force gradle to use certain version of dependency including transitive dependency. 

```java
configurations.all {
   resolutionStrategy.force ‘com.example.api:libC:1.2’
}
```

### Second solution: dependencySubstitution
You can also define substitution rule for dependency.

```java
configurations.all {
   resolutionStrategy.dependencySubstitution {
       substitute module('com.example.api:libC:1.3') with module('com.example.api:libC:1.2')
   }
}
```

I hope that now you might be able to resolve your version conflict issue. You can also read the official gradle  docs for more information. If you are still facing any problem or have some suggestion please comment.

*Reference:*

[Gradle dependency management]( https://goo.gl/hNnzsF)

[Gradle resolution strategy](https://goo.gl/V602Gb)
