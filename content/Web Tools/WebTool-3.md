---
title: "WebTool: Week3"
draft: false
---
#### Assignment
[Dithering Sketch](https://editor.p5js.org/brain/sketches/hU0ANATF-)
The original code is fairly simple, I left out the other dithering type and only leave bayer because I don't like the way the others look. Things I can let user decide:
- Image (or make it a webcam snapshot?)
- Dithering Color
- Download (Gif'd be cool if I am usin snapshots?)
- Threshold
- pixelDensity
<div align = "center" >
<img src="media/webtool/dither-screenshot.png" width = "400px">
</div>


Define window parameter, and checking console log to see if the tool.js file is successdfully linked to HTML. Then I create sliderto see change the dithering threshold.



<div align= "center">
<img src = "media/webtool/dither-1.png" width = "300px">
<img src = "media/webtool/dither-2.png"width = "300px">
<img src = "media/webtool/dither-3.gif"width = "300px">
</div>

----------------------
Then I figured out the snapshot and making gif function with just p5js. For this step, I was still using p5's createButton function just for testing if I can successfully get the webcam snapshots and make gif out of them.
<div align= "center">
<img src = "media/webtool/dither-4.gif" width = "300px">
</div>
After this, start replace the button with HTML elements.
<div align= "center">
<img src = "media/webtool/dither-5.png" width = "300px">
<img src = "media/webtool/dither-6.png" width = "300px">
<img src = "media/webtool/dither-7.png" width = "300px">
<img src = "media/webtool/dither-8.gif" width = "300px">
</div>






























---------------------------------


**The first thing i tried**
i want to make something like this.
Things for user input:
- blur amount
- how rigid is the cutout
- snapshot photo from webcam
- Text
- Download
- maybe gif?
<div align = "center" >
<img src="media/webtool/facemesh-sample.png" width = "200px">
</div>


I start with looking into ml5's facemesh for figuring out how to cut out the face. 
- figure out pinning oval shape of face

 <div align = "center" >
<img src="media/webtool/facemesh-1.png" width = "200px">
<img src="media/webtool/facemesh-2.png" width = "200px">
</div>
- To cut it out i used drawingContext from p5js that include clipping method(https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial/Compositing)
- https://p5js.org/reference/p5/drawingContext/

 <div align = "center" >
<img src="media/webtool/facemesh-3.png" width = "200px">
<img src="media/webtool/facemesh-4.png" width = "200px">
</div>
I added blur filter and distorted effect after this but It turned out the look is not as good as what was in my head so I didn't proceed with this.
#### Lecture
[Everest Pipkin Tool List](https://github.com/everestpipkin/tools-list)