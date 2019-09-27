# cordova-plugin-adcolony
AdColony ads for Apache Cordova.

Allows you to integrate with AdColony from within a Cordova app, supporting both Android and iOS. Requires the AdColony SDK

iOS SDK version is 4.1.0

Android SDK version is 4.1.0

Please make sure that you read the AdColony Project setup guides for both Android and iOS if you're building on both platforms.

All the documentation is available from here:

[AdColony Android SDK](ç)

[AdColony iOS SDK](https://github.com/AdColony/AdColony-iOS-SDK)

This update integrates AdColony using a podspec in the plugin definition

# Install plugin

```
$ cordova plugin add cordova-plugin-adcolony
```

See the AdColonyDemoApp code for how to configure and provide an APP\_ID and a ZONE\_ID within your JavaScript

### Android

If you are testing the Android Plugin, use the following demo APP\_ID and ZONE_ID:

APP\_ID=app185a7e71e1714831a49ec7

ZONE_ID=vz1fd5a8b2bf6841a0a4b826

You will need to manually merge the contents of the file platforms/android/proguard-adcolony.txt to your existing project proguard-project.txt file (I need to figure out how to do this via a script still)

### iOS

For the iOS Plugin, use the following demo APP\_ID and ZONE_ID in the configureWithAppID method

APP\_ID=appbdee68ae27024084bb334a

ZONE_ID=vzf8e4e97704c4445c87504e

Please note that you must follow steps 2 onwards in the AdColony Project Setup notes

# Methods

#### AdColony.configureWithAppID(appID, zoneIDs, options)  
Initial method wich connects to AdColony.  
(string) appID - the appID of your app in AdColony Dashboard  
([strings]) zoneIDs - array of your ad zones ids  
options - app options defined [here](https://adcolony-www-common.s3.amazonaws.com/Appledoc/4.1.0/Classes/AdColonyAppOptions.html)

#### AdColony.setAppOptions(options)  
Set App Options.
options - JSON Array typically with ONE element a JSON object with the options. Options defined [here](https://adcolony-www-common.s3.amazonaws.com/Appledoc/4.1.0/Classes/AdColonyAppOptions.html)

Note that I use the following strings from the Android SDK for cross-platform compatability

```
orientation
app_orientation
origin_store
disable_logging
user_id
gdpr_required
consent_string
test_mode
multi_window_enabled
mediation_network
mediation_network_version
plugin
plugin_version
keep_screen_on
```

#### AdColony.setAdOptions(options)  
Set Ad options.
options - JSON Array typically with ONE element a JSON object with the options. Options defined [here](https://adcolony-www-common.s3.amazonaws.com/Appledoc/4.1.0/Classes/AdColonyAdOptions.html)

#### AdColony.setUserMetaData(metadata)  
Set User meta-data for ad retrieval. Calling this sets the user metadata for all future ad requests 
metadata - JSON Array typically with ONE element a JSON object with the user meta-data. User meta-data defined [here](https://adcolony-www-common.s3.amazonaws.com/Appledoc/4.1.0/Classes/AdColonyUserMetadata.html)


#### AdColony.requestInterstitialInZone(zoneID)  
Request ad with given zoneID

#### AdColony.requestInterstitial()
Request ad with current zoneID

#### AdColony.registerRewardReceiver(rewardHandler)  
Register the given Javascript method to handle rewards (Demo uses 'AdColony.onRewardReceived)

#### AdColony.showWithPresentingViewController()
After ad is loaded you can show it by calling this method.

# Events

```
document.addEventListener('ConfigureSuccess', () => {  
  console.log('AdColonyPlugin: Configuration successfully completed.');
});
```
```
document.addEventListener('AdColonyRequestSubmitted', () => {
 console.log('AdColonyPlugin: Interstitial ad requested.');
});
```
```
document.addEventListener('AdColonyRequestFilled', () => {
 console.log('AdColonyPlugin: Interstitial ad loaded.');
});
```
```
document.addEventListener('AdColonyRequestNotFilled', (error) => {
  console.log('AdColonyPlugin: Request interstitial failed with error: ' + error);
});
```
```
document.addEventListener('AdColonyRequestOpened', () => {
  console.log('AdColonyPlugin: Interstitial ad opened.');
});
```
```
document.addEventListener('AdColonyRequestClosed', () => {
  console.log('AdColonyPlugin: Interstitial ad closed.');
});
```
```
document.addEventListener('AdColonyRequestExpiring', () => {
  console.log('AdColonyPlugin: Interstitial ad expiring.');
});
```

# Example

```
let appID = 'AdColonyAppID';
let zoneIDs = ['myZoneID1', 'myZoneID2'];
let options = null;

AdColony.configureWithAppID(appID, zoneIDs, options);

document.addEventListener('ConfigureSuccess', () => {  
   AdColony.requestInterstitialInZone(zoneIDs[0]);
});

document.addEventListener('AdColonyRequestFilled', () => {
 AdColony.showWithPresentingViewController();
});

document.addEventListener('AdColonyRequestClosed', () => {
  console.log('AdColonyPlugin: Interstitial ad closed.');
});

document.addEventListener('AdColonyRequestNotFilled', (error) => {
  console.log('AdColonyPlugin: Request interstitial failed with error: ' + error);
});

```

For a full working demo, I've created a Cordova App [AdColonyCordovaDemo on GitHub](https://github.com/ferdil/AdColonyCordovaDemo)


If you have saved some time using my work, do consider donating me something :-)

[Donations through PayPal gratefully accepted![paypal.me](https://www.paypalobjects.com/webstatic/paypalme/images/social/pplogo120_4_3.png)](https://www.paypal.me/LADEIRA137)

Original iOS only version Author:
[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=QVU9KQVD2VZML)
