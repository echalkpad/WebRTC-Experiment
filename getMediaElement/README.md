#### getMediaElement.js: A reusable library for all WebRTC applications! / [Demo](https://www.webrtc-experiment.com/getMediaElement/)

```html
<script src="//www.webrtc-experiment.com/getMediaElement.js"></script>
```

This library generates HTMLVideoElement with rich user-interface and advance media controls. It gives you full control over each control button; and its functionality!

<a href="https://www.webrtc-experiment.com/getMediaElement/">
	<img src="https://www.webrtc-experiment.com/images/getMediaElement.js.gif" />
</a>

```javascript
document.body.appendChild( getMediaElement(HTMLVideoElement) );
```

For audio-only element:

```javascript
document.body.appendChild( getMediaElement(HTMLAudioElement) );

// or simply by using "getAudioElement" instead:
document.body.appendChild( getAudioElement(HTMLAudioElement, {
    title: 'User Name',
    buttons: []        // use this line only if you want to hide audio-recorder button
}) );
```

=

##### A working example:

Audio+Video Stream:

```javascript
navigator.webkitGetUserMedia({audio:true, video: true}, function(audioVideoStream) {
     document.body.appendChild( getMediaElement(audioVideoStream) );
});
```

Audio only stream:

```javascript
navigator.webkitGetUserMedia({audio:true}, function(audioStream) {
     document.body.appendChild( getMediaElement(audioStream) );
});

// or simply by using "getAudioElement" instead:
navigator.webkitGetUserMedia({audio:true}, function(audioStream) {
     document.body.appendChild( getAudioElement(audioStream) );
});
```

=

##### Features

1. You can capture `onMuted` event; and disable audio/video tracks accordingly!
2. You can capture `onUnMuted` event; and enable audio/video tracks accordingly!
3. You can capture `onRecordingStarted` and use RecordRTC to record audio/video streams.
4. You can capture `onRecordingStopped` and invoke `stopRecording` method of RecordRTC to stop audio/video recording. You can write recorded audio/video blobs to indexed-db using RecordRTC's newly introduced `writeToDisk` and `getFromDisk` methods.
5. You can capture `onZoomin` to understand that video is NOW in full-screen mode.
6. You can capture `onZoomout` to understand that video is NOW in normal mode.
7. You can disable tool-tips using `enableTooltip:false`.
8. You can prefer dispalying media-control buttons all the time by setting `showOnMouseEnter:true`.
9. You can control `buttons` array to control which button should be displayed on media element.
10. You can use `toggle` method to change buttons' state at runtime!

=

##### Structure of getMediaElement.js

```javascript
var mediaElement = getMediaElement(HTMLVideoElement, {
    buttons: ['mute-audio', 'mute-video', 'record-audio', 'record-video', 'full-screen', 'volume-slider', 'stop'],
    onMuted: function (type) { },
    onUnMuted: function (type) { },
    onRecordingStarted: function (type) { },
    onRecordingStopped: function (type) { },
    onZoomin: function () { },
    onZoomout: function () { },
    onStopped: function () { },
    width: 'media-element-width',
    height: 'media-element-height',
    enableTooltip: true,
    showOnMouseEnter: true
});
```

=

#### getMediaElement objects takes two arguments:

1. HTMLVideoElement or HTMLAudioElement
2. Options

Second argument accepts following objects and events:

1. `buttons`; which is an array, allows you control media buttons to be displayed.
2. `width`; you can customize width of the media-container element by passing this object. Its default value is about "36%-of-screen".
3. `height`; you can customize height of the media-container element by passing this object. Its default value is "auto".
4. `onMuted`; which is fired if audio or video stream is muted. Remember, getMediaElement.js just mutes audio/video locally; you need to send websocket messages in `onMuted` event to remote party.
5. `onUnMuted`; which is reverse of `onMuted`.
6. `onRecordingStarted`; you can implement audio-recording options using RecordRTC!
7. `onRecordingStopped`; RecordRTC supports `stopRecording` method as well!
8. `onZoomin`; it is fired when media element is in full-screen mode.
9. `onZoomout`; it is fired when user leaves full-screen mode either by presssing `ESC` key; or by clicking a button.
10. `enableTooltip`; by default, it is "true".
11. `showOnMouseEnter`; by default, it is "true".

=

#### Possible options for `buttons` object

1. `mute-audio`
2. `mute-video`
3. `record-audio`
4. `record-video`
5. `full-screen`
6. `volume-slider`
7. `stop`

=

#### getMediaElement(firstArgument, secondArgument).toggle(options)

Using "toggle" method; you can customize media control buttons' state; e.g. Mute/UnMute or Zoom-in/Zoom-out etc.

```javascript
var mediaElement = getMediaElement(HTMLVideoElement);

// anytime, later
mediaElement.toggle(['mute-audio']);
mediaElement.toggle(['mute-audio', 'mute-video']);
```

"toggle" method accepts following values:

1. `mute-audio`
2. `mute-video`
3. `record-audio`
4. `record-video`
5. `stop`

"stop" be used to auto-remove media element:

```javascript
mediaElement.toggle(['stop']);

// or simply; as a string argument, instead of an array
mediaElement.toggle('stop');
```

=

##### License

[getMediaElement](https://github.com/muaz-khan/WebRTC-Experiment/tree/master/getMediaElement) is released under [MIT licence](https://www.webrtc-experiment.com/licence/) . Copyright (c) 2013 [Muaz Khan](https://plus.google.com/100325991024054712503).
