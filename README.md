# Next-Generation-Character-Rendering
My research and attempt for character rendering, including hair、eyes and face in unity URP.(Won't upload any resources, only share shaders and ideas).


![whole3](https://user-images.githubusercontent.com/56297955/182903868-248bd75a-d7c6-42a0-bbcb-e8799643430e.png)


![whole6](https://user-images.githubusercontent.com/56297955/182903927-4787ba16-0b19-40e7-bdbe-70577f260d9d.png)


## Hair

Due to the hair is rendered as transparent material, I use two layer materials, one rendered as opaque object, the other rendered as normal transparent hair.

And in order to solve the transparent sorting problem, I used Weighted Blended OIT method, but I found just ask the artist to merge the hair layers to just one model, can easily solve this question.

Another problem is the opaque layer will cause jaggies, so I use TAA to solve this.

![image](https://user-images.githubusercontent.com/56297955/182907859-33179eab-d932-4e63-9631-d6767e93b2c1.png)


#### Detail

I just use Kajiya-Kay Shading Model, it already shows a good look.The key to calclate the Kajiya-Kay specula


## Face
To implement pre-integration and Separable Subsurface Scattering algorithm.(pre-integration is done)

### Key:

(SSS + Diffuse) + Dual lobe specular + Transmittance  


## Eyes

The eyes are rendered with a more realistic multi-layered structure


![Screenshot 2022-07-20 220637](https://user-images.githubusercontent.com/56297955/182918311-2cb1cfc4-4e31-4f6a-8129-2857d250d294.png)


To render the eye ball, shold give the possibility to scale the pupil and render the limbus.


![Eye7](https://user-images.githubusercontent.com/56297955/182921125-1d71d5a9-4c70-4170-8a59-2eebb05fb8d5.png)

