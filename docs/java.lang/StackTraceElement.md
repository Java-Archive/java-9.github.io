# New Methods in java.lang.StackTraceElement
The class itself is inside the JDK since 1.4.

The StackTraceElement will now have the information about the module and module-version.
For this they added a new constructor 

```java
public StackTraceElement(String moduleName, 
                         String moduleVersion,
                         String declaringClass, 
                         String methodName,String 
                         fileName, int lineNumber)
```
and the new getter methods ```public String getModuleName()``` and ```public String getModuleVersion()```

If you want to try this, play with the following.

```java
public static void main(String[] args) {
    try {
      throw new RuntimeException("and go");
    } catch (Exception e) {
      final StackTraceElement[] stackTrace = e.getStackTrace();
      for (StackTraceElement stackTraceElement : stackTrace) {
        final String moduleName = stackTraceElement.getModuleName();
        final String moduleVersion = stackTraceElement.getModuleVersion();
        System.out.println("moduleVersion = " + moduleVersion);
        System.out.println("moduleName = " + moduleName);
        System.out.println(stackTraceElement.getClassName() + " - " + stackTraceElement.getMethodName());
      }
    }
  }
```

The output at may machine was the following.
```text
moduleVersion = null
moduleName = null
org.rapidpm.workshop.java09.java.lang.StackTraceElementV001 - main
moduleVersion = 9-ea
moduleName = java.base
jdk.internal.reflect.NativeMethodAccessorImpl - invoke0
moduleVersion = 9-ea
moduleName = java.base
jdk.internal.reflect.NativeMethodAccessorImpl - invoke
moduleVersion = 9-ea
moduleName = java.base
jdk.internal.reflect.DelegatingMethodAccessorImpl - invoke
moduleVersion = 9-ea
moduleName = java.base
java.lang.reflect.Method - invoke
moduleVersion = null
moduleName = null
com.intellij.rt.execution.application.AppMain - main
```

The interesting thing here is, that the first and the last triple is without 
a module -version and -name.

Try to find out, why ;-) 
