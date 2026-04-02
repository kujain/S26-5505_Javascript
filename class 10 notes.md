#### SESSION #10

# WEB APIs

- Built-in JavaScript tools that let you interact with browser features and user devices
- Extends the functionality of the browser
- Simplifies complex and often used functions
- No installation needed — they're already there in every modern browser
- Provides easy syntax to complex features
- Typically used by Javascript but it can be html only
- Permission-based — some APIs (location, notifications) require user consent
- The window object — most Browser APIs hang off this global object
eg.
```
console.log(window.localStorage);
console.log(window.navigator);
```

## DOM API 

- The DOM API is the most fundamental Browser API
- It's how JavaScript "talks to" the HTML page
- Everything you have done with `document.querySelector()` is the DOM API

```
// Selecting elements
document.getElementById('myId');
document.querySelector('.myClass');
document.querySelectorAll('p');

const newDiv = document.createElement('div');
newDiv.textContent = 'I am new!';
document.body.appendChild(newDiv);
```

## HTML5 GEOLOCATION 

- Navigator contains current position information for the client and can be accessed through: navigator.geolocation
- Gets the user's physical location (latitude/longitude)
- Requires permission — browser will prompt user
- Uses GPS on phones, IP/WiFi estimation on desktops
- Privacy-sensitive 

Returns a Geolocation object:
```
function youAreHere(position) {
  console.log("position: ", position);
}

// Check if available
if(navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(youAreHere);
}
```

Watch for changes:
```
function youHaveMoved(position) {
  console.log("changed position: ", position);
}

// Check if available
if(navigator.geolocation) {
  navigator.geolocation.watchPosition(youHaveMoved);
}
```

Reference: https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API


## HTML5 Clipboard API 

- Read from and write to the system clipboard
- Common use: "Copy to clipboard" buttons
- Modern API uses Promises (async)
- Requires user interaction — can't copy silently in background
- Reading clipboard requires permission; writing usually doesn't

```
// Copy text to clipboard
async function copyToClipboard(text) {
  try {
    await navigator.clipboard.writeText(text);
    console.log('Copied!');
  } catch (err) {
    console.error('Failed to copy:', err);
  }
}

// Read from clipboard (needs permission)
async function pasteFromClipboard() {
  try {
    const text = await navigator.clipboard.readText();
    console.log('Pasted:', text);
    return text;
  } catch (err) {
    console.error('Failed to read clipboard:', err);
  }
}
```

## Notifications API

- Send system notifications (appear outside browser)
- Requires explicit permission — user must click "Allow"
- Works even when tab is in background
- Don't abuse it — users could block your site
- Must check permission state before sending

```
console.log(Notification.permission);  // 'default', 'granted', or 'denied'

// Request permission
async function requestNotificationPermission() {
  const permission = await Notification.requestPermission();
  if (permission === 'granted') {
    console.log('Permission granted!');
  } else {
    console.log('Permission denied');
  }
}

// Send a notification
function sendNotification(title, body) {
  if (Notification.permission === 'granted') {
    const notification = new Notification(title, {
      body: body,
      icon: '/icon.png'  // optional
    });
    // Handle click
    notification.onclick = function() {
      window.focus();
      notification.close();
    };
  }
}
```


## HTML5 DATA ATTRIBUTES 

- Allows for a more structured method for passing configs and attributes from html to javascript.
- Used by all javascript/jQuery plugins to define settings for the plugin.

```
<div id="slideshow" data-type="carousel" data-transition="fade-in" data-auto-start="true">
  <div>Slide 1</div>
  <div>Slide 2</div>
</div>
```
```
const slide = document.getElementById("slideshow");
const type = slide.dataset.type;
const transition = slide.dataset.transition;
const auto_start = slide.dataset.autoStart;

// alternative generic way to get attributes:
const type = slide.getAttribute("data-type");
slide.setAttribute('data-type', 'slider' );
```




## HTML5 VIDEO/AUDIO

A clean and extensible approach to embedding media objects.

Pre-html5: 
```
<div>
    <object classid="clsid:02bf25d5-8c17-4b23-bc80-d3488abddc6b" codebase="http://www.apple.com/qtactivex/qtplugin.cab">
      <param name="src"  value="movie.mp4" />
      <param name="autoplay"  value="false" />
      <param name="controller"  value="true" />

      <!--[if !ie] -->
      <object type="video/mp4"  data="movie.mp4">
        <param name="controller"  value="true" />
        <param name="autoplay"  value="false" />
      </object>
      <!--[endif]-->
    </object>
</div>
```

