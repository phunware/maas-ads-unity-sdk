PWAdsUnity Change Log
==========================
Version 1.1.0 *(2017-06-23)*
----------------------------
 * changed default message handling for video ads to trigger off of PRECACHED messages rather than LOADED
 * fixed banner ad for iOS showing on top of interstitial ads
 * changed banner ad views to use RootViewController like other ad views so it can be properly layered amongst them
 * added support for ad placements per platform
 * renamed CustomDataPropertyDrawer to CustomDataItemPropertyDrawer
 * added PWAdPlacement which provides support for specifying zone ids on a per-platform basis
 * added SerializableDictionaryBase which facilitates the inspector display of the per-platform  placement options
 * corrected android request for interstitial video
 * corrected conditional compilation logic when building asset bundles
 * Updated native iOS Ads SDK to version 3.6.2
 * updated Android Ads SDK to 2.4.3
 * added sample app images to Sprite Sheet
 * improved draw calls from a min of 5 and max of 18 to a min of 2 and a max of 3
 * made all images in sample app comply with the same graphics and compression settings
 * removed zip file that did not below in the project
 * Extended ads caching API to be able to set the max cache size
 * Updated Unity Ads SDK to be compatible with version 5.6.1p4 of Unity
 * Updated iOS plugin bridge to be compatible with above updates
 * Updated Android plugin bridge to be compatible with above updates
 * Implemented Pre-Cacheing utilization within the Rewarded Video experience
 * implemented support for loading/pre-cacheing Interstitial Video ads
 * improved bundling on dependencies in the Android plugin
 * fixed several crash issues within the iOS plugin which were caused by dangerous/bad uses of performSelector
    
Version 1.0.1 *(2016-12-13)*
----------------------------
 * iOS Ads SDK updated to 3.5.1, which includes support for Landscape Ad Zones with End Cards
 * Android Ads SDK updated to 2.3.1, which includes support for Landscape Ad Zones with End Cards
 * Renamed MiniJSON class so it won't collide with itself if other modules have included it
 * Project organization improvements - packages are now better self-contained
 * Updated RVOfferWall prefab to be what's in use within the scene
 * Updated PWSAds.projmods to include WebKit.framework, for compatibility with Xcode 8
 * Separated build logic out of BuildMenu class into a PhunwareBuildUtil class which is now included in the packages
 * Ads requests now all use SSH enabled calls
 * VAST payloads for Video Ads now support the recommended format for <Extenions>, which includes container <Extention> elements

Version 1.0.0 *(2016-11-08)*
----------------------------
 * Initial release.
