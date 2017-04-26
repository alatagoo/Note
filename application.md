### 参考 
www.2cto.com/kf/201602/491002.html
### ZygoteInit 中启动SystemServer进程


SystemServer由ZygoteInit fork 一个进程来运行

当传入的第一个参数是 start-system-server 时启动systemServer, 随后会fork一个进程来启动systemServer，SYSTEMSERVERCLASSPATH在Android.mk 设置到init.environ.rc 中,



```
/frameworks/base/core/java/com/android/internal/os/ZygoteInit.java

// ============= mian ======================== //
public static void main(String argv[]) {
  ....
  if ("start-system-server".equals(argv[i])) {
    startSystemServer = ture;
  }
  ....


  ....
  if (startSystemServer) {
     startSystemServer(abiList, socketName);
  }
  ....
}


// ============ startSystemServer ============= //
 private static boolean startSystemServer(String abiList, String socketName){

   String args[] = {
       "--setuid=1000",
       "--setgroups=1001,1002,1003,1004,1005,1006,1007,1008,1009,1010,1018,1021,1032,3001,3002,3003,3006,3007",
       "--capabilities=" + capabilities + "," + capabilities,
       "--nice-name=system_server",
       "--runtime-args",
       "com.android.server.SystemServer",
   };

   // forck the process
   pid = Zygote.forkSystemServer( ........ )
   //
  if (pid == 0) {
    ....
    handleSystemServerProcess(parsedArgs);
  }


 private static void handleSystemServerProcess(.....){
     final StringsystemServerClasspath=Os.getenv("SYSTEMSERVERCLASSPATH");
     ........

     .........

 }


/system/core/rootdir/Android.mk


$(LOCAL_BUILT_MODULE): $(LOCAL_PATH)/init.environ.rc.in $(bcp_dep)
	@echo "Generate: $< -> $@"
	@mkdir -p $(dir $@)
	$(hide) sed -e 's?%BOOTCLASSPATH%?$(PRODUCT_BOOTCLASSPATH)?g' $< >$@
	$(hide) sed -i -e 's?%SYSTEMSERVERCLASSPATH%?$(PRODUCT_SYSTEM_SERVER_CLASSPATH)?g' $@
```


### SystemServer
