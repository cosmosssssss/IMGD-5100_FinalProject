# Description
This is an AR project made by AFrame. It includes marker detection technique, some details of adding animation and the particle effect.
# Motivation
AFrame is a Web-based AR engine which can use to build lots of amazing AR projects. (You can find some examples in Youtube). I am very interested in augmented reality so I try to build my own AR project by AFrame.
# Impletation Description
I will explain in detail how I implemented this project in the following order:
## 1. Uploading files and using them
![image](https://user-images.githubusercontent.com/57471535/118145819-9673a500-b440-11eb-9817-a7740a283fd6.png)  
**Step 1:** Upload your file. (Recommend a glb file, because you can directly use it without transferring its format.)  
![image](https://user-images.githubusercontent.com/57471535/118145167-e69e3780-b43f-11eb-914d-9d7e901ec98d.png)  
**Step 2:** Copy the link of the file.  
```
        <a-asset-item
          id="model"
          response-type="arraybuffer"
          src="https://cdn.glitch.com/9bf0117b-f72a-40d4-b940-fd3d02f03720%2FExquisite%20Kasi.glb?v=1619428634434"
        >
        </a-asset-item>
```
**Step 3:** Maker the file with a specific id and don't forget to paste the link as the source.  
```
       <a-entity
          animation="property: rotation; to: 270 -90 90; loop: true; dur: 10000"
          gltf-model="#model"
          position="0 0 1"
          scale="0.02 0.02 0.02"
          rotation="-90 -90 90"
        >
        </a-entity>
```
**Step 4:** Using it by calling its id.  
## 2. Adding animation
AFrame supports many complex animation, like changing position, changing rotation, changing color and so on. However, some of them are easy to implement, some of them need to pay attention to some details.  
For example, changing objects' opacity:
```
        <a-cylinder
          position="1 0.75 1"
          radius="0.3"
          height="1"
          color="#FFC65D"
          material="opacity:0"
          rotation="90 -90 90"
          animation="property: height; to: 0; dur:900; loop: true"
          animation__fadein="property: material.opacity; dur: 10000; easing: linear; from: 0; to: 1;"
        >
        </a-cylinder>
```
You need to tell the system the opacity will change **from: xx**. (If the animation does not appear, please refresh the page and try again.)
## 3. Marker detection
Marker detection is a very useful technique in AFrame. With this script, all things will only show up when the marker is detected. It is widely used in playing BGM or a video. In my project, I use it to play a video.
```
         <script>
          AFRAME.registerComponent("vidhandler", {
            // ...
            init: function() {
              // Set up initial state and variables.
              this.toggle = false;
              this.vid = document.querySelector("#vid");
              this.vid.pause();
            },
            tick: function() {
              if (this.el.object3D.visible == true) {
                if (!this.toggle) {
                  this.toggle = true;
                  this.vid.play();
                }
              } else {
                this.toggle = false;
                this.vid.pause();
              }
            }
          });
        </script>
```
## 4. Particle effect
There are many script on the Internet saying that they include particle effects, but this is the most comprehensive one I have found.
```
    <script src="https://unpkg.com/aframe-particle-system-component@1.0.x/dist/aframe-particle-system-component.min.js"></script>
```
Then you can implement a snow effect or a default effect with some animation.
```
       <a-entity
          position="0 -7 -15"
          particle-system="preset:snow;accelerationValue:0,-10,0;color:#f9e154;particleCount:1000;direction:1;rotationAxis:z;rotation:-90 0 0"
        ></a-entity>
        <a-entity
          position="0 0 0"
          particle-system="
                present:default;
                color: #FF0000, #FFFF00; 
                size: 1, 0;
                velocityValue: 0.001 0.001 0.001;
                velocitySpread: 0.5 0 0.5; 
                accelerationValue: 0.001 0.001 0.001;
                accelerationSpread: 0.001 0.001 0.001;
                rotationAngle: 0; 
                blending: 1;
                particleCount: 200;
                maxAge: 5;
                rotation:-90 -90 90;"
        >
        </a-entity>
```
## 5. Different between a-maker and a-marker-camera
Using a-marker, all staffs will disappear if the marker disappear or cannot be detected clearly. But using a-marker-camera, all things will stay on the screen as long as the marker was detected once which means it is more "stable" than using a-marker.  But when using a-marker-camera, I cannot play a video or a music. And this will be my future work：Playing video when using a-marker-camera.
# Evaluation
By opening the link I send and then scanning the "Hiro" marker, people could see my AR project with their phone or computer. After the first show, I changed playing background music to playing video. It turns out people prefer video playback, which seems more intuitive. And for more fun, I tried to add more animation and explore the particle effects. 
# Project Link
https://colossal-profuse-behavior.glitch.me  
Try my project by showing a "Hiro" marker in front of the camera.
