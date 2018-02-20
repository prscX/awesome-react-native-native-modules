
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

## Creating a Module Class

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

- Exposing Module Methods: Let's defines an `Show` method that takes a config object and success and cancel callbacks.

```java
public class MyNativeModule extends ReactContextBaseJavaModule {
    @ReactMethod
    public void Show(ReadableMap config, Callback successCallback, Callback cancelCallback) {
        Activity currentActivity = getCurrentActivity();
    
        if (currentActivity == null) {
            cancelCallback.invoke("Activity doesn't exist");
            return;
        }
    }
}
```

- Invoking Module Method from JavaScript

```javascript
import { NativeModules } from "react-native";

const { MyNativeModule } = NativeModules;

MyNativeModule.Show(
    {}, //Config Parameters
    () => {}, //Success Callback
    () => {} //Cancel Callback
)

```

> **Note**:
> - Module method are just for static invocation, it cannot be part of react tree

## Creating a Native View Component

- If you want to render a Native View component in react tree

- Create a Java Class extending from ReactNative ViewGroupManager

```java
public class RNNativeComponent extends ViewGroupManager<ViewGroup> {
    public static final String REACT_CLASS = "RNNativeComponent";
}
```

- Override `getName` method:

```java
@Override 
public String getName() {
    return REACT_CLASS;
} 
```

- Override `createViewInstance` method to return your custom native component

```java
@Override 
  protected FrameLayout createViewInstance(final ThemedReactContext reactContext) {
      return //Your-Native-Component-Wrappered-Inside-FrameLayout
  }
```

- Creating native prop methods

```java
  @ReactProp(name = "prop_name") 
  public void setPropName(NativeComponent nativeComponent, propDataType prop) {
  }
```


- Accessing in JavaScript

```javascript
import { requireNativeComponent } from "react-native"

const MyNativeComponent = requireNativeComponent("RNNativeComponent", RNNativeComponent, {
  nativeOnly: { }
})

<MyNativeComponent prop={this.props.prop}>
```