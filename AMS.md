### 涉及的文件
```
/frameworks/base/services/core/java/com/android/server/am/ActivityManagerService.java
/frameworks/base/core/java/android/app/IActivityManager.java
/frameworks/base/core/java/android/app/
/frameworks/base/services/core/java/com/android/server/am/
```

### AMS 接口功能
```
- 组件状态管理
- 组件状态查询
- task相关
- 其他
```

### ActivityStack
ActivityStack 是管理当前系统中所有Activity的状态的一个数据结构.

### 启动

### startActivity流程
```
Activity1 ---->
startActivity@ContextImpl.java ----->
execStartAcvivity@Instrumentation.java---->
startActivity@ActivityManagerService.java

```
