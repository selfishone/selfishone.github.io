---
layout: post
title: Java8 Features
categories: [Notes]
tags: [Java]
---

Java 8 since its release in 2014 has become the most widely adopted java version being used by over 80% of Java applications, it has become the default version to which legacy applications are usually updated to. The reason it is Java8 is usually because version 7 has reached its EOL but upgrading to version 9 is too big of a step that companies would like to take. But even when team are updating to Java8 or writing a new app using it rareley do they even use the new features of the version. This stems from the fact that why fix anything which is not broken. 



<!-- Start of Unsplash Embed Code - Full-width (Embed code by @BirdyOz)-->
<div style="width:100%; margin: 20px auto;">
    <img src="https://images.unsplash.com/photo-1555421689-491a97ff2040?ixlib=rb-1.2.1&amp;q=80&amp;fm=jpg&amp;crop=entropy&amp;cs=tinysrgb&amp;w=1080&amp;fit=max&amp;ixid=eyJhcHBfaWQiOjEyMDd9" class="img-responsive img-fluid img-lge" alt="person using iMac " title="person using iMac ">
    <div class="text-muted" style="opacity: 0.5">
        <small><a href="https://unsplash.com/photos/Imc-IoZDMXc" target="_blank">Photo</a> by <a href="https://unsplash.com/@austindistel" target="_blank">@austindistel</a> on <a href="https://unsplash.com" target="_blank">Unsplash</a>, accessed 02/04/2020</small>
    </div>
</div>
<!-- End of Unsplash Embed code -->
                
                

As much as I want to disagree, that is the harsh reality of things, I say harsh  because newer versions come with some awesome features.Even though legacy applications now a days have been updated to Java8 as a defacto version, teams usually dont use the new features. This article aims to educate people on what benifits these features provide as a way to give them a reson to try using the new features for development.

### **Java8 New Features**

Java 8 really has a ton of new features, but we will only be covering those below which I think are the most important ones:

* Default methods in interfaces
* Lambda Expressions
* Functional Interfaces

### **Default Methods in interfaces**

Let's say you have written a java interface which is implemented by a different programmers. The API had gained popularity over the course of the year and you plan to add on new functionality to it. But there is a catch, any addition you make to your interface must not effect the current implementations. The new changes you are going to introduce must not force new changes onto the current implementations. So how do we do it?

<div class="message">
Default methods enable you to add new functionality to existing interfaces and ensure binary compatibility with code written for older versions of those interfaces.
</div>

The answer would be to use static methods which can be decalred and defined within the interface, but the issue with this process is that the implementation cant be overriden by the implementing classes, which destroys the whole purpose of having implementaion be taken care of by programmers, and instead they would turn out to be utility methods.

Java8 provides us a solution which doesnt require any rewrite of the implementing classes by programmers i.e. default methods. Methods which are declared default can be given a default implementation which may or maynot be overridden by the implementing classes. 

### Example
To make this more cleear lets consider the following scenario, your company is in the business of making industry standard interfaces for Smart Watches. This will leave implementation to other developers. We know each smart watch should have the following features:

* change dails
* receive texts
* accept calls

Everything is going fine and later down the line you think that you should have included something like make calls as well. Now here is where default methods come to play

<script src="https://gist.github.com/selfishone/816d37972ffc6973392bb2860dbb1bb1.js"></script>

We see that the AppleSmartWatch class has implemented the default method in the SmartWatch interface to its liking, And there would be no problem even if it didnt implement the method since the intention of defaults is to retain compatability with the older versions.

Plus default methods are also important in the context of Lambda expressions which can be discussed later in the Lambdas section

### **Paradigm shift**

Java fundamentally is an object oriented language where everything has to exist within a class, unlike in python or javascript where functions can be declared or can exist outside the class, and behavior(functions) can be passed on just as we do with the variables. 

