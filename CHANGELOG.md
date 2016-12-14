PWAdsUnity Change Log
==========================

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
