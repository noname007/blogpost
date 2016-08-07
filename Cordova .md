# Cordova 

## Android Lifecycle Guide

Cordova Single Activity

Cordova Event|Rough Android Equivalent|Meaning|
------|-----|-----|
deviceReady|onCreate|application start|
pause|onPause| moving to the background|
resume|onResume|returning to the foreground|

Cordova Activity Pause

- user press home button or switch to another application
- some cordova plugin may launch activity and push cordova into background。!!!\<WARN\> it‘ s a chance the os will kill it 
	- pause -> deviceReady -> resume


## iOS Lifecycle Guide 

offical document has nothing 


## Plugin Development Guide

```
cordova.exec(function(winParam) {},
             function(error) {},
             "service",
             "action",
             ["firstArgument", "secondArgument", 42, false]);
```

## Cordova Dependencies

alter the engines in the package.json, include ```cordovaDependencies``` using the following structure 

```
engines:{
	cordovaDependencies:{
		PLUGIN_VERSION:{
			DEPENDENCY:SEMVER_RANGE,
			DEPENDENCY:SEMVER_RANGE
		}
	}
}
```



## Native Interfaces



