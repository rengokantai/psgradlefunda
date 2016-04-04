#### psgradlefunda
#####1
######running first time(delete gradle tagroup 'me.yd')
```
java -cp build\classes\main\ me.yd.Main
```
#####2 basic gradle
######simple task
below are identical: note (doLast and description)
```
project.task("task1")
task("task2")
task "task3"
task task4
task4.description = "desc"

task4.doLast{println "last"}
task3 <<{println "last"}
task task5 << {println "last"}
```
######phases
init->config(exec non action part of tasks)->exe phase(doFirst,doLast)
```
task task5 
{doFirst{println "first"}
description "desc"
doLast{println "last"}}

task5.doFirst{print "override"}  //this will print first, override "first", then print first
######seeting prop
declare:
```
def var = "varname"
//Or
project.ext.var = "varname"
```
use:
```
println "$var"
```
#####task dep
######basic dep
```
taskA dependsOn taskC, taskD
```
use ```gradle -q taskname```to quiet mode
######
mustRunAfter
shouldRnnAfter   #ignore circular dependency.

######
a.finalizedBy b  // b must run after a

#####Build a Java Project
###### java plugin
```
gradle compileJave
gradle classes
```
######gradle daemon
run tasks faster
```
gradle --daemon build
```
or set in env .gradle, add file gradle.properties,edit
```
org.gradle.daemon=true
```
Not use:
```
gradle --no-daemon build
```
######multiple projects
in top level,we create two files:  
build.gradle:
```
allprojects{
    apply plugin:'java'
}
project(':Proj1'){}
project(':Proj2'){
    dependencies{
        compile project(':Proj1')
    }
}
```
settings.gradle:
```
include 'Proj1','Proj2'
```