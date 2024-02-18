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
