In Mac Book , when you install new JDK (from Java9 onwards – JDK comes with both JDK and JRE ) it gets installed in 

Vamsi@ip-50-5-80-117 ~ % /usr/libexec/java_home -V

Matching Java Virtual Machines (4):
    21.0.5 (x86_64) "Oracle Corporation" - "Java SE 21.0.5" /Library/Java/JavaVirtualMachines/jdk-21.jdk/Contents/Home
    17.0.10 (x86_64) "Oracle Corporation" - "Java SE 17.0.10" /Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home
    14.0.1 (x86_64) "Oracle Corporation" - "Java SE 14.0.1" /Library/Java/JavaVirtualMachines/jdk-14.0.1.jdk/Contents/Home
    1.8.333.02 (x86_64) "Oracle Corporation" - "Java" /Library/Internet Plug-Ins/JavaAppletPlugin.plugin/Contents/Home
/Library/Java/JavaVirtualMachines/jdk-21.jdk/Contents/Home

/Library/Java/JavaVirtualMachines/ <version> , if don’t set any JAVAHOME env variable , by default mac takes latest version 

but when we run which java it doenst point to above installation link insated it gives common binaries 
Vamsi@ip-50-5-80-117 bin % which java
/usr/bin/java
 mac os internally gives reference from /usr/bin/ or /usr/local/bin to actual installation , that’s why though you did not installation location to path env variable , it works .Lets say I have minikube installed but I didn’t add to path variable , still when I hit minikube –version from any path it works how ? 
to path variable  usr/local/bin added. (though mini kube installation is somewhere else) 
usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin

now I downloaded mvn not through home brew , so its downloaded to different folder , so there is no link from my downloads to usr/local/bin – if I would have downloaded from brew .. it would have directly added simlink from maven to usr/local/lib simlink .. 
now im going to that manually , insated of adding downloads folder to path variable


Vamsi@ip-50-5-80-117 / % sudo mv /Users/Vamsi/Downloads/MeghanaParentsVISA/apache-maven-3.9.9 /opt/maven/

Vamsi@ip-50-5-80-117 / % sudo ln -s /opt/maven/apache-maven-3.9.9/bin/mvn /usr/local/bin/mvn

Vamsi@ip-50-5-80-117 / % mvn -version
Apache Maven 3.9.9 (8e8579a9e76f7d015ee5ec7bfcdc97d260186937)
Maven home: /opt/maven/apache-maven-3.9.9
Java version: 21.0.5, vendor: Oracle Corporation, runtime: /Library/Java/JavaVirtualMachines/jdk-21.jdk/Contents/Home
Default locale: en_US, platform encoding: UTF-8
OS name: "mac os x", version: "12.7.4", arch: "x86_64", family: "mac"

Moved from downloads to opt/maven and created simlink using sudo ln -s /opt/maven/apache-maven-3.9.9/bin/mvn /usr/local/bin/mvn

![image](https://github.com/user-attachments/assets/56c77db3-07d5-4d5e-8722-017ada54ca5d)

