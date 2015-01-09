# External Keyboard Plugin for Cordova, Phonegap and Ionic

The `cordova.plugins.ExternalKeyboard` provides an easy way to configure keyboard shortcuts for iOS 7 devices with an external bluetooth keyboard. Currently the plugin requires a little bit of manual installation (see below).


# Installation

First install the plugin proper:

    cordova plugin add https://github.com/petrsimon/cordova.externalkeyboard.git

After running the command above, open the iOS project in XCode and add the following code:

## In `MainViewController.h`

replace 

```objective-c
@interface MainViewController : CDVViewController
@end
```

with 

```objective-c
#import "ExternalKeyboard.h"
@interface MainViewController : CDVViewController {
    NSMutableArray *commands;
}

- (void) setKeyCommands:(NSArray*) commands;
@end
```

## In `MainViewController.m`

Under @implementation MainViewContoller - add the following: 

```Objective-c
// For the External Keyboard Support
- (BOOL)canBecomeFirstResponder {
	return YES;
}
- (NSArray *)keyCommands {
	return @[
		[UIKeyCommand keyCommandWithInput:@"0" modifierFlags:0 action:@selector(keyPress0)],
		[UIKeyCommand keyCommandWithInput:@"1" modifierFlags:0 action:@selector(keyPress1)],
		[UIKeyCommand keyCommandWithInput:@"2" modifierFlags:0 action:@selector(keyPress2)],
		[UIKeyCommand keyCommandWithInput:@"3" modifierFlags:0 action:@selector(keyPress3)],
		[UIKeyCommand keyCommandWithInput:@"4" modifierFlags:0 action:@selector(keyPress4)],
		[UIKeyCommand keyCommandWithInput:@"5" modifierFlags:0 action:@selector(keyPress5)],
		[UIKeyCommand keyCommandWithInput:@"6" modifierFlags:0 action:@selector(keyPress6)],
		[UIKeyCommand keyCommandWithInput:@"7" modifierFlags:0 action:@selector(keyPress7)],
		[UIKeyCommand keyCommandWithInput:@"8" modifierFlags:0 action:@selector(keyPress8)],
		[UIKeyCommand keyCommandWithInput:@"9" modifierFlags:0 action:@selector(keyPress9)],
		[UIKeyCommand keyCommandWithInput:@"\r" modifierFlags:0 action:@selector(keyPressR)],
    ];
}
- (void)keyPress0 {
	NSString *jsStatement = [NSString stringWithFormat:@"external_device_command('%s')", "0"];
	[self.commandDelegate evalJs:jsStatement];
}
- (void)keyPress1 {
	NSString *jsStatement = [NSString stringWithFormat:@"external_device_command('%s')", "1"];
	[self.commandDelegate evalJs:jsStatement];
}
- (void)keyPress2 {
	NSString *jsStatement = [NSString stringWithFormat:@"external_device_command('%s')", "2"];
	[self.commandDelegate evalJs:jsStatement];
}
- (void)keyPress3 {
	NSString *jsStatement = [NSString stringWithFormat:@"external_device_command('%s')", "3"];
	[self.commandDelegate evalJs:jsStatement];
}
- (void)keyPress4 {
	NSString *jsStatement = [NSString stringWithFormat:@"external_device_command('%s')", "4"];
	[self.commandDelegate evalJs:jsStatement];
}
- (void)keyPress5 {
	NSString *jsStatement = [NSString stringWithFormat:@"external_device_command('%s')", "5"];
	[self.commandDelegate evalJs:jsStatement];
}
- (void)keyPress6 {
	NSString *jsStatement = [NSString stringWithFormat:@"external_device_command('%s')", "6"];
	[self.commandDelegate evalJs:jsStatement];
}
- (void)keyPress7 {
	NSString *jsStatement = [NSString stringWithFormat:@"external_device_command('%s')", "7"];
	[self.commandDelegate evalJs:jsStatement];
}
- (void)keyPress8 {
	NSString *jsStatement = [NSString stringWithFormat:@"external_device_command('%s')", "8"];
	[self.commandDelegate evalJs:jsStatement];
}
- (void)keyPress9 {
	NSString *jsStatement = [NSString stringWithFormat:@"external_device_command('%s')", "9"];
	[self.commandDelegate evalJs:jsStatement];
}
- (void)keyPressR {
	NSString *jsStatement = [NSString stringWithFormat:@"external_device_command('%s')", "\\r"];
	[self.commandDelegate evalJs:jsStatement];
}

/* ## */
```



### 

# Usage

## Set up 
Currently the expected format for shortcuts is a simple string with modifier keys and input keys delimited by a space and the commands delimited by a configurable string such as `|`:
```javascript
var commands = "ctrl s|ctrl n|meta s|meta alt j";
```

The `meta` key stands for the Command Key (⌘) on Mac. The Mac Option Key (⌥) is represented by "alt".

Then send the commands to the plugin:

```javascript
var commands = "ctrl s|ctrl n|meta s|meta alt j",
    delimiter = "|";
cordova.plugins.ExternalKeyboard.setKeyCommands(commands, delimiter);
```


## Handling the shortcuts
On the page or in one of your modules, create the function `handleKeyCommand` like so:
```javascript
window.handleKeyCommand = function(combo) {
    // do something usefull
}
```

In AngularJS or Ionic it is quite possible to define or overwrite the `handleKeyCommand` function in a controller or to send the combo to a service that will take care of it, e.g.
```javascript
window.handleKeyCommand = function(combo) {
    $scope.handleCombo(combo)
    // or using a service
    Keymap.handleShortcut(combo);
}
```

# Supported Platforms

- iOS
