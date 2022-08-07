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

I just use Kajiya-Kay Shading Model, it already shows a good look.The key to calclate the Kajiya-Kay specular is to replace the normal by tangent, then to calculate specular.

The most important part is about the uv and tangent space, for the hair patch, the tangent(in tangent space) is along with the U direction, so we can shift the specular based on this feature, and do the specular calculation.

For Strand-based anisotropic lighting, hair is a lot of wires, each is rendered as cylinder:

![image](https://user-images.githubusercontent.com/56297955/183281437-5c757ea5-eb74-4aaa-b0d6-4c4c7dd3cbbb.png)

The correct way to calculate specular is the integral of (N · H), but it is too heave. Consider the tangent direction, Tangent、normal、Half Vector can be placed in a plane, and the angle is 90 degrees. 

![image](https://user-images.githubusercontent.com/56297955/183282518-66195017-4575-455b-8254-9c2b650c0395.png)

So we can replace the (N · H) by T and H:

![image](https://user-images.githubusercontent.com/56297955/183282533-2ff88385-e6ce-47b0-a838-164787f6b9a1.png)

Then just use this to calculate specular, we can get the circular specular and change with the view and light direction.


![image](https://user-images.githubusercontent.com/56297955/183285021-4cacdd7b-d744-47dd-b30f-f5868bcf0243.png)


And in real world, the specular should have two layers, one with color and the other has no color, and should be shifted a little to show something like jaggies.


![image](https://user-images.githubusercontent.com/56297955/183284813-9a383d4b-2f3d-4f16-8d18-8222dc9ede5e.png)


The theory behind is shift T by Normal, T + shift * Normal means scale and rotate the T:


![IMG_20220807_181200_edit_433170275539632](https://user-images.githubusercontent.com/56297955/183288388-50dc2bb2-8d49-42c8-a933-2cb88753691f.jpg)


With the projected length changed the specular position also changing.


## Face
To implement pre-integration and Separable Subsurface Scattering algorithm.(pre-integration is done)

### Key:

(SSS + Diffuse) + Dual lobe specular + Transmittance  


## Eyes

The eyes are rendered with a more realistic multi-layered structure


![Screenshot 2022-07-20 220637](https://user-images.githubusercontent.com/56297955/182918311-2cb1cfc4-4e31-4f6a-8129-2857d250d294.png)


To render the eye ball, shold give the possibility to scale the pupil and render the limbus.


![Eye7](https://user-images.githubusercontent.com/56297955/182921125-1d71d5a9-4c70-4170-8a59-2eebb05fb8d5.png)

