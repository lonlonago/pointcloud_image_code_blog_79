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
