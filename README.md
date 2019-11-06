# react-media-recorder :o2: :video_camera: :microphone:

`react-media-recorder` is a react component with render prop that can be used to record audio/video streams using [MediaRecorder](https://developer.mozilla.org/en-US/docs/Web/API/MediaRecorder) API.

## Installation

```
npm i -S @getapper/react-media-recorder  
```

or

```
yarn add @getapper/react-media-recorder  
```

## Usage

```javascript
import ReactMediaRecorder from "@getapper/react-media-recorder";

const RecordView = () => (
  <div>
    <ReactMediaRecorder
      video
      render={({ status, startRecording, stopRecording, mediaBlob, mediaUrl }) => (
        <div>
          <p>{status}</p>
          <button onClick={startRecording}>Start Recording</button>
          <button onClick={stopRecording}>Stop Recording</button>
          <video src={mediaUrl} controls />
        </div>
      )}
    />
  </div>
);
```

Since `react-media-recording` uses render prop, you can define what to render in the view. Just don't forget to wire the `startRecording`, `stopRecording` and `mediaUrl` to your component.

### Props available in the `render` function

#### status

A string `enum`. Possible values:

* `idle`
* `recording`
* `paused`
* `stopped`
* `no_constraints`
* `invalid_media_constraints`
* `no_specified_media_found`
* `media_in_use`
* `media_aborted`
* `permission_denied`
* `delayed_start` (_only if a `delay` has been set_) [_deprecating soon_]

If the audio is muted, you'll see the status suffixed with `_muted`.

#### startRecording

A `function`, which starts recording when invoked.

#### pauseRecording

A `function`, which pauses the recording when invoked.

#### resumeRecording

A `function`, which resumes the recording when invoked.

#### stopRecording

A `function`, which stops recording when invoked.

#### muteAudio

A `function`, which mutes the audio tracks when invoked.

#### unmuteAudio

A `function` which unmutes the audio tracks when invoked.

#### mediaBlob

A `blob` object that can be converted in a buffer and uploaded to a server.

#### mediaUrl

A `blob` url that can be wired to an `<audio />`, `<video />` or an `<a />` element.

### Options / Props

#### audio

Can be either a boolean value or a [MediaTrackConstraints](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackConstraints) object.

type: `boolean` or `object`  
default: `true`

#### blobPropertyBag

[From MDN](https://developer.mozilla.org/en-US/docs/Web/API/Blob/Blob):  
An optional `BlobPropertyBag` dictionary which may specify the following two attributes (for the `mediaBlob`):

* `type`, that represents the MIME type of the content of the array that will be put in the blob.
* `endings`, with a default value of "transparent", that specifies how strings containing the line ending character \n are to be written out. It is one of the two values: "native", meaning that line ending characters are changed to match host OS filesystem convention, or "transparent", meaning that endings are stored in the blob without change

type: `object`  
default:  
if `video` is enabled,

```
{
   type: "video/mp4"
}
```

if there's only `audio` is enabled,

```
{
  type: "audio/wav"
}
```

#### delay [_deprecating soon_]

If you want to start recording after a delay. In milliseconds.

type: `number`  
default: `0`

#### muted [_deprcating soon_]

Whether you want to mute the audio (while recording video)

type: `boolean`  
default: `false`

#### render

A `function` which accepts an object containing fields: `status`, `startRecording`, `stopRecording`, `mediaUrl` and `mediaBlob`. This function would return a react element/component.

type: `function`  
default: `() => null`

#### video

Can be either a boolean value or a [MediaTrackConstraints](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackConstraints) object.

type: `boolean` or `object`  
default: `false`

#### whenStopped(blobUrl)

Will be invoked when the recording stops. This callback will be invoked with the blobUrl as its params.

type: `function`  
default: `() => null`

## Contributing

Feel free to submit a PR if you found a bug (I might've missed many! :grinning:) or if you want to enhance it further.

Thanks!. Happy Recording!
