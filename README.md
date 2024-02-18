 Determine whether it is the ground by calculating the characteristic root and eigenvalue of each point

Calculate the projection of the normal vector of each point on the Z axis 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574671027
  ```  


--------------------------------------------------------------------------------

Recently, I spent a few days doing a small task to extract the power lines from the point cloud mapping data scanned by the drone. The data is as shown in the figure below, with about 8 million points of data 

 ![avatar]( 476f449931d540d8a6b061cfdabfcd68.jpg) 

 The ground vegetation accounts for the majority, and there are also a lot of noise and noise data in the sky 

 ![avatar]( 133a6077c4d149a1b383f6948c030091.jpg) 

 First, roughly filter the ground vegetation according to the height, leaving the sky noise and some ground points, as well as the base station of the wire. 

 ![avatar]( 51e3f9670a5e445f9366d9c7b3998e6a.jpg) 

 picture 

 If you statistically filter the clutter in the sky, you're left with base stations and some ground points. 

 ![avatar]( 3cc2bcc5f6954d62a4eaf0583166dc50.jpg) 

 picture 

 Then do a sample of the remaining points to avoid too many points. The subsequent calculation is too complicated. The result of this step shows that it does not seem to have changed much 

 picture 

 ​ 

 ![avatar]( 668fb72da3374ff69a3d624ffadd4f4f.jpg) 

 Then according to the method of a paper, the killer was used to extract the candidate transmission line points. The result was close to perfect, leaving only a few ground points and a small number of miscellaneous points. Only a little follow-up processing was required 

 picture 

 ![avatar]( 3d08112894b3493691375e3939262df3.jpg) 

 Further extract and segment each power line and label it with different colors, while automatically removing other irrelevant objects according to the characteristics 

 ![avatar]( 385bd96b49b04fa58d718483a315af4d.jpg) 

 picture 

 Perfect! Math is really useful! 



--------------------------------------------------------------------------------

 We tried randomly coloring each point of the point cloud, and the result looked messy, like a pile of garbage...

 ![avatar]( 438806cc8b34450dba849d36cbb0f984.png) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574629478
  ```  


--------------------------------------------------------------------------------

 We use an artifact to scan point cloud data as an example.

Split its ground section, leaving only the scanned point cloud data of the workpiece

 ![avatar]( 4b50cf88b8e84b8480deded84b495843.png) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574681329
  ```  


--------------------------------------------------------------------------------

 The point cloud can be rotated using Euler angles, rotation matrices, or quaternions.

 ![avatar]( bf528cc0782449a4be0765b15d3a372f.png) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574663028
  ```  


--------------------------------------------------------------------------------

 You can calculate the surface area and volume of the closed point cloud surface; in fact, it is quite simple to do 3D reconstruction without closing, and then treat the point cloud as closed to calculate the volume and surface area 

 ![avatar]( 35a375429a4f460095aadb429426d5b0.png) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574687991
  ```  


--------------------------------------------------------------------------------

![avatar]( 6c6e96bd365a4c578a095f523b49a658.png) 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957461375
  ```  


--------------------------------------------------------------------------------

I wanted to do a three-dimensional curve interpolation before, but I couldn't find a good existing implementation, so I wrote one myself 

 The effect is as shown in the picture: 

 ![avatar]( bd2e02dbbb234edbbcb6b521bc6fb086.png) 

 The idea is also very simple, just interpolate XYZ separately  

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574660199
  ```  


--------------------------------------------------------------------------------

Sometimes we don't want to change the coordinates of the original points, but we need to reduce the number of points.

You can use uniform downsampling.

What it does is, it takes one for every N points, and the final number of points becomes 1/N of the original number.

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574683300
  ```  


--------------------------------------------------------------------------------

![avatar]( 5bb35581495d453e97cb86d9ef0d9f1a.png) 

 After sampling, the points will appear to be arranged neatly and evenly, but the positions will shift slightly compared to before.

 Voxel downsampling creates a uniformly downsampled point cloud from the input point cloud using a regular voxel mesh.

It is usually used as a preprocessing step for multipoint cloud processing tasks. The algorithm is divided into two steps:

1. Points are stored in voxels.

2. Each occupied voxel generates a point by averaging the coordinates of all points inside.

