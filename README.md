# Integrating Google Maps into React Native App on iOS

# Steps To Follow

# Step 1: Create React Native Application

# create a React Native application from scratch using react-native-cli

If you haven’t installed React Native, you can find how to install it in the official documentation.

Now we can create our app, simply using react-native init GoogleMap in a command line.

# Step 2: Install react-native-maps package

Let’s install the package with the following npm install --save react-native-maps command.
in your Project Directory via the command cd GoogleMap.

# Step 3: Configuration on iOS

Next, we run react-native link react-native-maps after which you should be able to use this library on iOS.

# Note that by default this will use Apple Maps and you will miss some of the features provided by Google. To enable Google Maps, we will follow the below instructions.

# Step 4: Enable Google Maps on iOS

# Note before performing the below steps please check the iOS folder by Navigate to “ios/” and check if Podfile exist or not.

# Podfile allready exist no need to run the following pod init command in the command line

For this we will need to use Cocoapods. We will create a Podfile where we will specify the dependencies of our iOS application.
Navigate to “ios/” folder in GoogleMap folder and run the following pod init command in the command line.

Setup Podfile (found as below, replacing all references to _YOUR_PROJECT_TARGET_ with our project target (it’s the same as project name by default, which in our case is "GoogleMap"). Copy and Paste below content and replace all references

# Pods for GoogleMap

# Add the below lines in the Podfile after this line ====>>>> # pod 'react-native-maps', :path => '../node_modules/react-native-maps'

pod 'react-native-google-maps', :path => '../node_modules/react-native-maps'
pod 'GoogleMaps'
pod 'Google-Maps-iOS-Utils'

# Next, we need to install the Pods. Run the following pod install command in the command line.

# Step 5: Create a Google Maps API Key

    # 1 In order to use Google maps, we will need to create a Google Maps API key.
        for this visit https://developers.google.com/maps/documentation/ios-sdk/get-api-key
            Click “Get Started” Button

    # 2 Then, we will see a section where we need to choose the project. Choose “Create a new project” in the drop-down menu and    name it “GoogleMap”, then click “Next”.

    After a few steps, we will see confirmation pop-up window, which says that “You’re all set”. Copy the “Key” for future actions.

# Open the project in Xcode

    Next, we will open the produced workspace file (.xcworkspace) in “XCode” to build our project.

# Step 6: Back to the Code

# To enable Google Maps on iOS, copy the Google API key and edit AppDelegate.m file. Insert these two lines into your AppDelegate.m file:

#import <GoogleMaps/GoogleMaps.h> //Line to be added

# inside - (BOOL)application:(UIApplication _)application didFinishLaunchingWithOptions:(NSDictionary _)launchOptions

# {

# #if DEBUG

# InitializeFlipper(application);

# #endif ===> after this line

[GMSServices provideAPIKey:@"_YOUR_API_KEY_"]; // add this line using the api key obtained from Google Console //Line to be added

Let’s build our project (“XCode -> Product -> Build”).

# After building the project if we get an error

First of all, in “Project Navigator” choose project “GoogleMap”. After, open section “Link Binary With Libraries” under “Build Phases”. Delete “libAirMaps.a” in the list, and try to rebuild project again.

# Step 7: Let’s begin building out the app by changing some codes in the App.js file

import React, {Component} from 'react';
import {StyleSheet, Text, View} from 'react-native';
import MapView, {PROVIDER_GOOGLE, Marker} from 'react-native-maps';

function App() {
return (
<View style={styles.container}>
<MapView
style={styles.map}
provider={PROVIDER_GOOGLE}
initialRegion={{
          latitude: 37.751,
          longitude: -97.822,
          latitudeDelta: 0.0922,
          longitudeDelta: 0.0421,
        }}>
<Marker
pinColor="red"
coordinate={{
            latitude: 37.751,
            longitude: -97.822,
            latitudeDelta: 0.0922,
            longitudeDelta: 0.0421,
          }}
/>
</MapView>
</View>
);
}

const styles = StyleSheet.create({
container: {
flex: 1,
},
map: {
flex: 1,
},
});

export default App;
