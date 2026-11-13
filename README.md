# Desk Calm

A Windows desktop app for the Presage SmartSpectra SDK Challenge.

Desk Calm watches a webcam and shows a live breathing rate from the Presage SmartSpectra SDK. One sentence under the camera changes with that number, so someone at a desk can take a short still break.

This is a wellness cue. It is not a medical device, and it does not diagnose or treat anything.

## What changes on screen

| Breaths per minute | Banner |
| --- | --- |
| No number yet | Sit still. The breathing number needs about 30 seconds. |
| 20 or more | Breathing looks quick. Drop your shoulders and slow down. |
| 13 to 19 | Steady. This is a good desk pace. |
| 12 or less | Breathing looks slow and quiet. Stay with it. |

Breathing is always measured. Cardio and face metrics are optional toggles from the SmartSpectra sample and are not required for the banner.

## Consent and data

- Start stays disabled until you tick "I allow this app to use my camera while it is open. Video is not saved."
- The camera turns on only after Start, and turns off on Stop.
- Frames are handled inside the SmartSpectra SDK on this computer. This app does not write video, screenshots, or measurements to disk.
- This app does not upload video to its own server. The SDK contacts Presage only to check the API key.
- Nothing in this app is shared with a third-party AI service.
- Close the window to release the camera.

## What you need

- Windows 10 or 11, with a webcam
- Node.js 22.12 or newer
- A free Presage API key from https://physiology.presagetech.com/

## Run it

cd signal-desk
npm install

Open renderer.js. Find this line:

const API_KEY = 'YOUR_API_KEY_HERE';

Replace YOUR_API_KEY_HERE with your own key. Do not commit that key.

Then:

npm start

Use Command Prompt or PowerShell, not the VS Code integrated terminal. VS Code sets ELECTRON_RUN_AS_NODE=1, which makes Electron quit immediately.

In the window:

1. Tick the camera consent box. Start becomes clickable.
2. Click Start.
3. Sit still, with your face and upper chest in frame and the room reasonably bright.
4. Wait about 30 seconds. The breathing number and the colored sentence should update.
5. Click Stop. The camera preview goes dark.

## Project layout

- main.js: Electron window. Allows the camera permission prompt.
- index.html: Desk Calm layout, consent checkbox, calm banner.
- renderer.js: SmartSpectra SDK, charts, banner rules, consent gate.
- styles.css: Layout and banner colors.

The SDK sample this started from is the official Electron quickstart in Presage-Security/SmartSpectra.

## Measurement notes

The breathing number is a roughly 30-second average from the SDK. It works best when you are still, the camera is stable, and your face and chest are visible and well lit. Talking, large movement, a shaky camera, or very dark clothes can make the number unreliable. The banner is only a prompt to slow down or stay with a quiet pace.