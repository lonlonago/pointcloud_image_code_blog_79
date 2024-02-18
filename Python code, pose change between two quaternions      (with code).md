In this example, we have two quaternions q1 and q2, representing the initial pose and the final pose, respectively. We first calculate the difference between these two quaternions using the quat_diff function. Then, we use the quat_to_rot function to convert the resulting quaternion difference into a rotation matrix. Finally, we construct the homogeneous transformation matrix T by joining the rotation matrix with the zero translation vector and adding a row [0,0,1] at the bottom. The resulting transformation matrix T can be used to transform a point or vector from the initial pose to the final pose. 

  ```python  
After clicking on the GitHub Sponsor button above, you will obtain access permissions to my private code repository ( https://github.com/slowlon/my_code_bar ) to view this blog code. By searching the code number of this blog, you can find the code you need, code number is: 202402030957466661
  ```  
