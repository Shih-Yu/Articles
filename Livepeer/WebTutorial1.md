# How to stream live with Livepeer

In this article, we will go through all the steps to build a simple website using html that will playback our live stream using Livepeer.

## Workflow for live streaming

When creating a live stream there are some equipments involved for the streamer. A live stream needs to have a `video source` for capturing the visuals, an `audio source` to capture the sounds, if any that goes with the video. After that is established, the raw data from both sources needs to be `encoded` so that it can be trasmitted over the internet. Afterwards, this data then needs to be converted to the ideal formats regardless of what the device is for viewing. This is what the `transcode` does. Finally, a `player` of some sort is used to play back the final version of the data and is what the viewer will see.

Below are simplified steps to create a simple live stream:

- [ ] Video source - built-in camera from computer

- [ ] Audio source - built-in microphone from computer

- [ ] Encoder - OBS software

- [ ] Transcoder - Livepeer

- [ ] Video player - JWPlayer

We will do the following steps:

- [ ] Create [Livepeer](https://livepeer.com/) account

- [ ] Create a [JWPlayer](https://www.jwplayer.com/) account

- [ ] Download [OBS](https://obsproject.com/) broadcaster

- [ ] Create our project

### Using Livepeer

- [ ] Open a browser and go to [Livepeer](https://livepeer.com/register) site and sign up for a free account.

<details><summary>See Image</summary>

![Livepeer Site](https://github.com/Shih-Yu/Articles/blob/9dc1d2957dfde7101ed59c26eb659d4d687548d3/Livepeer/assets/WebTutorial/Livepeer1.png)

![Livepeer Site](https://github.com/Shih-Yu/Articles/blob/9dc1d2957dfde7101ed59c26eb659d4d687548d3/Livepeer/assets/WebTutorial/Livepeer2.png)

</details>

- [ ] Once an account is created and logged in, select the `Stream` link from the left side menu. Click on the `+ Create Stream` button and give your stream a name.

<details><summary>See Image</summary>

![Livepeer Site](https://github.com/Shih-Yu/Articles/blob/9dc1d2957dfde7101ed59c26eb659d4d687548d3/Livepeer/assets/WebTutorial/Livepeer3.png)

![Livepeer Site](https://github.com/Shih-Yu/Articles/blob/9dc1d2957dfde7101ed59c26eb659d4d687548d3/Livepeer/assets/WebTutorial/Livepeer4.png)

![Livepeer Site](https://github.com/Shih-Yu/Articles/blob/9dc1d2957dfde7101ed59c26eb659d4d687548d3/Livepeer/assets/WebTutorial/Livepeer5.png)

</details>

> This should create a dashboard for this stream and provide information that we will need for other set up processes. For now, we will only need the `Stream Key`, `RTMP ingest URL`, and the `Playback URL`.

<details><summary>See Image</summary>

![Livepeer Site](https://github.com/Shih-Yu/Articles/blob/9dc1d2957dfde7101ed59c26eb659d4d687548d3/Livepeer/assets/WebTutorial/Livepeer6.png)

</details>

### Using JWPlayer

- [ ] In a separate browser tab, go to [JWPlayer](https://info.jwplayer.com/sign-up/) and sign up for a free account.

<details><summary>See Image</summary>

![JWPlayer Site](https://github.com/Shih-Yu/Articles/blob/9dc1d2957dfde7101ed59c26eb659d4d687548d3/Livepeer/assets/WebTutorial/JWPlayer1.png)

![JWPlayer Site](https://github.com/Shih-Yu/Articles/blob/9dc1d2957dfde7101ed59c26eb659d4d687548d3/Livepeer/assets/WebTutorial/JWPlayer2.png)

</details>

- [ ] Click on the `Upload from URL` button and paste in the `Playback URL` from Livepeer.

<details><summary>See Image</summary>

![JWPlayer Site](https://github.com/Shih-Yu/Articles/blob/9dc1d2957dfde7101ed59c26eb659d4d687548d3/Livepeer/assets/WebTutorial/JWPlayer3.png)

</details>

> For this tutorial, we can just select the `No, don't host media on import` option.

- [ ] Then click on `Add URLs` button and player is created for our live streaming.

<details><summary>See Image</summary>

![JWPlayer Site](https://github.com/Shih-Yu/Articles/blob/9dc1d2957dfde7101ed59c26eb659d4d687548d3/Livepeer/assets/WebTutorial/JWPlayer4.png)

![JWPlayer Site](https://github.com/Shih-Yu/Articles/blob/9dc1d2957dfde7101ed59c26eb659d4d687548d3/Livepeer/assets/WebTutorial/JWPlayer5.png)

</details>

### Installing OBS

- [ ] Go to [OBS](https://obsproject.com/) website and download the format that suites your computer.

- [ ] Install OBS and open the software.

- [ ] Select the `settings` button on the menu located in the bottom right corner of the app, then click on `Stream` option on the left side of the menu.

- [ ] Here is where we will add information for Livepeer streaming, enter the following information:

  - [ ] Service: `custom`

  - [ ] Server: `RTMP ingest URL` from Livepeer

  - [ ] Stream Key: `Stream Key` from Livepeer

- [ ] Click `ok` button and back in the OBS interface

  - [ ] We need to add a source before before we can start live streaming

  - [ ] Under ther source window on the bottom, click `+` and select `Video Capture Device`

  - [ ] Then give it a name and click `ok`

  Now we will select a device, which should be the default camera from your computer. Once it is selected, you should be able ot see the camera turn on and displaying an image. Click on the `ok` button and it should take you back to the interface.

  We you click `Start Stream` you should see the same stream in the Livepeer page as well as the JWPlayer page.

  We are now up and running for live streaming, but lets make this viewable on a simple webiste so others can see.

  > Before we start the website, first get the embed code from JWPlayer by clicking the `Embed` button on the top of the page next to the red `Save` button. A window should pop up and give you option to select the type of embed code. For this example, we will choose the IFrame format. Copy this code and we will add it to our website.

### Directory and file setup

Find a location on your computer for where you want this file to be stored. Create a directory for it and a html file.

```sh
mkdir streamDemo && touch index.html
```

Now lets change into the directory that we just created and open it with the code editor of your choice.

```sh
cd streamDemo
```

In the `index.html` file, we will create a simple web page, enter the code below into the file.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Web Stream Demo</title>
  </head>
  <!-- Internal CSS styling  -->
  <style>
    body {
      background-color: #0c0908;
    }

    h1 {
      text-align: center;
      margin-top: 100px;
      color: #8777d6;
    }

    .flex-container {
      display: flex;
      justify-content: center;
      margin-top: 100px;
    }

    iframe {
      border: 3px solid#8777D6;
      border-radius: 5px;
    }
  </style>

  <body>
    <!-- Title of the page -->
    <h1>Welcome to the live stream!</h1>
    <div class="flex-container">
      <iframe
        src="https://cdn.jwplayer.com/players/yPdwJR8o-qHcvMMW9.html"
        width="640"
        height="360"
        frameborder="0"
        scrolling="auto"
        title="WebDemo"
        allowfullscreen
      ></iframe>
    </div>
  </body>
</html>
```
