# Twilio Video adaptable solution for Mendix
This Mendix app module adds high-quality  video (WebRTC) capability to your Mendix application powered by the [Twilio Video](https://www.twilio.com/docs/video) programmable API. 
The module includes a REST API connector including Video Room callback (webhook) support to synchronize Room and Participant status events with the Mendix database. 
Two Mendix pluggable widgets are included with working demo implementations for Responsive and Native applications.

![Videl call invitation](https://github.com/Entidad/farmworker-wallet-os-video/blob/main/docs/Video_call_invite.png) ![Video call incoming](https://github.com/Entidad/farmworker-wallet-os-video/blob/main/docs/Video_call_incoming.png) ![Video call](https://github.com/Entidad/farmworker-wallet-os-video/blob/main/docs/Twilio_Video_react-native.png)

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
1. Twilio Access Token Generator v2 (app module)
2. Encryption v10.0.6 (The module does not explicitly provide production-ready microflows to manage the `twilioCredential` configuration entity but it is highly-advised that the Mendix developer solve for encryption of the Twilio API key secret before deploying their app)
3. Native Mobile Resources v6.1.1
4. [Native Keep Awake](https://marketplace.mendix.com/link/component/118878) by Aiden v1.1.0 
5. Mendix React-Native pluggable widget [mendix-react-native-twilio-video-webrtc](https://github.com/Entidad/mendix-react-native-twilio-video-webrtc/releases/tag/v0.0.15)
6. Mendix React pluggable widget [mendix-web-twilio-video-webrtc](https://github.com/Entidad/mendix-web-twilio-video-webrtc/releases/tag/v1.0.3)
   
## Installation
1. Download module and run app locally in Mendix Studio Pro. Default app is configured to run on `http://localhost:8085/`

## Configuration
1. Configure the Twilio Video service from the [Twilio Console](https://console.twilio.com/)
   1. Optionally, configure a default [Status Callback URL](https://console.twilio.com/us1/develop/video/manage/room-settings) endpoint to enable webhook notifications. NOTE if running locally, you will need an HTTP relay service (e.g https://hookdeck.com/)
2. Configure twilioCredential to store Twilio API secrets securely in Mendix database
   1. Login as `demo_administrator` user to access the responsive Administration demo application: `TwilioVideo/_Demo/Responsive/Administration/Pages/TwilioVideoChat_Config`
   2. Save your Twilio API screts
3. Run Responsive demo application
   1. Login as `demo_user` to join a Video Room: `TwilioVideo/_Demo/Responsive/VideoRoom/Pages/VideoRoom_Web`
4. Run Native demo application to join a Video Room: `TwilioVideo/_Demo/Native/VideoRoom/Pages/Home_Native`

## Known bugs [optional]
To report bugs, submit an issue report on our [Github repo](https://github.com/Entidad/farmworker-wallet-os-video/issues)

## Frequently Asked Questions
1. Is the module production ready?
   * The TwilioVideo app module provides core building blocks for implementing Video chat features into your Mendix Responsive and/or Native apps, but the resources provided are not enough to deliver a production grade solution.
2. Can Mendix developers contribute to the source code to improve the solution components?
   * We welcome contributions and hope that Mendix developers who find this module useful would be interested in helping us making improvements. Please fork the repo and submit a PR request with bugs fixes or improvements. 
