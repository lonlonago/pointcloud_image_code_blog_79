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