But it sometimes does help thinking in terms of behaviour rather than objects, and functional programing provides a way for that by making functions the so called first class citizens instead of the classes. It enables to write us less verbose and concise code which has always been a problem with Java. So starting with version 1.8, java has provided us with a way to use functional programming concepts by introducing **lambda Expressions** and **functional intefaces**. 

### **Lambda Expressions**

As stated before it sometimes helps to think in terms of behavior rather than in terms of objects. So this problem arises in the context of functions which need to be used at only one place.

<div class="message">
Java lambda expressions are Java's first step into functional programming. A Java lambda expression is thus a function which can be created without belonging to any class.
</div>

### Example
Let us take an example of a thread, what we normally do is implement the Runnable class to create a thread object, so this would mean that we would have to write a whole new class just to implement the run method. Wouldnt it be a lot easier if we just passed on the behaviour of the run method rather than creating a whole new class? 

<script src="https://gist.github.com/selfishone/8651a0ff5ca5cea630c5fc4de8306d0c.js"></script>
<script src="https://gist.github.com/selfishone/9ccae0ea6e73087ee34fae6ecf142adc.js"></script>

Java 7 gave us a better way to do this, instead of creating a new class implementing the Runnable interface we can pass the behaviour of the run() method when instantiating a thread object, this can be achieved by using anonymous inner classes instead, but even this makes the whole code very verbose.

<script src="https://gist.github.com/selfishone/1485c00ae1d33ddb6c83d0e11eca1724.js"></script>

Even though we have improved the code over here, we still are creating a class just to implement the run() method, the only thing is that we dont have a name for it since we wont use it anywhere else (anonymous classes). Java8 provides us even a better way via lambda expressions to just pass on the behaviour required for run() method.

<script src="https://gist.github.com/selfishone/be783ac2d655b9d9b1bcdab46f333825.js"></script>

The major difference from the method before is that we are assigning the behavior to interface directly rather than overriding it in the implementation, we can either pass on the behavior by passing the refernce of runnable or directly use run() method onto the interface reference. We have greatly reduced the number of lines of code making the code pretty concise. 

**Note:** Java doesnt support function keyword like functional programming languages like javascript do. Instead we use interfaces which hold behaviors as references. This was done instead of creating function key word in order to have backward compatabilty with the older versions.

Plus Lambda expressions can only be used along with **functional interfaces** which will be discussed in the next section.

### **Functional Interfaces**

<div class="message">
An interface with only one abstract function is called a Functional interface
</div>

Java provides **@FunctionalInterface** annotation to ensure no additional abstract methods are added to an inteface. This is always good to use because Lambda Expressions based on functional Interface would fail at compile time if a new abstract method gets added to the interface in future, so the annotation is actually to warn developers of this. It is not necessary to have though.

Java has a list of functional interfaces defined in **java.lang.util** package. Instead of creating new interfaces to use lambdas we can instead make use of these. The collection is very good and consists of most used java patterns.

### **Summary**

Java 8 has brought to us these awesome feature which will improve the way we write code and its maintainabiltiy only if we use it. For instance we have seen that lambdas are a way to make the code pretty concise, and defaults have provided us a way to adhere to the principle of **open to extension and closed to modification ** giving us a proper way to improve our interfaces. 

Thanks!

### **References**

[Functional Interfaces](https://blog.jooq.org/2016/02/25/abusing-java-8-functionalinterfaces-as-local-methods/)

[Lambdas Best Practices](https://www.baeldung.com/java-8-lambda-expressions-tips)

[Why Java needs fubctors](https://www.oracle.com/technical-resources/articles/java/architect-lambdas-part1.html)

[Java8 new features and enhansements](https://docs.oracle.com/javase/8/docs/technotes/guides/language/enhancements.html)

[Java8 default methods](https://www.journaldev.com/2752/java-8-interface-changes-static-method-default-method)

[Everything about lambdas from JavaBrains](https://javabrains.thinkific.com/courses/java-8-lambda-basics)
