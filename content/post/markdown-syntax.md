+++
aliases = ["migrate-from-jekyl"]
author = "Hugo Authors"
categories = ["themes", "syntax"]
date = 2019-03-11T00:00:00Z
description = "Sample article showcasing basic Markdown syntax and formatting for HTML elements."
feature_image = "/images/francesco-ungaro-GX81x7KTfIw-unsplash.jpg"
series = ["Themes Guide"]
tags = ["markdown", "css", "html", "themes"]
title = "Markdown Syntax Guide"

+++
***

![](https://cdn-images-1.medium.com/max/2560/1*DAaYWXIdhMcRJuAenAfp4g.png)

### Firestore Pagination in Android — Using FirebaseUI Library 🔥

Hi everyone, In this article, we will learn to implement _Paging support_ for _Firestore Database_ in Android. Before starting to the topic, Let’s first take a look at the available components within the Firebase.

**FirebaseUI-Android** library has **FirestoreRecyclerAdapter** for easy implementation of the population of **Firestore Database**. But if the database is having a total number of children in thousands or around then it becomes a bad presentation of User Interface. Let’s take an example if you are implementing social media app and you are having around 100 Posts. If we load these Posts using _FirestoreRecyclerAdapter_ then it will load all the Posts at the time of loading. So, this will be wastage of memory or hectic for the user to scroll down with a large list or it is not good to present in front of the application user. To overcome this, we will use pagination which will load Firestore Database document items in pages.

This API is available on [this](https://github.com/firebase/FirebaseUI-Android/tree/master/firestore) official **FirebaseUI**’s GitHub repository.

`FirestorePagingAdapter` — binds a `Query` to a `RecyclerView` by loading data in pages. Best used with large, static data sets. Real-time events are not respected by this adapter, so it will not detect new/removed items or changes to items already loaded. The `FirestorePagingAdapter` is built on top of the [Android Paging Support Library](https://developer.android.com/topic/libraries/architecture/paging.html).

**See Output:**

![](https://cdn-images-1.medium.com/max/800/1*a3mU6pdewXtrsp3smLjllQ.gif)

Demo output of Implementation of Firestore Paging Adapter.

### 💻 Getting Started :

Let’s get started to the code! I will show you this demo in both the Android development languages i.e. **_Kotlin _**as well as **_Java _**side by side.

Open _Android Studio._ Create a new project OR you can simply _clone this repository:_ [https://github.com/PatilShreyas/FirestorePagingDemo-Android](https://github.com/PatilShreyas/FirestorePagingDemo-Android "https://github.com/PatilShreyas/FirestorePagingDemo-Android")

First of all, go to Firebase Console and create a new Android Project. Download configuration file i.e. **_`google-services.json` _**and place it in the **/app** directory.

In this app, you are showing a paginated list of Posts. Posts will load in `RecyclerView.`

#### Gradle Setup

In the app module of `build.gradle` include following dependencies.

App module build.gradle file.

\`\`\`kt

Hello

\`\`\`

#### App Setup

Make model class (Consider `Post.java`) in the app.

Model Class

Then, create a `ViewHolder` class by inheriting `RecyclerView.ViewHolder` as below.

ViewHolder class.

### Initialize :

Don’t forget to set _`LayoutManager`_ to the RecyclerView.  
Set it using _`RecyclerView#setLayoutManager()` ._

#### Setup Configuration for PagedList

First of all configure PagedList   
_Remember that, the size you will pass to `setPageSize()` a method will load x3 items of that size at first load._ (Here, in this example we passed value 10. So, it will load 10x3 i.e. 30 items at first load).

Paging Configuration

Then Configure Adapter by building FirestorePagingOptions. It will generic.   
_Remember one thing,_ This query should only contain `where()`and `orderBy()` clauses. Any `limit()` or pagination clauses will cause errors.

Firestore Paging adapter configuration.

#### Initialize Adapter

_`FirestorePagingAdapter`_ is built on the top of Android Architecture Components - Paging Support Library. To implement, you should already have _`RecyclerView.ViewHolder`_ subclass. Here We used _`PostViewHolder`_ class.

* **Java Code 👇**

Java code for creating FirestorePagingAdapter

* **Kotlin Code 👇**

Kotlin code for creating FirestorePagingAdapter

Any changes occur in the adapter will result in the callback _`onLoadingStateChanged()`_

#### Error Handling

To get to know about Errors caught during Paging, Override method `onError()` in the adapter.

Error Handling in Adapter

#### Retrying List (After Error / Failure)

To retry items loading in RecyclerView, `retry()` method from Adapter class is used.   
Use it as `FirestorePagingAdapter#retry()`.   
This method should be used only after caught in Error. `retry()` should not be invoked anytime other than ERROR state.   
Whenever `LoadingState` becomes `LoadingState.ERROR` we can use `retry()`to load items in RecyclerView which were unable to load due to recent failure/error and to maintain Paging List stable.  
See the demo for a method.

    mAdapter.retry();

#### Refreshing List

To refresh items in RecyclerView, `refresh()` method from Adapter class is used.   
Use it as `FirestorePagingAdapter#refresh()`.   
This method clears all the items in RecyclerView and reloads the data again from the beginning.   
See the demo for a method.

Refreshing the list

#### Set Adapter

Finally, Set adapter to the`RecyclerView`.

**Java Code** 👉`mRecyclerView.`**`setAdapter(mAdapter)`**`;`

**Kotlin Code** 👉`recyclerView.`**_`adapter` _**`= `**`mAdapter`**

#### Lifecycle

At last, To begin populating data, call `startListening()` method. `stopListening()` stops the data being loaded.

To begin populating data, call the `startListening()` method. You may want to call this in your `onStart()` method. Make sure you have finished any authentication necessary to read the data before calling `startListening()` or your query will fail.

Start Lifecycle of the Adapter

Similarly, the `stopListening()` call freezes the data in the `RecyclerView` and prevents any future loading of data pages.

Call this method when the containing Activity or Fragment stops:

Stop Lifecycle of the Adapter

> _Thus, we have implemented the **FirestoreRecycler Pagination**. 😃_

You can see the _full app demo_ on below-listed resources with source code and step-by-step guide.

Please have a clap for this article if you found it helpful!

**_Thank You!_ 😃**

If you need any help get in touch with me on [Facebook](https://www.facebook.com/shreyaspatil99?source=post_page---------------------------), [Twitter](https://twitter.com/imShreyasPatil?source=post_page---------------------------), [LinkedIn](https://www.linkedin.com/in/patil-shreyas?source=post_page---------------------------), [GitHub](https://github.com/PatilShreyas?source=post_page---------------------------), [Personal Site](https://patilshreyas.github.io/?source=post_page---------------------------).

### Resources:

[**PatilShreyas/FirestorePagingDemo-Android**  
_Demo app for implementation of Firestore Paging library in Android app. - PatilShreyas/FirestorePagingDemo-Android_github.com](https://github.com/PatilShreyas/FirestorePagingDemo-Android "https://github.com/PatilShreyas/FirestorePagingDemo-Android")

[**firebase/FirebaseUI-Android**  
_Optimized UI components for Firebase. Contribute to firebase/FirebaseUI-Android development by creating an account on…_github.com](https://github.com/firebase/FirebaseUI-Android/tree/master/firestore "https://github.com/firebase/FirebaseUI-Android/tree/master/firestore")

By [Shreyas Patil](https://medium.com/@patilshreyas) on [July 21, 2019](https://medium.com/p/1d7fe1a75704).

[Canonical link](https://medium.com/@patilshreyas/firestore-pagination-in-android-using-firebaseui-library-1d7fe1a75704)

Exported from [Medium](https://medium.com/) on May 22, 2020.