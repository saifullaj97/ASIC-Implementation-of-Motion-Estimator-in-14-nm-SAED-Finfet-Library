# ASIC-Implementation-of-Motion-Estimator-in-14-nm-SAED-Finfet-Library
The objective of this project is the RTL2GDSII implementation of Motion Estimator design used for lowering data size while retaining video quality in video compression in cutting-edge 14nm Finfet technology. 

In the realms of computer vision and image processing, motion estimation is the intricate task of deducing motion vectors. These vectors encapsulate the transformation from one 2D image to another, commonly between successive frames in a video sequence. This undertaking is considered 'ill-posed' due to the complexity of motion occurring in three dimensions (3D), while the captured images only reflect a projection of this 3D motion onto a 2D plane. These motion vectors can pertain to the entirety of the image (known as global motion estimation), or to specific components like rectangular blocks, arbitrarily shaped patches, or even on a per-pixel basis. The representation of these motion vectors can be achieved through various models, ranging from translational to more intricate ones mimicking the motion of an actual video camera, encompassing rotations, translations in all three dimensions, and zooming effects.

Motion Estimator
• Task: Detect blocks of video data in successive frames that are related only via a translation.
• Digital Video is captured as blocks of 16x16 pixels
• Want to determine if block has moved largely unchanged
• If true can transmit motion vector rather than block
• Permits high level of compression
• Example (4x4 block)

Reference Block in
Frame 1
“Draw block” with
motion vector (1,2)
in frame 2
