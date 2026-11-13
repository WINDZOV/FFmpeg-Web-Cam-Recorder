## PowerShell FFmpeg Webcam Recorder

A lightweight PowerShell function that uses FFmpeg to record video and audio simultaneously from your DirectShow devices, bypassing the standard Windows video recording limits (the 3-hour cap).

## Prerequisites

Install FFmpeg (via winget):
```
winget install Gyan.FFmpeg
```
## Setup & usage

Create your PowerShell profile script file (it will be created only if it doesn't exist):
```
if (!(Test-Path $PROFILE)) { New-Item -Type File -Force $PROFILE }
```
Create a directory for videos:
```
New-Item -ItemType Directory -Force -Path "C:\Users\YourUsername\videos"
```
Find the names of your audio and video devices to insert them into the function:
```
ffmpeg -list_devices true -f dshow -i dummy
```
Open the file to edit:
```
notepad $PROFILE
```
Add your cam function:
```
function cam {
    $date = Get-Date -Format "yyyy-MM-dd_HH-mm-ss"
    ffmpeg `
    -f dshow `
    -i video="YourVideoDeviceName" `
    -f dshow `
    -i audio="YourAudioDeviceName" `
    -c:v libx264 `
    -preset veryfast `
    -c:a aac `
    "C:\Users\YourUsername\videos\cam_$date.mp4"
}
```
Save, close, reload your profile:
```
. $PROFILE
```
Then run:
```
cam
```
To stop recording press `q`
