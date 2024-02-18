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