Parameter voxel_size is the size of the voxel, the smaller the parameter, the more points the result of downsampling,

The disadvantage of this method is that it will change the coordinates of the original point.

Because the points after downsampling are calculated by averaging. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574632598
  ```  


--------------------------------------------------------------------------------

Voxel meshes are another type of 3D geometry represented by regular 3D meshes.

Generate a voxel mesh from a point cloud using the create_from_point_cloud function.

If at least one point in the point cloud is within the voxel grid, the grid is occupied.

The color represents the average value of the midpoints of that voxel.

Parameter voxel_size used to define the mesh resolution.

也可以使用 create_from_point_cloud_within_bounds(input, voxel_size, min_bound, max_bound)

To impose a range limit on the generated voxel mesh

A voxel grid can also be used to test whether a point is within the occupied grid.

Method check_if_included takes a (n, 3) array as input,

Returns an array of type bool.  

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574674354
  ```  


--------------------------------------------------------------------------------

 Combine multiple PNG images together to create a RAW image

Just set the input and output paths. 

 The code is as follows 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574638798
  ```  


--------------------------------------------------------------------------------

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



--------------------------------------------------------------------------------

WeChat 394467238 

 Sometimes we need to expand the original point cloud data to make it more robust. 

 The idea is very simple, that is, to generate a random normal distribution of noise, and then add it to the original XYZ data of the point cloud; 

 Put the code directly, the code has been run, no problem: 

 The std in the code is the standard deviation of the normal distribution, which is the standard deviation of the distance distribution of the noise data from the original data 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574666299
  ```  
 The last step is to combine the original data with the noisy data into one data. 



--------------------------------------------------------------------------------

 Python code, the pose change between two 4 * 4 rotation matrices, that is, find the relative rotation matrix between two rotation matrices 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574655251
  ```  


--------------------------------------------------------------------------------

In this example, we have two quaternions q1 and q2, representing the initial pose and the final pose, respectively. We first calculate the difference between these two quaternions using the quat_diff function. Then, we use the quat_to_rot function to convert the resulting quaternion difference into a rotation matrix. Finally, we construct the homogeneous transformation matrix T by joining the rotation matrix with the zero translation vector and adding a row [0,0,1] at the bottom. The resulting transformation matrix T can be used to transform a point or vector from the initial pose to the final pose. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957466661
  ```  


--------------------------------------------------------------------------------

The intuitive idea of the ICP algorithm is as follows: 

 The ICP algorithm actually alternates the above two steps and iterates until it converges. 

 The general algorithm flow of ICP is: 

 1. Point cloud preprocessing 

 - Filtering, cleaning data, etc 

 Step 2: Match 

 - Apply the transformation solved in the previous step to find the nearest point 

 3. Weighted 

 - Adjust the weights of some corresponding point pairs 

 4. Eliminate unreasonable corresponding pairs 

 5. Calculation of losses 

 6. Minimize loss and solve the current optimal transformation 

 7. Go back to step 2. Iterate until convergence 

 Overall, the ICP divides the point cloud registration problem into two sub-problems: 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574654120
  ```  


--------------------------------------------------------------------------------

Generated the true value of the slam odometer and the value of the odometer, and saved the vertices and edges as g2o files 

 ![avatar]( 6a327aceae824f4e9fbe66c5079ef8f1.png) 

  Randomly generate slamming true values and odometry g2O text 

 piece 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574619928
  ```  


--------------------------------------------------------------------------------

 Can read 2D and 3D g2o files, and can convert quaternion poses into node and edge data. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574639599
  ```  


--------------------------------------------------------------------------------

Scan Context is literally "scan, context" in English. Analogous to when we read, we need to understand the context in order to understand its meaning. When LidarSLAM performs loop detection, it also needs to compare the "context" (previous data) to know if we have come to the same place before (loop). 

 The main feature of the Scan Context paper, written by Giseop Kim and Ayoung Kim of KAIST University in South Korea, is to propose Scan Context, a global descriptor for non-histograms, to help us search for "context" (current/previous data) more quickly and efficiently. Typical applications are loop detection and Place Recognition in LiDAR SLAM. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 2024020309574658556
  ```  


--------------------------------------------------------------------------------

