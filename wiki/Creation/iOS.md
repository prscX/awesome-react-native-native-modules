
## Macros

- **RCTBridgeModule**: RCTBridgeModule is a protocol. It provides an interface for registering a bridge module RCTBridgeModule `@protocol RCTBridgeModule`

- **RCT_EXPORT_MODULE(js_name)**: Register your module with the bridge during class implementation. It has an argument js_name which is optional and it is used as the JS module name. In case if it is not defined, Objective-C class name will be defined as the JS module name.

- **RCT_EXPORT_METHOD(method)\RCT_REMAP_METHOD(, method)**: Bridge modules can also define methods that are exported to JavaScript as `NativeModules.ModuleName.methodName`

```objectivec
RCT_EXPORT_METHOD(funcName:(NSString *)onlyString
                    secondName:(NSInteger)argInteger)
  { ... }
```

This is exposed to JavaScript as `NativeModules.ModuleName.funcName`

## How to create a Native Module Package

We’ll need to add two files to our project: a header file and its implementation file.



```objectivec
- MyNativePackage.h

#import "RCTBridgeModule.h"

@interface MyNativePackage : NSObject <RCTBridgeModule>
@end

- MyNativePackage.m

#import "MyNativePackage.h"

@implementation MyNativePackage

RCT_EXPORT_MODULE();

@end
```

## Creating a Module Method

We can now add a method to actually get the system volume in Volume.m (see this commit in our example code):

```objectivec
RCT_EXPORT_METHOD(Show:(RCTResponseSenderBlock)callback) {
}
```

- Invoking Module Method from JavaScript

```javascript
import { NativeModules } from 'react-native'

const MyNativeModule = NativeModules.MyNativeModule;
MyNativeModule.Show(() => {})
```

## Creating a Native View Component

- Create a view method to return your native component

```objectivec
- (UIView *)view {
    //Initialize & return your native component view
}
```

- Creating native props methods

```objectivec
RCT_CUSTOM_VIEW_PROPERTY(prop, DATA_TYPE_OF_PROP, YOUR_NATIVE_COMPONENT_CLASS) {
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