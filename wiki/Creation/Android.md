
## How to create a Native Module Package

- Create a Java class for your Native Module Package by extending from ReactPackage, ideally it can look like below:

- Override `createNativeModules` & `createViewManagers` methods

```java

public class MyNativePackage implements ReactPackage {
    @Override
    public List<NativeModule> createNativeModules(ReactApplicationContext reactContext) {
    }

    @Override
    public List<ViewManager> createViewManagers(ReactApplicationContext reactContext) {
    }
}

```

- Add your Native Modules to `createNativeModules` method

```java
public List<NativeModule> createNativeModules(ReactApplicationContext reactContext) {
    List<NativeModule> modules = new ArrayList<>();
    modules.add(new MyNativeModule(reactContext));

    return modules;
}
```

- Add your Native Module UI Components to `createViewManagers` method

```java
public List<ViewManager> createViewManagers(ReactApplicationContext reactContext) {
    List<ViewManager> components = new ArrayList<>();
    components.add(new RNNativeComponent());

    return components;
}
```

## Creating a ReactContextBaseJavaModule

- We’ll start by creating the MyNativeModule class, and extending ReactContextBaseJavaModule.

```java
public class MyNativeModule extends ReactContextBaseJavaModule {
    public MyNativeModule(ReactApplicationContext reactContext) {
        super(reactContext);
    }
}
```

- That’s a good start, but in order for React Native to find our module in NativeModules we’ll need to override the getName method.

```java
@Override
public String getName() {
    return "MyNativeModule";
}
```

- We now have a fully functional (if totally useless) native module that we can import in our JavaScript code. Let’s make it do something a bit more interesting.

- Exposing Module Methods
Let's defines an show method that takes a config object and success and cancel callbacks.

```java
public class ImagePickerModule extends ReactContextBaseJavaModule {
    @ReactMethod
    public void show(ReadableMap config, Callback successCallback, Callback cancelCallback) {
        Activity currentActivity = getCurrentActivity();
    
        if (currentActivity == null) {
            cancelCallback.invoke("Activity doesn't exist");
            return;
        }
    }
}
```

