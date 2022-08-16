# skeleton_read-Display
**Reading NTU Skeleton data and 2d display**
The code here is borrowed from [How to realize NTU-RGB D skeleton visualization gracefully with Matplotlib](https://programmer.ink/think/how-to-realize-ntu-rgb-d-skeleton-visualization-gracefully-with-matplotlib.html?utm_source=pocket_mylist)

---------------------------------------------------------------------------------------------------------------------

Skeleton data from NTU was extracted by Microsoft Kinect v2, and it has 23 nodes. Before getting further, it is good to know connectivity between nodes

**How the nodes are connected**

![skel](https://user-images.githubusercontent.com/48506842/184852712-bcca53e9-b7b6-462d-83be-06228c63969d.png)

---------------------------------------------------------------------------------------------------------------------

## Code Implementation

This code is as follows

    1. Import Data Files
    
    2. Create a list with filled with 0 to later store the skeleton data
    
    3. Using for-sentence, Loop every frame, skeleton, and , joint to assign data to the array created beforehand
    
    4. Draw Skeleton Nodes with Scatter Diagram and Bone Connections with Line
    
    5. Frame by Frame Display
    
    
 
 First, import packages and data
 
    import numpy as np
    import matplotlib.pyplot as plt
    
    file_name=r'file_path/S***C***P***R***A***.skeleton'
    max_V=25 #number of Vertices
    max_M=2 #Number of Skeletons
 ---------------------------------------------------------------------------------------------------------------------
  
 Then Loop through to obtain the joint point coordinate information
 
    with open(file_name, 'r') as fr:
        frame_num = int(fr.readline())
        point = np.zeros((3, frame_num, 25, 2))
        for frame in range(frame_num):
            person_num = int(fr.readline())
            for person in range(person_num):
                fr.readline()
                joint_num = int(fr.readline())
                for joint in range(joint_num):
                    v = fr.readline().split(' ')
                    if joint < max_V and person < max_M:
                        point[0,frame,joint,person] = float(v[0])#A coordinate of a joint
                        point[1,frame,joint,person] = float(v[1])
                        point[2,frame,joint,person] = float(v[2])
                        
---------------------------------------------------------------------------------------------------------------------
                        
Prepare the drawing and select the appropriate coordinate axis according to the coordinate value 

    xmax= np.max(point[0, :, :, :])+ 0.5
    xmin= np.min(point[0, :, :, :])- 0.5
    ymax= np.max(point[1, :, :, :])+ 0.3
    ymin= np.min(point[1, :, :, :])- 0.3
    
    
---------------------------------------------------------------------------------------------------------------------

Determine which nodes are connected as bones according to NTU skeleton structure
Note that the sequence number starts from 0 and needs to be minus 1
    arms= np.array([24,12,11,10,9,21,5,6,7,8,20])-1 #Arms
    rightHand= np.array([12,25])-1 #one 's right hand
    leftHand= np.array([8,23])-1 #left hand
    legs= np.array([20,19,18,17,1,13,14,15,16]) - 1 #leg
    body= np.array([4,3,21,2,1]) -1  #body

---------------------------------------------------------------------------------------------------------------------

**after a few setting parameters, let's draw the image**

    n= 0     # Show from frame n
    m= 2 # At the end of frame m, n < m < row, this m can select a threshold less than the maximum number of frames for easy viewing. If m=1, a frame will be displayed
    plt.figure()
    plt.ion() #Use plt.ion() to convert the display mode of matplotlib to interactive mode. Even if plt.show() is encountered in the script, the code will continue to execute.
    color_point = '#03ff' #Joint point color, which can be input into the hexadecimal palette
    color_bone = 'red' #Bone color
    for i in range(n, m):
        plt.cla() ## Clear axis clears the currently active axis in the current drawing. Other axes are not affected.
        plt.scatter(point[0, i, :, :], point[1, i, :, :], c=color_point, s=40.0) #Drawing joint points through scatter diagram
        #Draw the connecting line between two points through the line diagram, that is, the bone
        plt.plot(point[0, i, arms,0], point[1, i, arms,0], c=color_bone, lw=2.0) 
        plt.plot(point[0, i, rightHand,0], point[1, i, rightHand,0], c=color_bone, lw=2.0)
        plt.plot(point[0, i, leftHand,0], point[1, i, leftHand,0], c=color_bone, lw=2.0)
        plt.plot(point[0, i, legs,0], point[1, i, legs,0], c=color_bone, lw=2.0)
        plt.plot(point[0, i, body,0], point[1, i, body,0], c=color_bone, lw=2.0)

        #Second skeleton, if any
        plt.plot(point[0, i, arms,1], point[1, i, arms,1], c=color_bone, lw=2.0)
        plt.plot(point[0, i, rightHand,1], point[1, i, rightHand,1], c=color_bone, lw=2.0)
        plt.plot(point[0, i, leftHand,1], point[1, i, leftHand,1], c=color_bone, lw=2.0)
        plt.plot(point[0, i, legs,1], point[1, i, legs,1], c=color_bone, lw=2.0)
        plt.plot(point[0, i, body,1], point[1, i, body,1], c=color_bone, lw=2.0)

        plt.text(xmax-0.5, ymax-0.1,'frame: {}/{}'.format(i, row-1)) #What frame is this
        plt.xlim(xmin, xmax) #Coordinate axis
        plt.ylim(ymin, ymax)
        plt.pause(0.001)
 
    plt.ioff()
    plt.show()
---------------------------------------------------------------------------------------------------------------------


Here are the Outputs we might get 


![skel1](https://user-images.githubusercontent.com/48506842/184855980-3cf5f952-04bf-42d3-b428-08bd90e841bd.png)


![skel2](https://user-images.githubusercontent.com/48506842/184855993-bb875c9b-b60a-4b2a-a23e-31caf1a4ff70.png)


![skel3](https://user-images.githubusercontent.com/48506842/184856002-0db7c661-60ff-4d59-8be0-a85b92fe5248.png)


---------------------------------------------------------------------------------------------------------------------


# NTU RGB+D 120 Human Action Recognition Dataset

"NTU RGB+D" is a large-scale dataset for human action recognition. It is introduced in our CVPR 2016 paper [PDF](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Shahroudy_NTU_RGBD_A_CVPR_2016_paper.pdf).

"NTU RGB+D 120" is the extended version of the "NTU RGB+D" dataset. It is introduced in our TPAMI 2020 paper [PDF](https://arxiv.org/pdf/1905.04757.pdf).

For any possible query regarding the datasets, please contact the first author of the paper.

## How to download NTU dataset

###Skeleton Only Dataset

**S001~S017**[NTU+RGB 60](https://drive.google.com/open?id=1CUZnBtYwifVXS21yVg62T-vrPVayso5H)

**S018~S032**[NTU+RGB 120](https://drive.google.com/open?id=1tEbuaEqMxAV7dNc4fqu1O4M7mC6CJ50w)

NTU RGB+D" and NTU RGB+D 120" datasets contain 56,880 and 114,480 action samples, respectively. Both datasets include 4 different modalities of data for each sample:

    RGB videos
    depth map sequences
    3D skeletal data
    infrared (IR) videos

Video samples have been captured by three Microsoft Kinect V2 cameras concurrently. The resolutions of RGB videos are 1920×1080, depth maps and IR videos are all in 512×424, and 3D skeletal data contains the 3D locations of 25 major body joints at each frame.

Each file/folder name in both datasets is in the format of SsssCcccPpppRrrrAaaa (e.g., S001C002P003R002A013), in which sss is the setup number, ccc is the camera ID, ppp is the performer (subject) ID, rrr is the replication number (1 or 2), and aaa is the action class label.

The "NTU RGB+D" dataset includes the files/folders with setup numbers between S001 and S017, while the "NTU RGB+D 120" dataset includes the files/folders with setup numbers between S001 and S032.


## More Details 

You might want to check out [here](https://github.com/shahroudy/NTURGB-D#ntu-rgbd-120-action-recognition-dataset)