NOW: 
```
<audio src="assets/08_please.mp3" controls>
  Your browser does not support the audio element.
</audio>

<video src="assets/Nearness_on_Vimeo.mp4">
  Your browser does not support the video element.
</video>
```

## HTML5 VIDEO/AUDIO ATTRIBUTES

### Media attributes:
```
<video src="assets/Nearness_on_Vimeo.mp4" autoplay>
  Your browser does not support the video element.
</video>


<video src="assets/Nearness_on_Vimeo.mp4" controls>
  Your browser does not support the video element.
</video>

<video src="assets/Nearness_on_Vimeo.mp4" loop>
  Your browser does not support the video element.
</video>

<video src="assets/Nearness_on_Vimeo.mp4" poster="assets/casa2_hero_1452814189.jpg">
  Your browser does not support the video element.
</video>

<video src="assets/Nearness_on_Vimeo.mp4" preload="none">
  Your browser does not support the video element.
</video>
```

## HTML5 VIDEO/AUDIO CONTROL

Controlling media with Javascript: 
```
const video = document.getElementsByTagName("video")[0];

video.play();
video.pause();
video.volume = 90;
video.muted  = true;
video.loop   = true;
```

Events: 
```
video.addEventListener("pause", function(event) {
  	console.log("video has been paused"); 
})

video.addEventListener("play", function(event) {
  	console.log("video has been paused"); 
})

video.addEventListener("volumechange", function(event) {
  	console.log("video volume has been changed"); 
})

video.addEventListener("timeupdate", function(event) {
  	console.log("video timecode has changed"); 
})

```

### Custom player: 
```
const btn = document.getElementById('play-pause-button');

const mediaPlayer = document.getElementsByTagName("video")[0];

mediaPlayer.controls = false;
btn.addEventListener('click', togglePlayPause.bind(btn));


//play pause toggle
function togglePlayPause() {
   //var btn = document.getElementById('play-pause-button');
   if (mediaPlayer.paused || mediaPlayer.ended) {
	  changeButtonType(btn, 'pause');
      mediaPlayer.play();
   }
   else {
	  changeButtonType(btn, 'play');
      mediaPlayer.pause();
   }
}

// a generic function to handle button states
function changeButtonType(btn, value) {
   btn.title = value;
   btn.innerHTML = value;
   btn.className = value;
}

//stop
let btn1 = document.getElementById('stop-button');
btn1.addEventListener('click', stopPlayer);

function stopPlayer() {
   mediaPlayer.pause();
   mediaPlayer.currentTime = 0;
}

//mute
let btn2 = document.getElementById('mute-button');
btn2.addEventListener('click', toggleMute);

function toggleMute() {
   if (mediaPlayer.muted) {
      changeButtonType(btn2, 'mute');
      mediaPlayer.muted = false;
   }
   else {
      changeButtonType(btn2, 'unmute');
      mediaPlayer.muted = true;
   }
}

//reset
let btn3 = document.getElementById(reset-button');
btn3.addEventListener('click', resetPlayer);

function resetPlayer() {
   mediaPlayer.currentTime = 0;
   changeButtonType(btn, 'play');
}

// show progress bar
mediaPlayer.addEventListener('timeupdate', updateProgressBar, false);
function updateProgressBar() {
   const progressBar = document.getElementById('progress-bar');
   const percentage = Math.floor((100 / mediaPlayer.duration) *
   mediaPlayer.currentTime);
   progressBar.value = percentage;
   progressBar.innerHTML = percentage + '% played';
}
```


## HTML5 CAMERA API

Navigator provides the getUserMedia Promise object to access the device's camera: 
```
// access the camera for video
navigator.mediaDevices.getUserMedia({
  video: true
})
```

```
// example
const constraints = { video: { facingMode: "user" }, audio: false };

navigator.mediaDevices
    .getUserMedia(constraints)
    .then(function(stream) {
        track = stream.getTracks()[0];
        cam_pic.srcObject = stream;
  })
  .catch(function(error) {
      console.error("Oops. Something is broken.", error);
  });
```

## HTML5 CANVAS

