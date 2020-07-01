---
title: "Audio Visualization with Web Audio and Canvas"
date:  2016-10-16
---

# Audio Visualization with Web Audio and Canvas

<div class="centered">
  <a href="/audio-visualization">
    <img src="/img/audio-visualization.png"/>
    <div>
      demo
    </div>
  </a>
  <a href="http://github.com/razzius/audio-visualization">source code</a>
</div>

While exploring ways to visualize audio, I found [this blog post](http://jonathanwatmough.com/2008/02/prototyping-code-in-clojure/) and was inspired by the screenshot to create something similar using web technologies. My implementation uses [Web Audio AnalyserNode](https://developer.mozilla.org/en-US/docs/Web/API/AnalyserNode) and borrows most of the Web Audio code from [this demo](https://webaudiodemos.appspot.com/AudioRecorder/).

I developed this in Chrome and didn't attempt to vendor prefix or compile down ES6 features so other browsers aren't expected to work.

### Controls:

- Switch between viewing the audio frequencies and waveform spectrum
- Change the length of history data stored (try lowering this if there is lag)
- Change the hue factor which is multiplied by the magnitude to determine the color
- Change the alpha transparency of the graph

One of my favorite presets is having the hue multiplier set to .3 so the colors range from a rich red to a pastel yellow. With alpha set to 1, It looks like this:

<div class="centered">
  <img width="600" height="400" src="/img/red_spectrum.png"/>
</div>

Eventually I hope to use this as a frontend to display results from an audio recognition engine and better understand audio processing. One drawback of this approach is that it uses [requestAnimationFrame](https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame) and thus has a variable framerate, so the audio data isn't recorded with a consistent sampling rate.

One experiment with this implementation was using only JavaScript and a `root`, in the style of React. I liked this approach for the ease of attaching events and not having to query the DOM, though layouts and styling would be harder to get right without being able to inspect the element hierarchy. The entire source is just under 200 lines, [check it out!](https://github.com/razzius/audio-visualization/blob/master/index.js) You can also edit the source as its running on the devtools "Sources" tab - try changing the `context.fillStyle` template string.
