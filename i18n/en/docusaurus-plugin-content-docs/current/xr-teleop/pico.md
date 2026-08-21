---
title: USER MANUAL FOR PICO
sidebar_label: PICO
sidebar_position: 1
---

<div className="bingru-theme" />

import GearIcon from './Screenshots/gear.svg';

# USER MANUAL FOR PICO

Human-Robot TeleOperation for Pico

Latest version:  [`download`![download](./Screenshots/download.svg)](https://github.com/KLMmotion/km_teleop_openxr/releases)

Tianji | KernalMind

## Open app

Uninstall the previous Apex_teleop App. Install latest .apk to your headset, open with two controllers keeping tracked. Agree to popups.

## Check your setups

### Battery

Make sure your headset battery is above 20%, or the warning message would pop up and you may not start using teleoperation for safety concerns.

<figure>
    <img src={require("./Screenshots/ss_charge.jpg").default} alt="Low battery warning message" />
    <figcaption>Low battery warning message</figcaption>
</figure>

### Internet

Make sure your headset is connected to host through USB hub and LAN cable for best experience. You are strongly suggested to turn off WiFi in headset in case of any interference during operation. Click on the button below the message to open WiFi setting panel.

<figure>
    <img src={require("./Screenshots/ss_wifi.jpg").default} alt="WiFi setting" />
    <figcaption>WiFi setting</figcaption>
</figure>

### Controller Battery

Check your controller battery level before using. If it is too low, the controller will not be able to track and you will not be able to use teleoperation. You may need to charge it or replace batteries for a while and try again. The controller icon near the battery icon shows the real-time tracking status provided by OpenXR Runtime, not the battery numbers.

### Room Boundary

We use your room boundary settings to determine the location of the real-world floor and display the position of the virtual robotic arm. If you haven't set up your room boundary, the system UI and virtual robotic arm may appear too high or too low during teleoperation. Please check if your room boundary is correctly configured in <i><b>Settings > General > Room Boundary</b></i>. You must setup the floor height correctly.

### Language

You can change the language by clicking the language dropdown button in the upper left bar of the main panel. We support English, Chinese and Japanese for current version. The change will take effect on speech announcement feature as well.

<figure>
    <img src={require("./Screenshots/teleop_language.jpg").default} alt="Language setting" />
    <figcaption>Language setting</figcaption>
</figure>

## Important Configurations

### Robot End-effector Configuration

This option allows you to freely switch the robotic arm's end-effector configuration, typically between a dexterous hand or a gripper. Depending on the manufacturer's actuator, the corresponding configuration on the XR teleoperation side must also be adjusted.

<figure>
    <img src={require("./Screenshots/teleop_endeffector.jpg").default} alt="Connect to host and end-effector settings" />
    <figcaption>Connect to host and end-effector settings</figcaption>
</figure>

If the robotic arm is equipped with a gripper select Controller.

If the robotic arm is equipped with a dexterous hand select Gloves on the XR side (currently supporting either Manus or UDCAP).

<div style={{display: 'flex', justifyContent: 'space-between', gap: '10px'}}>
    <figure style={{margin: 0, width: '48%'}}>
        <img src={require("./Screenshots/PicoAxis_MANUS.jpg").default} alt="Manus" style={{width: '100%'}} />
        <figcaption>Manus</figcaption>
    </figure>
    <figure style={{margin: 0, width: '48%'}}>
        <img src={require("./Screenshots/PicoAxis_UDCAP.jpg").default} alt="UDCAP" style={{width: '100%'}} />
        <figcaption>UDCAP</figcaption>
    </figure>
</div>

### Transport Protocol

#### Best-Effort

This mode uses UDP to send tracking data. It is the default mode and is recommended for most users. However this causes packet drop and may have jitters. You are recommended to choose this mode when you have good network connection like wired connection.

#### Reliable

This mode uses TCP to send tracking data. It is slower and may have higher latency. You are recommended to choose this mode when you have bad or unstable network connection, like Wi-Fi.

### Body Tracking

#### PICO Full-body Tracking Feature

When using the data from PICO full-body tracking feature, wear at least 2 PICO trackers (recommond 3, left and right feet, and waist).open PICO Motion Tracker app to setup, calibrate and back to our app after setting up. The button below would open Motion Tracker app directly.

<div style={{display: 'flex', justifyContent: 'space-between', gap: '10px'}}>
    <figure style={{margin: 0, width: '48%'}}>
        <img src={require("./Screenshots/ss_motiontracking.jpg").default} alt="Motion tracking feature" style={{width: '100%'}} />
        <figcaption>Motion tracking feature</figcaption>
    </figure>
    <figure style={{margin: 0, width: '48%'}}>
        <img src={require("./Screenshots/fullbody.jpg").default} alt="Full-body tracking 24 nodes schematic" style={{width: '100%'}} />
        <figcaption>Full-body tracking schematic</figcaption>
    </figure>
</div>

#### Effortless Full-body Tracking

:::tip Tip
This feature is supported after version 1.0.8
:::

This feature is an alternative for PICO full-body tracking feature. It is designed for trackerless teleoperation, taking use of left/right controller and head position to simulate full-body ik within the app. Before using, please make sure the controller and head tracking keep tracked, and switch the mode to this option, click on `Calibrate` and stretch your arms for 5 seconds. If the skeleton shows up, you're ready to go.

<figure style={{margin: 0, width: '100%'}}>
    <img src={require("./Screenshots/EffortlessFullbody_skeleton.jpg").default} alt="Effortless full-body tracking" />
    <figcaption>Teleoperation in Effortless Full-body Tracking mode</figcaption>
</figure>

## Connect to host

This interface would be shown after you enter the app.

Please enter your host IP address and your height (in cm). You can click the button above the height input field to get an estimated value. If a host address is detected, a button reading `ApexHost XXX.XXX.XXX.XXX` will also appear above the IP input field; click it to auto-fill the host address into the field.

You can also change the end-effector configuration directly on the main panel (the button is located above the `Connect` button). Switch the origin configuration of the robotic arm sent out in XR based on different situations (e.g., Gripper, Dexhand) to calibrate the tracker position.

:::tip Tip
You must exit teleoperation to change configuration, the button remains uninteractable while you are manipulating the robot.
:::

Once you fill IP and height, click on `Connect` button to connect to host.

- Connect successfully: 
    - You will receive two short vibration on controllers both hands.
    - The `Connection` icon will change.
- Connect fail: 
    - You will receive a long vibration on controllers both hands.
    - The `Connection` icon does not make any changes.

### Host Recording

Press the `B` button on your right controller to notify the host to start or stop recording. Voice prompts will indicate whether the recording started successfully or failed.
Before using this feature, please ensure that the HTTP connection between the headset and the host is functioning correctly. You can verify this by checking the recording icon on the main panel; if there is no exclamation mark, it indicates the current connection is normal.

## How to start and end teleoperation

After connect to the host, you can start teleoperation by pressing the `Y` button on your left controller. The interface would show you the status of connection. In this mode, you can use the controllers to control the robot. Press the `X` button to end teleoperation. There will be voice prompts when starting and ending the process. If a low battery or device disconnection occurs during operation, the teleoperation will automatically disconnect, accompanied by controller vibrations.

Align your hand with the virtual robotic arm and hold the `Grip` button to start teleoperating. Release the Grip button to pause. We strongly recommend pressing the `X` button to exit teleoperation completely whenever you are paused or not actively controlling the arm.

On the main panel, if the left and right controller icons are lit up and not red, it indicates that the controller tracking is normal.

During teleoperation, you will see the video streaming views as shown below:

<div style={{display: 'flex', justifyContent: 'space-between', gap: '10px'}}>
    <figure style={{margin: 0, width: '49%'}}>
        <img src={require("./Screenshots/teleop_wifi_connectingvideo.jpg").default} alt="Connecting video stream" style={{width: '100%'}} />
        <figcaption style={{textAlign: 'center', fontSize: '0.9em'}}>Connecting video stream</figcaption>
    </figure>
    <figure style={{margin: 0, width: '49%'}}>
        <img src={require("./Screenshots/teleop_wifi_connectedvideo.jpg").default} alt="Connected video stream" style={{width: '100%'}} />
        <figcaption style={{textAlign: 'center', fontSize: '0.9em'}}>Connected video stream</figcaption>
    </figure>
</div>

<figure style={{marginTop: '15px'}}>
    <img src={require("./Screenshots/teleop_video_focused.jpg").default} alt="Robotic arm right wrist camera stream" style={{width: '100%'}} />
    <figcaption style={{textAlign: 'center', fontSize: '0.9em'}}>The user is viewing the camera stream from the robotic arm's right hand to assist in fine-grained manipulation</figcaption>
</figure>

In the focused view, besides the main binocular camera stream in the center, you can also see the video streams from the left and right wrist cameras on both sides of the robotic arm. This added detail significantly enhances the accuracy of teleoperation control.

## Stream and Play the XR App

:::tip Tip
This feature is supported after Version 1.0.8.
:::

Once you opened the teleoperation app, the stream link will appear at the bottom of the main panel, as what is showed below:

<figure>
    <img src={require("./Screenshots/videosender_showip.jpg").default} alt="XR view stream" />
    <figcaption>XR view stream</figcaption>
</figure>

You can open this stream in your computer browser by entering the link shown above into the browser. You device and the XR device must be under the same network.

There are two modes when viewing XR stream: `First-Person` and `Free Cam` mode. In `Free Cam` mode you can drag and click. This mode is designed for assisting the non-professional users, `First-Person` mode is view-only . There are three modes of stream quality: `low`, `regular`, and `high`.

<div style={{display: 'flex', justifyContent: 'space-between', gap: '10px'}}>
    <figure style={{margin: 0, width: '49%'}}>
        <img src={require("./Screenshots/videosender_showcase.jpg").default} alt="XR screencast" style={{width: '100%'}} />
        <figcaption style={{textAlign: 'center', fontSize: '0.9em'}}>XR Screencast to PC and Pad</figcaption>
    </figure>
    <figure style={{margin: 0, width: '49%'}}>
        <img src={require("./Screenshots/videosender_pad.jpg").default} alt="Connected video stream" style={{width: '93%'}} />
        <figcaption style={{textAlign: 'center', fontSize: '0.9em'}}>Free Cam mode, interaction showcases.</figcaption>
    </figure>
</div>

## How to enter Developer Mode

:::warning Warning
This is for developer use only. You may bring safety issues to both of your device and the robot. Please enable it only when you know what you are doing.
:::

Click on <GearIcon style={{width: '20px', height: '20px', verticalAlign: 'middle', display: 'inline-block'}} /> logo on the top row of the panel to open developer panel. You will see new options appear next to the main panel. The App uses TCP for host communication, UDP for robot control and receives teleoperation data from robot, and WebRTC for video streaming.

Click again to close developer panel.

<figure>
    <img src={require("./Screenshots/teleop_debugmode.jpg").default} alt="Developer Mode" />
    <figcaption>Developer Mode</figcaption>
</figure>

What can you do in Developer Mode?

In developer mode, you can check the communication details and specific logs between the host and the headset, monitor video transmission and decoding status, configure individual ports, and perform other advanced and fine-grained configurations:

- Change Host connection, Spatial Video, and Data ports **individually**.
- Test Host connection, Spatial Video, and Data connection status and disconnect/connect them individually.
- See App log regarding to Host connection, Spatial Video, and Data.

## Safety check

[To be updated.]

## Lookup table for interactions

<table>
  <thead>
    <tr>
      <th>Controller</th><th>Button</th><th>Function</th><th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Left Hand</td><td>Menu Button</td><td>Maximize/Minimize Panel</td>
      <td rowSpan={13}>
        <figure style={{margin: 0}}>
          <img src={require("./Screenshots/picoultracontroller.png").default} alt="Pico 4 Ultra Controller" width={380} />
          <figcaption style={{textAlign: 'center'}}>Pico 4 Ultra Controller</figcaption>
        </figure>
      </td>
    </tr>
    <tr><td>Left Hand</td><td>Y Button</td><td>Start teleoperation</td></tr>
    <tr><td>Left Hand</td><td>X Button</td><td>Exit teleoperation</td></tr>
    <tr><td>Right Hand</td><td>A Button</td><td>Robot pose reset</td></tr>
    <tr><td>Right Hand</td><td>B Button</td><td>Start/Stop host recording</td></tr>
    <tr><td>Right Hand</td><td>Menu Button</td><td>Hold to reset XR origin</td></tr>
    <tr><td>Both Hands</td><td>Trigger</td><td>Click UI, Control Gripper</td></tr>
    <tr><td>Both Hands</td><td>Grip</td><td>Hold to control robot</td></tr>
    <tr><td>Left Hand</td><td>Thumbstick(Press and push)</td><td>Robot base rotation</td></tr>
    <tr><td>Right Hand</td><td>Thumbstick(Press and push)</td><td>Robot base translation</td></tr>
    <tr><td>Left Hand</td><td>Thumbstick(Long press)</td><td>Enable full-body chassis control</td></tr>
    <tr><td>Right Hand</td><td>Thumbstick(Long press)</td><td>Enable thumbstick chassis control</td></tr>
    <tr><td>Both Hands</td><td>Thumbstick(Long press both)</td><td>Disable chassis movement</td></tr>
  </tbody>
</table>

## Known issues

### Why does the robotic arm twitch or slowly drift when the controller is fully occluded?

This system uses optical tracking between the headset and controllers. If the controller is fully occluded, tracking is lost. However, detecting tracking loss requires a brief time threshold. If the controller is abruptly blocked and quickly restored, the underlying system may fail to notify the application layer in time.

While we have implemented jitter filtering for safety, slow pose drift cannot be entirely eliminated. **If users notice any slow drifting during teleoperation, they should stop operating immediately.**

Control of the robotic arm will automatically and immediately halt if optical tracking is confirmed lost or if controller batteries are depleted.