Canvas allows graphics to be drawn onto a web page in real time through JavaScript.
```
<canvas id="canvasDrawing1" width="200" height="100">
This browser doesn't support the canvas element.
</canvas>

const canvas = document.getElementById("canvasDrawing1");
```

### Context:

An object containing all the methods used to draw onto and manipulate the canvas. 
```
// 2D
let context = canvas.getContext("2d");

// 3D
let context3D = canvas.getContext("webgl");
```

## HTML5 CANVAS - ADDING SHAPES

Create Shapes
```
// set defaults
context.fillStyle = "#0000cc"; // a blue fill color
context.strokeStyle = "#ccc"; // a gray stroke color
context.lineWidth = 4;

// draw
context.fillRect(10,10,100,50);

// draw
context.strokeRect(10,100,100,50);


// Lines
context.beginPath();
context.moveTo(20, 50);
context.lineTo(180, 50);
context.moveTo(20, 50);
context.lineTo(20, 90);
context.strokeStyle = "#c00";
context.lineWidth = 10;
context.stroke();

// ARCs
context.beginPath();
context.arc(200, 200, 30, 0, Math.PI * 2, false);
context.strokeStyle = "#ff0";
context.lineWidth = 4;
context.stroke();

// text
context.fillStyle = "#cc0033"; // fill color
context.font = "bold 26px sans-serif";
context.fillText("Hello", 20, 200);

// fill
context.fillStyle = "#443";
context.beginPath();
for (let y = 10; y < 200; y+= 10) {
  console.log(y);
  context.moveTo(10,y);
  context.lineTo(200,y);
  context.lineTo(200,y+(0.05*y));
}
context.fill();

// Image
let img = document.createElement('img');
img.src = 'assets/no_image.gif';
img.addEventListener('load', function() {
	context.drawImage(img, 10, 10 );
});

//Transform
context.scale(1,2) // works on anything drawn after
context.rotate(0.1*Math.PI)
context.translate(50,100)
```

## HTML5 CANVAS - EXAMPLE

```
// draw random circles
for (let y = 0; y < 200; y++) {
  let cx = Math.random()*600;
  let cy = Math.random()*400;
  let cw = Math.random()*15;
  let cc = 'rgba('+ Math.floor(Math.random()*25)*10 + ', ' + Math.floor(Math.random()*25)*10 + ', ' + Math.floor(Math.random()*15)*10 + ')';
  // alpha:
  //let cc = 'rgba('+ Math.floor(Math.random()*25)*10 + ', ' + Math.floor(Math.random()*25)*10 + ', ' + Math.floor(Math.random()*15)*10 + ', ' + Math.random() + ')';

  console.log(y,cx,cy,cw,cc);

  context.fillStyle = cc;
  context.moveTo(cx,cy);
  context.beginPath();

  context.arc(cx, cy, cw, 0, Math.PI * 2, false);
  context.fill();
  context.lineWidth = 1;
  context.stroke();
}
```

```
//with interval
let count = 0;
function init() {
  let timer = setInterval(draw, 10);
  return timer;
}
function draw() {
  let cx = Math.random()*600;
  let cy = Math.random()*400;
  let cw = Math.random()*15;
  let cc = 'rgb('+ Math.floor(Math.random()*25)*10 + ', ' + Math.floor(Math.random()*25)*10 + ', ' + Math.floor(Math.random()*15)*10 + ')';
  console.log(cx,cy,cw,cc);
  context.fillStyle = cc;
  context.moveTo(cx,cy);
  context.beginPath();
  context.arc(cx, cy, cw, 0, Math.PI * 2, false);
  context.fill();
  count++;
  console.log(count);
  if (count > 200) {
    clearInterval( timer );
  }
}
init();
```

## MORE HTML5 APIs

- Prefetch API
- Speech Synthesis API
- Geolocation API
- Fullscreen API
- Web Storage API
- Battery API
- Clipboard API
- etc...

An exhaustive list: https://developer.mozilla.org/en-US/docs/Web/API


## In-class Assignment
Assignment - make a pie or bar chart

```
const data = [
  {name: "Name 1", count: 1045, color: "blue"},
  {name: "Name 2", count: 563, color: "red"},
  {name: "Name 3", count: 231, color: "silver"},
  {name: "Name 4", count: 423, color: "pink"}
];
```

