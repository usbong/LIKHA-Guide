# LIKHA Guide

This is a guide for creating LIKHAs using the LIKHA Xcode project found [here](https://github.com/chrisamanse/LIKHA).

This guide is divided into three parts:

1. [Customizing LIKHA](#1-customizing-likha)
2. [App Store Deployment](#2-app-store-deployment)
3. [In-App Purchases](#3-in-app-purchases)

## Setup

Download the LIKHA repo [here](https://github.com/chrisamanse/LIKHA). To start customizing LIKHA, open the `LIKHA.xcworkspace` using Xcode 7.3.1.

## 1. Customizing LIKHA

1. To use your own utree, simply replace `LIKHA.utree` which is found in the main folder of the repo. It is important to use the same filename for the utree as the app looks for a utree with the filename `LIKHA` and file extension `utree`. If you plan to upload the app in the App Store, you should also replace the Bundle Identifier value found in `LIKHA` using Xcode (The identifier is in the reverse domain format - com.example.identifier). If you already have an Apple Developer account set up, you can also select your team there.

  ![](./Screenshots/Part 1/1.png)

2. To change the app name displayed below the App Icon in the homescreen, replace the value of "Bundle name" in `Info.plist`.

  ![](./Screenshots/Part 1/2.png)
  
3. To customize the About text shown in the About part of the app, edit the contents of `About.txt`.

  ![](./Screenshots/Part 1/3.png)

4. You can replace the images found in the app in `Assets.xcassets`. For the App Icon, you need to use image sizes which is defined below each group (29 pt means 29x29 and 2x for 29pt means 58x58, and so on). To quickly generate these images, use an app icon generator such as [Iconizer](http://raphaelhanneken.github.io/iconizer/).

  ![](./Screenshots/Part 1/4.png)
  
  ![](./Screenshots/Part 1/5.png)

5. To run the app using the simulator, choose "LIKHA" target from the dropdown selection on the right of the Start/Stop buttons found in the top left part of Xcode. You can also choose which type of device to run.

  ![](./Screenshots/Part 1/6.png)


## 2. App Store Deployment

1. To distribute your app to the App Store, you need to have an Apple Developer Program membership. To upload the app, you need to create an App ID in the [Apple Developer account page](https://developer.apple.com), and go to Certificates, Identifiers and Profiles. Create an App ID with a Bundle Identifier that corresponds with the Bundle Identifier of your app.

  ![](./Screenshots/Part 2/1.png)

  ![](./Screenshots/Part 2/2.png)

  ![](./Screenshots/Part 2/3.png)

2. After creating the App ID, you need to create a Provisioning Profile in the same page. Go to the Provisioning Profiles section and click add. In the Add Provisioning Profile page, select App Store in Distribution. Press Next, and select the App ID you just created. In the next page, select your Distribution certificate.

  ![](./Screenshots/Part 2/4.png)
  
  ![](./Screenshots/Part 2/5.png)
  
  ![](./Screenshots/Part 2/6.png)

3. After you create the Provisioning Profile, you can download it directly from the browser. Alternatively, you can also download it from Xcode by going to Preferences > Accounts, then choosing View Details on the Developer Team in your Apple ID account.

  ![](./Screenshots/Part 2/7.png)
  
  ![](./Screenshots/Part 2/8.png)
  
4. Once you have the App ID, you can now create your app in [iTunes Connect](https://itunesconnect.apple.com). Create the app, then choose the App ID you created.

  ![](./Screenshots/Part 2/9.png)

5. Also, once you've downloaded your Provisioning Profile, set it on your LIKHA project in Build Settings as shown in the screenshot. You need to change the Release part of Code Signing and Provisioning Profile part of the Build Settings.

  ![](./Screenshots/Part 2/10.png)

6. Now that you have configured the settings of your project, you can now submit your app by first archiving your app. Choose LIKHA > Generic iOS Device, in the Scheme and Destination dropdown in the top left of the Xcode window as shown in the screenshot. To archive, go to Product > Archive.

  ![](./Screenshots/Part 2/11.png)

7. After archiving has finished, Xcode will automatically open the Organizer Window (You can manually open it in the menu bar Window > Organizer). Choose your app and archive in the window. You'll see options on the right sidebar of the window to upload to the App Store, Validate or Export. Choose Upload to App Store to upload the app to iTunes Connect (If you already have archives of the app uploaded to iTunes Connect, make sure that the current build number of the current archive does not yet exist, else, the upload will fail and Xcode will prompt you that the archive with that build number already exists).

  ![](./Screenshots/Part 2/12.png)


## 3. In-App Purchases

1. To add In-App Purchases (IAP), go to your app page in iTunes Connect. Click the "+" sign to add an In-App Purchase. Choose a Non-Consumable purchase, since language bundles need only to be purchased once. Input the Reference Name, which will be used for sales reports, and the Product ID, which will be used for fetching IAP items from the app. Choose the Pricing Matrix.

  ![](./Screenshots/Part 3/1.png)
  
  ![](./Screenshots/Part 3/2.png)
  
  ![](./Screenshots/Part 3/3.png)
  
2. In the In-App Purchase Details, add a title and description of the IAP by adding a Language. This will be displayed in the App Store and in the app. Since this app only uses English localization **natively** (it uses UsbongKit for translations), only English language is needed for the IAP description. In the bottom part, you'll also need a screenshot of the IAP in action (the app showing that the IAP being used) for Apple to review it. You can do this later after you add it in your app.
  
  ![](./Screenshots/Part 3/4.png)
  
  ![](./Screenshots/Part 3/5.png)
  
3. To add the IAP in your app, go back to Xcode and edit `LIKHABundles.plist`. An example is already there which you should replace. In the Root item with Dictionary type, add an Array type item with the IAP Product ID as the key, i.e. `com.example.language_bundle`. In the Array, add the languages that this bundle will unlock. Repeat for every IAP item. Finally, test the app if the languages are locked.

  ![](./Screenshots/Part 3/6.png)
  
  ![](./Screenshots/Part 3/7.png)

4. To test the purchasing of these items, you'll need to create "Sandbox Users" in iTunes Connect. These users are simply used for testing. Go to iTunes Connect, then Users and Roles to create these Sandbox Users. Make sure to remember the password for these users. To test purchasing, you'll need to run your app in a real device. You can run it by connecting the device in your Mac and choosing the device in Xcode. While in the device, make sure the App Store user is the Sandbox User you created.

  ![](./Screenshots/Part 3/8.png)
  
  ![](./Screenshots/Part 3/9.png)
  
  ![](./Screenshots/Part 3/10.png)
  
  ![](./Screenshots/Part 3/11.png)

5. You can now follow the steps in [App Store Deployment](#2-app-store-deployment) to upload your app to iTunes Connect.

To learn more about distributing apps in the App Store, you can go to the Apple Developer Resources for detailed guides, such as [App Distribution Guide](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/).


Copyright (c) 2016 Usbong Social Systems, Inc.
