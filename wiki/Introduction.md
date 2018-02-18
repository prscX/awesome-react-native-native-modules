# Introduction

Native Modules enable an app to access platform API that are not exposed to JavaScript. There can be multiple use cases for creating a Native Module, maybe you want to reuse some existing Java/Objective-C/Swift/Kotlin code without having to reimplement it in JavaScript, or write some high performance components, multi-thread code such as for image processing or any number of advanced extensions.

React Native is designed in such that it is possible for you to write real native code and have access to the full power of the platform in JavaScript. 

## <a name="Things-you-should-know-BEFORE-you-create-a-Native-Module">Things you should know BEFORE you create a Native Module</a>


| **Dev Stack**||
|----|----|
|**`Platforms`**| Fair understanding of __Android, iOS__ Platform API's
|**`IDE`**|Xcode, Android Studio
|**`Languages`**| You need a basic knowledge of native language __JavaScript, Objective-C, Swift, Java__ in order to create a Native Module


## <a name="Eligibility-Criteria-for-creating-a-Native-Module">Eligibility Criteria for creating a Native Module</a>

The main vision of React Native is to Learn once, write anywhere, we also believe in the same ideology. Before creating any Native Module we should consider below points:

- **Availability:** Please check the availability of Platform API's, Native Libraries for which you are planning to create a Native Module, ideally it should be supported on both Platforms (iOS, Android).
- **Community & Maintenance:** Libraries which you are considering ideally should have a strong community, contributors backing, so that you can easily fulfil your community raised requests/queries.
- **Performance**: If you are looking for HIGH performance and cannot be achieved using JavaScript.
- **Scalability:** Native library which you are considering for Native Module should be scalable enough to fulfil your community needs.


## <a name="Advantages-of-Native-Module">Advantages of Native Module</a>

- **Reusability & Time Saving:** Libraries already exist in native, you can simply create a RN Bridge in order to access it in JavaScript.

- **Performance, Animation & Multithread:** Native Modules are always HIGH rich in performance and multithread since it can use full power of Platform API's.

- **Look & Feel:** There are scenarios where only Native Modules can accomplish native look and feel of component.

## <a name="Disadvantage-of-Native-Module">Disadvantage of Native Module</a>

- **Maintenance & Scalability:** Since Native Modules are written in different languages, it becomes hard to maintain same source in two different languages until you do not have a strong backing community.

