# React Native Bridging Guide

## Android Native Bridging

### 1. Create Native Module
```java
public class CustomModule extends ReactContextBaseJavaModule {
    public CustomModule(ReactApplicationContext reactContext) {
        super(reactContext);
    }

    @Override
    public String getName() {
        return "CustomModule";
    }
}
```

### 2. Implement Native Methods
```java
@ReactMethod
public void nativeMethod(String message, Promise promise) {
    try {
        // Native implementation
        promise.resolve("Result");
    } catch (Exception e) {
        promise.reject("ERROR", e.getMessage());
    }
}
```

### 3. Register the Module
```java
public class CustomPackage implements ReactPackage {
    @Override
    public List<NativeModule> createNativeModules(ReactApplicationContext reactContext) {
        List<NativeModule> modules = new ArrayList<>();
        modules.add(new CustomModule(reactContext));
        return modules;
    }

    @Override
    public List<ViewManager> createViewManagers(ReactApplicationContext reactContext) {
        return Collections.emptyList();
    }
}
```

### 4. Add to MainApplication.java
```java
@Override
protected List<ReactPackage> getPackages() {
    List<ReactPackage> packages = new PackageList(this).getPackages();
    packages.add(new CustomPackage());
    return packages;
}
```

## iOS Native Bridging

### 1. Create Native Module
```objective-c
// CustomModule.h
#import <React/RCTBridgeModule.h>

@interface CustomModule : NSObject <RCTBridgeModule>
@end

// CustomModule.m
#import "CustomModule.h"

@implementation CustomModule

RCT_EXPORT_MODULE();

@end
```

### 2. Implement Native Methods
```objective-c
RCT_EXPORT_METHOD(nativeMethod:(NSString *)message
                  resolver:(RCTPromiseResolveBlock)resolve
                  rejecter:(RCTPromiseRejectBlock)reject)
{
    @try {
        // Native implementation
        resolve(@"Result");
    } @catch (NSException *exception) {
        reject(@"ERROR", exception.reason, nil);
    }
}
```

### 3. Using in JavaScript/TypeScript
```typescript
import { NativeModules } from 'react-native';

const { CustomModule } = NativeModules;

// Using the native module
try {
    const result = await CustomModule.nativeMethod('Hello from JS');
    console.log(result);
} catch (error) {
    console.error(error);
}
```

## Best Practices

1. **Error Handling**
   - Always use try-catch blocks in native code
   - Return meaningful error messages
   - Handle promises properly in JS

2. **Type Safety**
   - Use TypeScript for better type checking
   - Define proper interfaces for native modules

3. **Performance**
   - Avoid blocking the main thread
   - Use async methods for heavy operations
   - Batch updates when possible

4. **Maintenance**
   - Document native modules thoroughly
   - Keep native code minimal and focused
   - Follow platform-specific conventions