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

### Andorid Plugin

Android plugins are based on Cordova-Android，which is built from an Android WebView with a native bridge. The native portion of an Android plugin consists of at least one Java class that extends the CordovaPlugin class and overrides one of its execute methods.

#### threading 

plugin's js code doesn't run in the main thread of the webview interface . It runs on the webcore thread ,as does the execute method . 


```
cordova.getActivity().runUiThread(new Runable(){
	public void run(){
	}
})

```

```
cordova.getThreadPool().execute(new Runnable() {
  public void run() {
            }
        });
```

### iOS Plugin


it‘s different with android 。 plugin methods execute in the same thread as the main interface. If your plugin requires a greaat deal of processing or requires a blocking call. you should use a background thread.

```
-(void)myPluginMethod:(CDVInvokeUrlCommand*)command
{
	[self.commandDelegate runInBackground:^{
		// some blocking commands
		
		CDVPluginResult* pluginResult = [CDVPluginResult resultWithStatus:CDVCommandStatus_OK messageAsString:payload];
		//the sendpluginresult method is thread-safe
		[self.commandDelegate sendPluginResult:pluginResult callbackId:command.callbackId];
	}];
}
```