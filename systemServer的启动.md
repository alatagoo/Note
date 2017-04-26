### ZygoteInit

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

   // forck the process
   pid = Zygote.forkSystemServer( ........ )

   //
  if (pid == 0) {
    ....
    handleSystemServerProcess(parsedArgs);
  }


 private static void handleSystemServerProcess(.....){
     final StringsystemServerClasspath=Os.getenv("SYSTEMSERVERCLASSPATH");
 }



```
当传人的第一个参数是 start-system-server 时启动systemServer, 随后会fork一个进程来启动systemServer
