## skeleton_read-Display
Reading NTU Skeleton data and 2d display

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


##More Details 

You might want to check out [here](https://github.com/shahroudy/NTURGB-D#ntu-rgbd-120-action-recognition-dataset)
