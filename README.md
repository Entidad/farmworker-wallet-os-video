# Twilio Video adaptable solution for Mendix
This Mendix app module adds high-quality  video (WebRTC) capability to your Mendix application powered by the [Twilio Video](https://www.twilio.com/docs/video) programmable API. 
The module includes a REST API connector including Video Room callback (webhook) support to synchronize Room and Participant status events with the Mendix database. 
Two Mendix pluggable widgets are included with working demo implementations for Responsive and Native applications.

![Video call peer](https://github.com/Entidad/farmworker-wallet-os-video/blob/main/docs/Video_call_peer.png) ![Video call outbound](https://github.com/Entidad/farmworker-wallet-os-video/blob/main/docs/Video_call_outbound.png) 

![Video call inbound](https://github.com/Entidad/farmworker-wallet-os-video/blob/main/docs/Video_call_inbound.png) ![Video call](https://github.com/Entidad/farmworker-wallet-os-video/blob/main/docs/Twilio_Video_react-native.png)

## Typical usage scenario
Connect your Mendix application with Twilio client SDKs (REST API, iOS, and Android) to your [Twilio Video](https://www.twilio.com/login) service subscription to provide peer-to-peer or multi-party group Video chat. 

## Features and limitations
The adaptable app module includes:

1. Domain model
2. Demo applications
* Administration app
* Responsive app
* Mobile Native app  
3. REST API consumer Microflows to create or update Video Room resources
4. REST service to process real-time asyncchronous Video Room [status callbacks](https://www.twilio.com/docs/video/api/status-callbacks)

## Dependencies
1. [Twilio Access Token Generator v3.0.0](https://marketplace.mendix.com/link/component/242851) (by Entidad)
2. Encryption v11.1.1 (The module does not explicitly provide production-ready microflows to manage the `twilioCredential` configuration entity but it is highly-advised that the Mendix developer solve for encryption of the Twilio API key secret before deploying their app)
3. Native Mobile Resources v12.2.1
4. Community Commons v11.5.1
5. [REST Responses](https://marketplace.mendix.com/link/component/118687) by MxLabs v2.1.0
6. [Native Keep Awake](https://marketplace.mendix.com/link/component/118878) by Aiden v3.0.0
7. NPM package [@twilio/video-react-native-sdk](https://github.com/twilio/react-native-twilio-video-webrtc) v3.5.0
8. Mendix React-Native pluggable widget [mendix-react-native-twilio-video-webrtc](https://github.com/Entidad/mendix-react-native-twilio-video-webrtc)
9. Mendix React pluggable widget [mendix-web-twilio-video-webrtc](https://github.com/Entidad/mendix-web-twilio-video-webrtc)
10. Xcode 16.2
11. Android Studio Quail 1 | 2026.1.1 Patch 2
   
## Installation
1. Download module and run app locally in Mendix Studio Pro. Default app is configured to run on `http://localhost:8085/`

## Configuration
1. Configure the Twilio Video service from the [Twilio Console](https://console.twilio.com/)
   - Optionally, configure a default [Status Callback URL](https://console.twilio.com/us1/develop/video/manage/room-settings) endpoint to enable webhook notifications: `https://<YOUR_DOMAIN_NAME>/rest/twilio/video/room-events`
   - NOTE if running locally, you will need an HTTP relay service (e.g https://hookdeck.com/)
2. Configure twilioCredential to store Twilio API secrets securely in Mendix database
   - Login as `demo_administrator` user to access the responsive Administration demo application: `TwilioVideo/_Demo/Responsive/Administration/Pages/TwilioVideoChat_Config`
   - Save your Twilio API screts
3. Install npm package
```
npm install @twilio/video-react-native-sdk@3.5.0
```
4. Edit Podfile for iOS distribution
```
# Add Twilio Video WebRTC pod   
pod 'twilio-video-react-native-sdk', path: '../node_modules/@twilio/video-react-native-sdk'  
```
6. Rebuild your native apps (See Native build section below)
7.  Run Responsive demo application
   - Login as `demo_user` to join a Video Room: `TwilioVideo/_Demo/Responsive/VideoRoom/Pages/VideoRoom_Web`
8. Run Native demo application to join a Video Room: `TwilioVideo/_Demo/Native/VideoRoom/Pages/Home_Native`

## Native build
The App Github repo now includes a pre-configured nativeTemplate [../resources/nativeTemplate](https://github.com/Entidad/farmworker-wallet-os-video/tree/main/resources/nativeTemplate) to fast-track demo activities.
1. Clone Github repo
2. Install npm packages
```
cd resources/nativeTemplate/
nvm install 24
nvm use 24
npm i --legacy-peer-deps
npm run configure
```
3. Edit iOS Podfile
```
# Add Twilio Video WebRTC pod 
pod 'react-native-twilio-video-webrtc', path: '../node_modules/react-native-twilio-video-webrtc'
```
4. If you have trouble distributing to Apple Test Flight due to a bitcode issue, edit iOS Podfile
```
bitcode_strip_path = `xcrun --find bitcode_strip`.chop!
    def strip_bitcode_from_framework(bitcode_strip_path, framework_relative_path)
      framework_path = File.join(Dir.pwd, framework_relative_path)
      command = "#{bitcode_strip_path} #{framework_path} -r -o #{framework_path}"
      puts "Stripping bitcode: #{command}"
      system(command)
    end

    framework_paths = [
      "Pods/TwilioVideo/TwilioVideo.xcframework/ios-arm64_armv7/TwilioVideo.framework/TwilioVideo"
    ]

    framework_paths.each do |framework_relative_path|
      strip_bitcode_from_framework(bitcode_strip_path, framework_relative_path)
    end
```
5. Install iOS pods
```
cd ios
pod install --repo-update
```

## Known bugs [optional]
To report bugs, submit an issue report on our [Github repo](https://github.com/Entidad/farmworker-wallet-os-video/issues)

## Frequently Asked Questions
1. Is the module production ready?
   * The TwilioVideo app module provides core building blocks for implementing Video chat features into your Mendix Responsive and/or Native apps, but the resources provided are not enough to deliver a production grade solution.
2. Can Mendix developers contribute to the source code to improve the solution components?
   * We welcome contributions and hope that Mendix developers who find this module useful would be interested in helping us making improvements. Please fork the repo and submit a PR request with bugs fixes or improvements. 
