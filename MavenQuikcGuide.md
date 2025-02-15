1. Maven Dependency Management
•	When you add a JUnit dependency in your pom.xml, Maven downloads the JUnit JAR file and places it in your local Maven repository (usually in ~/.m2/repository).
•	When you run mvn compile, Maven compiles your main code and test code separately. The compiled classes for your test code are placed in the target/test-classes directory.
•	The JUnit library itself (the JAR file) is not copied to your target/test-classes directory. Instead, it remains in your local Maven repository.
2.  Classpath Management
•	Maven automatically configures the classpath for you during the build and test processes. When you run tests (using mvn test), Maven includes the JUnit JAR from your local repository in the classpath, allowing your test classes in target/test-classes to reference it.
•	This means that even though you don't see the JUnit JAR directly in the target directory, it's still available for your tests because Maven knows to include it when running tests.
Transitive Dependency
 Maven strategies -  Shortest path and first declared .. we can override this probably by declaring as direct dependency

A 2.0  C 4.0
B 2. 0  C 5.0
By default in final repo u ‘ll have A2.0, B2.0 and C.40 as C4.0 as first declared. But if we want C 5.0 then you can declare direct dependency 

A 2.0 ->C4.0
B2.0->C.50
C 5.0  -- In this case C4.0 will be ignored as C 5.0 is shortest path compared to 4.0

Scopes:
Test, Compile(default),Runtime, Provided – widely used ones
If we mark any dependency marked with scope and that will be available only during that time , lets say JUNIT dependencies are not needed during compile – so we mark them as Test

Lets say u need some libraries only for ur coding but at run time its already available – something like servlet libraries – then u can mark them as Provided

Runtime is opposite – u dnt need for coding but need for run time , like mysql dependencies

Maven LifeCycle

3 Life cycles
Default Life Cycle : 
validate , 
Compile – gnerates .class files in target 
test,  - generate .class file test/target
package – creates jar/war
verify ,
install, -installs in local repository 
deploy – deploys in remote repository 

Clean LifeCycle
Clean




Site Life Cycle
Site –generates html files
Site-deploy – deploys generated html files in to remote servers

Actually when we run mvn <pahse> we are indirectlly telling execute all plugins with scope define as phase mentioned in command 

two symtxes for maven mvn <phase>  and mvn goal:pluginname 

Anology : If PreparingDishes , keepingOnTable , Cleaning are 3 phases ; 
Tools like mixer, knife are tools like plug in and each tool has goal mixer-mixing ingerdisants ; Knife -CuttingVegtables;
MixingIngerdiants and CuttingVegtables goals are attached to PreparingDishes phase - 

So i can run mvn command in two ways

mvn PreparingDishes -- this will run two goals MixingIngerdiants and CuttingVegtables 

or else i can run each goald independently 

mvn Mixer:MixingIngerdiants
mvn Knife:CuttingVegtables

In Maven though you dont explicitly define each plug in and respective goal - there will be some default goals infused to pom.xml thats why yu may not see some plugins for compile phase still those eill be executed


End of the day maven commands are running certain goals in specific sequnece
```
Lifecycles
 ├── Default Lifecycle
 │   ├── validate
 │   ├── compile
 │   │   └── maven-compiler-plugin:compile
 │   ├── test
 │   │   └── maven-surefire-plugin:test
 │   ├── package
 │   │   └── maven-jar-plugin:jar
 │   ├── install
 │   │   └── maven-install-plugin:install
 │   ├── deploy
 │       └── maven-deploy-plugin:deploy
 │
 ├── Clean Lifecycle
 │   ├── pre-clean
 │   ├── clean
 │   │   └── maven-clean-plugin:clean
 │   ├── post-clean
 │
 ├── Site Lifecycle
     ├── pre-site
     ├── site
     │   └── maven-site-plugin:site
     ├── post-site
     ├── site-deploy
         └── maven-site-plugin:deploy

```
