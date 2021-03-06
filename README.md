# Ionic2eBook
Ionic2eBook is an ebook reader built with Ionic2, Angular2 and Cordova. This app allows authors to embed their book in this app and ship this app as a book while monetizing through AdMob advertisements.

This ebook reader displays each page with CSS multi-column layout. As each page is panned forward, this ebook will page to the next column on the right. Similarly, for each pan backwards, this ebook will page to the next column on the left.

All HTML5 content and CSS styling that can be displayed in CSS multi-column layout can be displayed by this eBook reader.

The advantages of this eBook reader are:
- Ability to track usage statistics using Firebase Analytics. Each pan of a page is tracked.
- Ability to monitize content using AdMob advertisements.
- Runs on both Android and iOS.
- Runs on a browser without advertisements and tracking. Code can be improved to support both.

## Example Use of This eBook
This eBook is used to publish the following books on the following platforms:
- [iOS, Malaysian Labour Law Abridged](https://itunes.apple.com/pk/app/malaysian-labour-law-abridged/id991514757?mt=8)
- [Android, Malaysian Labour Law Abridged](https://play.google.com/store/apps/details?id=com.singularmosaic.malaysianlabourlaw&hl=en)

## Install Ionic2, Angular2 and Cordova
```
npm install -g cordova ionic
```

## Download The Source Code and Libraries
```
git clone https://github.com/pinocchio-geppetto/ionic2ebook.git
cd ionic2ebook
npm update
```

## Compile and Run on a Web Browser
```
ionic serve
```

## Compile and Run on iOS
1. Run `ionic platform add ios`
2. Install XCode as described in https://cordova.apache.org/docs/en/latest/guide/platforms/ios/.
3. Register an iTunesConnect developer account as described in the iOS section here: http://ionicframework.com/docs/guide/publishing.html.
4. Run `ionic build ios --prod --release`.
5. Sign your app as in (3) above.
6. Upload and run the generated app on an iOS device or on an emulator using XCode.
7. Publish your eBook as described in the iOS section: http://ionicframework.com/docs/guide/publishing.html.

## Compile and Run on Android
1. Run `ionic platform add android`
2. Install AndroidStudio as described in https://cordova.apache.org/docs/en/latest/guide/platforms/android/index.html.
3. Generate your keystore and replace it with the existing keystore as described here: http://ionicframework.com/docs/guide/publishing.html. The [existing keystore](https://github.com/pinocchio-geppetto/ionic2ebook/blob/master/ionic2ebook.keystore) will continue to work but you will not want to publish your app using this keystore.
4. The passowrd to the keystore in (3) above is stored here: [password to existing keystore](https://github.com/pinocchio-geppetto/ionic2ebook/blob/master/ionic2ebook.keystore.password) in case it becomes handy.
5. Run `ionic build android --prod --release'.
6. Upload and run the generated app on an Android device or on an emulator.
7. Publish your eBook as described in the Android section: [http://ionicframework.com/docs/guide/publishing.html](http://ionicframework.com/docs/guide/publishing.html).

Note that this eBook uses Crosswalk and Crosswalk (as of this writing using AndroidStudio version 2.3, and Android SDK Tools 25.0.3) does not display on Android emulators and GenyMotion. Crosswalk will display on actual devices and can be tested this way.

# Place Content Into This eBook
This ebook relies on HTML5 and CSS styling which is paged with CSS multi-column layout. Any HTML5 and CSS styling which is supported by CSS multi-column layout will work with this eBook.

The examples inside the book shows how Table Of Contents should be displayed. It is self explanatory.

Reserved tags are used by this eBook to represent special positions within the content. They are:
1. id="Preface"
This id is used to identify the begining of the book that is just past the table of content. This eBook will not remember last position read by the reader if the reader is at the Table of Content.

2. id="_Toc417167144"
This is the "chapter 1" tag. The book will scroll here if it has never been viewed before.
It is the first page displayed if the book is opened for the very first time.

3. The last empty `<p></p>` tag at the very end of the book is needed to signify the end of book. The Safari browser is not able to return the correct coordinates within the eBook when the last paragraph spans more than one column if this empty is not placed at the very end. Keep this empty paragraphy as the last paragraph.

# Configuration
Configure your eBook to track usages statics using Firebase and to monitize your eBook using AdMob.

## Configure Firebase Analytics
Register a Firebase account. For each platform, do the following:
1. For Android, update ionic2ebook/google-services.json with a new download from your Firebase console. Formore information: https://firebase.google.com/docs/android/setup.
2. For iOS, update ionic2ebook/GoogleService-Info.plist with a new download from your Firebase console. For more information: https://firebase.google.com/docs/ios/setup.

If the firebase files above are not updated, the app will continue to work but there will be no Firebase reporting.

## Configure AdMob
Register an AdMob account. For each platform, do the following:
1. For Android, edit the file ionic2ebook/src/app/service/interstitial-ads.service.ts. In the constructor of the class `class InterstitialAdsService`, update `adId` to your AdMob `adId`.
2. For Android, edit the file ionic2ebook/src/app/service/interstitial-ads.service.ts. In the constructor of the class `class InterstitialAdsService`, update `adId` to your AdMob `adId`.

```
    if (this.platform.is('ios')) {
      this.adOptions.adId = 'ca-app-pub-3940256099942544/4411468910', // test from firebase. Change this to your adId
      console.log('ios ad selected.');
    }
    else if (this.platform.is('android')) {
      this.adOptions.adId = 'ca-app-pub-3940256099942544/4411468910', // test from firebase. Change this to your adId
      console.log('andoird ad selected.');
    }
```
