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