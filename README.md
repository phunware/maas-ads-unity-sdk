Unity Ads SDK
================



Project Folder Structure
---------------


#### PWAds-Unity

The Advertisement plugin now supports both, iOS and Android platforms in one single package which seamlessly adapts to the platform (unity player) you have selected with no additional work required.

#### Build

This folder contains the client facing package, in other words, this is the distributable plugin.

The following libraries can be found under "Phunware/Plugins"


#### Plugin Dependencies

##### iOS:

These dependencies can be found under /Unity/Assets/Plugins/iOS
    
1. PWCore.framework Version 3.0.3.
2. PWAdvertising.framework (Ass well as the PWAds.bundle) Version 3.6.2
    *Notes: PWAds.bundle contains a javascript file, in order to get this working the file inside unity was renamed to mraid._js. Upon compilation, this file automatically is deployed by the post processing module to .js*
 
##### Android:

These dependencies can be found under /Unity/Assets/Plugins/Android
    
1. PWAds-2.4.3.aar Version 2.4.3 -- Android ads SDK
2. core-3.0.3.aar   Version 3.0.3 -- Android Phunware Core SDK
3. pwads-bridge-unity.jar Version 1.1.0 -- Android Unity - SDK bridge


#### PW.iOS.Project.Build

This project is used to build a plugin for the purpose of post processing the XCode project output with zero client intervention for iOS builds only. Currently is configured to perform the following tasks:

1. Add the required by PWCore and PWAdvertisement dependencies like: AVFoundation, QuartzCore and so forth
2. Ads the PWCore, PWAdvertisement frameworks and PWAds.bundle to the output project.
3. Renames PWAds.bundle/mraid.js to mraid._js on the output project.
4. Adds required compiler and linker flags to the output project.

To configure the build process, you can edit the following JSon file in /Plugins/iOS/PWSAds.projmods, The json structure is straightforward and self descriptive. The following is the structure currently used:

````
{
    "group": "PWAds",
    "libs": ["libz.tbd",
    	"libsqlite3.tbd",
    	"libiconv.2.tbd"
    	],
    "frameworks": ["PWAdvertising.framework",
    	"PWCore.framework",
    	"SystemConfiguration.framework",
		"QuartzCore.framework",
		"CoreTelephony.framework",
		"MessageUI.framework",
		"EventKit.framework",
		"EventKitUI.framework",
		"CoreMedia.framework",
		"AVFoundation.framework",
		"MediaPlayer.framework",
		"AudioToolbox.framework",
		"WebKit.framework",
		"AdSupport.framework",
		"StoreKit.framework",
		"Security.framework",
		"MobileCoreServices.framework",
		"UIKit.framework",
		"CoreLocation.framework"
    ],
    "headerpaths": ["**"],
    "files":   [],
    "rename": ["mraid._js>mraid.js"],
    "folders": [],
    "excludes": ["^.*.meta$", "^.*.mdown$"],
    "compiler_flags": [""],
    "linker_flags": ["-ObjC"]
}
````


#### PWAds-iOS-CodeEdit

This folder contains an XCode project to make editing the iOS plugins easier, but is not used during compilation and has no purpose other than for editing.



## Known Issues

###iOS:

####Build Options
Unity currently outputs a project with ENABLE BITCODE flag set, but PWCore 2.0 was not built with this flag. Building for device target will fail unless the flag is turned off.  Post processing is still not equipped to turn this flag off automatically.  Also, symbolication for both build configurations should be turned off (ie set to just DWARF; NOT with dSYM File).

#### Symbolic Links to Resources Folders
.framework files come with symlinks to Resources folders, which are troublesome to Unity.  When updating the iOS frameworks, It may be necessary to remove the following files that are symlinks:
Internal/Objective-C/PWAds/Frameworks/PWAdvertising.framework/Resources
Unity/Assets/Plugins/iOS/PWAdvertising.framework/Resources
It might even be safest to just search for all symbolic links by the name Resources and delete them: find . -type l -name Resources -exec rm {} \;
a shell script rmbadlinks has been provided to do just that.  The presence of these bad symbolic links to folders named Resources could be the culprit if you're experiencing application unresponsive crashes upon launching Unity.

Another way to deal with this, which we have done in the included .framework files, is to simply remove everything but the current binary and Headers folder.

### Client Documentation:

#### Importing the Plugin:

To import the plugin, simply go to Assets -> Import Package -> Custom Package and browse to your downloaded plugin location.


#### Working with the Plugin

Is important to note that the plugin does not work in the editor player, this is a native plugin therefore, you should test using either a real device, or an emulator for both, iOS and/or Android. 

To add a banner, interstitial, landing page, native, video or rewarded video ad to your scene, simply create an empty game object (location does not matter) and add the PWAdBehaviour plugin script as a component to the game object by manually dragging the script onto the game object or by using the Component Menu.  Another option for integration could be without the usage of the PWAdBehaviour script.  However, for proper communication with the native ads sdk's, some component script must implement the IPWAdsHandler interface.  Public static functions for interfacing with the native ads SDK's are provided by way of the script PWAdvertisement which is derived from for each of the supported native platfoms.  PWAdRequestData, PWAdResponseData and PWAdCallbackEventArgs provide the necessary data model support for requesting and viewing Phunware advertisements.

A Custom Editor script is provided for the PWAdBehaviour component which provides an easy to use option for configuring ad request data.  The first thing to configure is the ad type, which can be selected from the list of supported types.  A zone Id must be provided with every type, and certain ads can have custom fields that may or may not also be required.  For example, if Rewarded Video ad type is selected, fields to configure the User Id and CustomData will show in the inspector

## Ad Types
### Banner
A size must be selected as well as an alignment option.  Additionally, an optional 3D Banner flag can be used with 320x50 banners.

Once the banner ad has been requested, it will remain on screen until dismissal, and a new ad will be inserted into the banner every 30 seconds.
### Interstitial Image
Will show a full screen image

### Video
Will show a full screen video

### Landing Page
Will show the contents of a website as configured for the ad zone.

### Native
Will show an ad corresponding to the layout view selected

### Rewarded Video
Will show a Rewarded Video whose views per interval are tracked and maintained by the Phunware ads service.

For Rewarded Video, upon ad request, a user Id value for the current user must be provided by the host app.  Additionally, there is a field provided for custom data, which the developers can use for dynamic functionality.  CustomData can be set as a JSON string containing anything important and up to 255 characters in length.