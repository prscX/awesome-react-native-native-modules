
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

