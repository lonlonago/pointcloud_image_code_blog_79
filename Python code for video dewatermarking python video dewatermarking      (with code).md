 Recently, there is a video that wants to remove the watermark. I searched for products on the market. After using it, I found that the effect is very long... Most of them are direct Gaussian blurring. 

 In addition, it can only handle the watermark of the rectangular frame, which cannot be handled for the watermark that covers the entire video obliquely like mine; 

 So I want to try using the code to watermark myself to see if it can be better. 

 ![avatar]( 043781aa05ad08547195d79076e260cb.png) 

 The process is as follows: 

 1 First transfer the picture to the HSV color space, and manually extract the HSV value range of the watermark; 

 2. Extract multiple watermark templates and synthesize a better watermark mask; 

 3. There are two ways to process the watermark of each frame of the video, one is the inpaint that comes with opencv, and the other is the value of the random replacement watermark I wrote myself as the value of the nearby point. Compared with my method, the effect is better; 

 The following is extracted from multiple masks: 

 ![avatar]( 072ceb416f627fce373e511382967390.png) 

 Synthetic mask, the effect is very good: 

 ![avatar]( e196d1089b762cc23c95d99e5e68f4e6.png) 

 Of course, you can also manually select a single mask with better effect: 

 ![avatar]( 5cf9a2204ec674114fad5a94107b2d3c.png) 

 The final effect comparison: 

 OpenCV inpaint method 

 ![avatar]( c33284c2ef2c26543c52663fab95d5c3.png) 

 My approach to self-awareness works slightly better. 

 ![avatar]( fd6a214a298e2f4828f2152e38e36bae.png) 

 The code is as follows: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574628267
  ```  
 If you want to handle images, just tweak the code a bit. 

 However, the shortcomings of this code are also obvious, that is, it is very slow... Hahaha 

