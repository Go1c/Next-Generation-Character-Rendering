# Next-Generation-Character-Rendering
My research and attempt for character rendering, including hair、eyes and face in unity URP.(Won't upload any resources, only share shaders and ideas).


![whole3](https://user-images.githubusercontent.com/56297955/182903868-248bd75a-d7c6-42a0-bbcb-e8799643430e.png)


![whole6](https://user-images.githubusercontent.com/56297955/182903927-4787ba16-0b19-40e7-bdbe-70577f260d9d.png)


## Hair

Due to the hair is rendered as transparent material, I use two layer materials, one rendered as opaque object, the other rendered as normal transparent hair.

And in order to solve the transparent sorting problem, I used Weighted Blended OIT method, but I found just ask the artist to merge the hair layers to just one model, can easily solve this question.

Another problem is the opaque layer will cause jaggies, so I use TAA to solve this.

![image](https://user-images.githubusercontent.com/56297955/182907859-33179eab-d932-4e63-9631-d6767e93b2c1.png)
