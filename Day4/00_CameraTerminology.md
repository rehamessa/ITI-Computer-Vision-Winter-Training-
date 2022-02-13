# Basics - Camera Terminology

## Filed of view

- This is the vertical and horizontal `angular` portion of the environment (scene) that is visible to the sensor.
- In self-driving cars, you typically want to balance the FoV with the resolution of the sensor to ensure we see as much of the environment as possible with the least number of cameras.
- There is a trade space related to FoV.
  - Larger FoV usually means more lens distortion, which you will need to compensate for in your camera calibration.
  - Example, wide-angle and fish-eye cameras.

![Field of view](Files/Illustration-of-camera-lenss-field-of-view-FOV.ppm.png)

![Field of view](Files/FOV.jpeg)

---

## Resolution

- This is the total number of pixels in the horizontal and vertical directions on the sensor.
- This parameter is often discussed using the term megapixels (MP).
- For example, a 5 MP camera, such as the FLIR Blackfly, has a sensor with 2448 × 2048 pixels, which equates to 5,013,504 pixels.
- Higher resolutions allow you to use a lens with a wider FoV but still provide the detail needed for running your computer vision algorithms.
- This means you can use fewer cameras to cover the environment and thereby lower the cost.

Cameras in the market

- Blackfly.
- ZED Stereo.

![Resolution](Files/pixels.JPG)

---

## Focal length

- This is the length from the lens optical center to the sensor.
- The focal length is best thought of as the zoom of the camera.
- A longer focal length means you will be zoomed in closer to objects in the environment.
- In your self-driving car, you may choose different focal lengths based on what you need to see in the environment.
- For example, you might choose a relatively long focal length of 100 mm to ensure enough resolution for your classifier algorithm to detect a traffic signal at a distance far enough to allow the car to react with smooth and safe stopping:

![Focal Length](Files/focal.png)

---

## Aperture and f-stop

- This is the opening through which light passes to shine on the sensor.
- The unit that is commonly used to describe the size of the opening is the f-stop, which refers to the ratio of the focal length over the aperture size.
- For example, a lens with a 50 mm focal length and an aperture diameter of 35 mm will equate to an f-stop of f/1.4.
- The following figure illustrates different aperture diameters and their f-stop values on a 50 mm focal length lens.
- Aperture size is very important in your self-driving car as it is directly correlated with the Depth of Field (DoF).
- Large apertures also allow the camera to be tolerant of obscurants (for example, bugs) that may be on the lens.
- Larger apertures allow light to pass around the bug and still make it to the sensor:

![Aperture](Files/apertures.jpg)

---

## Depth of field (DoF)

- This is the distance range in the environment that will be in focus.
- This is directly correlated to the size of the aperture.
- Generally, in self-driving cars, you will want a deep DoF so that everything in the FoV is in focus for your computer vision algorithms.
- The problem is that deep DoF is achieved with a small aperture, which means less light impacting the sensor.
- So, you will need to balance DoF with dynamic range and ISO to ensure you see everything you need to in your environment.
- The following figure depicts the relationship between DoF and aperture:

![Depth of view](Files/DOF.png)

---

## Dynamic Range

- This is a property of the sensor that indicates its contrast ratio or the ratio of the brightest over the darkest subjects that it can resolve.
- This may be referred to using the unit dB (for example, 78 dB) or contrast ratio (for example, 2,000,000/1).
- Self-driving cars need to operate both during the day and at night.
- This means that the sensor needs to be sensitive enough to provide useful detail in dark conditions while not oversaturating when driving in bright sunlight. 
- Another reason for High Dynamic Range (HDR) is the example of driving when the sun is low on the horizon.
- I am sure you have experienced this while driving yourself to work in the morning and the sun is right in your face and you can barely see the environment in front of you because it is saturating your eyes.
- HDR means that the sensor will be able to see the environment even in the face of direct sunlight. The following figure illustrates these conditions:

![HDR Video](Files/HDR.png)

---

## International Organization for Standardization (ISO) sensitivity

- This is the sensitivity of the pixels to incoming photons.
- Wait a minute, you say, do you have your acronym mixed up? It looks like it, but the International Organization for Standardization decided to standardize even their acronym since it would be different in every language otherwise.
- Thanks, ISO! The standardized ISO values can range from 100 to upward of 10,000. Lower ISO values correspond to a lower sensitivity of the sensor.
- Now you may ask, "why wouldn't I want the highest sensitivity?" Well, sensitivity comes at a cost...NOISE.
- The higher the ISO, the more noise you will see in your images.
- This added noise may cause trouble for your computer vision algorithms when trying to classify objects.
- In the following figure, you can see the effect of higher ISO values on noise in an image.
- These images are all taken with the lens cap on (fully dark).
- As you increase the ISO value, random noise starts to creep in:

![ISO](Files/ISO.png)

### Let's Try it out, pickup your mobile phone

---

## Frame rate (FPS)

- This is the rate at which the sensor can obtain consecutive images, usually expressed in Hz or Frames Per Second (FPS).
- Generally speaking, you want to have the fastest frame rate so that fast-moving objects are not blurry in your scene.
- The main trade-off here is latency: the time from a real event happening until your computer vision algorithm detects it.
- The higher the frame rate that must be processed, the higher the latency.
- In the following figure, you can see the effect of frame rate on motion blur.
- Blur is not the only reason for choosing a higher frame rate.
- Depending on the speed of your vehicle, you will need a frame rate that will allow the vehicle to react if an object suddenly appears in its FoV.
- If your frame rate is too slow, by the time the vehicle sees something, it may be too late to react:

![Animation](Files/fps1.gif)
![FPS Diff](Files/fps2.jpg)

---

## Lens flare

- These are the artifacts of light from an object that impact pixels on the sensor that do not correlate with the position of the object in the environment.
- You have likely experienced this driving at night when you see oncoming headlights.
- That starry effect is due to light scattered in the lens of your eye (or camera), due to imperfections, leading some of the photons to impact "pixels" that do not correlate with where the photons came from – that is, the headlights.
- The following figure shows what that effect looks like.
- You can see that the starburst makes it very difficult to see the actual object, the car!

![Lens Flare](Files/flare.jpg)

---

## Lens distortion

- This is the difference between the rectilinear or real scene to what your camera image sees.
- If you have ever seen action camera footage, you probably recognized the "fish-eye" lens effect.
- The following figure shows an extreme example of the distortion from a wide-angle lens. You will learn to correct this distortion with OpenCV:

![Distortion](Files/distortion.jpg)

---

## Flow (From Photons to Bits)

In this image we follow the light in its jurney from photons to bits in the camera's storage.

Following image shows image sensing pipline

![Image](Files/CamFlow.png)
