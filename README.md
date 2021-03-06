# SIRT-FISTA-TV Reconstruction Algorithm

SIRT-FISTA-TV is a regularized iterative reconstruction algorithm that is very robust to noisy and blurred data and can highly
reduce missing wedge artifacts. It consists of three steps:
1) SIRT update (SART and OS-SART could be used also)
2) TV minimization (gradient descent is used) 
3) FISTA technique to speed up convergence speed

The algorithm is accelerated on GPU using CUDA mex functions.

It depends on two toolboxes: ASTRA and Spot.
- The projection and backprojections functions of ASTRA are used.
- The Spot toolbox is used to provide a MATLAB framework that wraps linear operations into MATLAB objects that act like matrices.

We provide two examples to test the algorithm: example1.m and example2.m

## Example 1
The code named example1.m shows an example of reconstruction from simulated data. This code includes the following steps:
1. Load a 3D numerical model "3D_model_with_pores_256_256_512_float.raw" from directory "Data"
2. Generate 2D projections of this 3D model
3. Perform 3D reconstruction
4. Save reconstructed volume in directory "Reconstruction_results"

## Example 2
The code named example2.m shows an example of reconstruction from experimental data. This code includes the following steps:
1. Load 2D experimental projections "PdSiO2_aligned_tilt_series_1024_1024_69_16int" from directory "Data"
2. Perform 3D reconstruction
3. Save reconstructed volume in directory "Reconstruction_results" 


## Directories
1. "ASTRA-toolbox": includes ASTRA toolbox
2. "Spot-toolbox": includes SPOT toolbox
3. "Data": includes data that we have to reconstruct from
4. "Reconstruction_results": Reconstruction results are saved here
5. "TV minimization": includes mex cuda files for TV minimization

## Installation
1. Select "ASTRA-toolbox", "Spot-toolbox", "TV minimization" and "Data" in MATLAB file browser -----> right click -----> Add to
Path -----> Selected Folders and Subfolders. 
Note that you can type command "filebrowser" to open MATLAB file browser if it's not the case.
2. Install CUDA toolkit (version 8.0 works well) Link: https://developer.nvidia.com/cuda-80-ga2-download-archive
3. Install a C++ compiler (it's recommended to install Visual studio 2013 Community) Link: https://my.visualstudio.com/Downloads?q=visual%20studio%202013&wt.mc_id=o~msft~vscom~older-downloads


## Numerical Comparison With Noisy Data

We addded a Gaussian noise of zero mean and sigma = 2% of maximum value in noiseless projections. We show below a horizontal slice of each reconstructed volume (tilting angle range is [-70°,70°]). 


![picture1](https://user-images.githubusercontent.com/44570277/48008279-a268a880-e119-11e8-9708-70e091ee7e75.png)      ![picture2](https://user-images.githubusercontent.com/44570277/48008456-04291280-e11a-11e8-9a6f-abe32598c3e1.png)      ![picture3](https://user-images.githubusercontent.com/44570277/48008505-228f0e00-e11a-11e8-90e8-f99f6973b736.png)

### <pre>    Original Image                  SIRT                      SIRT-FISTA-TV </pre>

![picture4](https://user-images.githubusercontent.com/44570277/48009042-28d1ba00-e11b-11e8-9413-ed0b82a3d20e.png) ![picture5](https://user-images.githubusercontent.com/44570277/48009078-39823000-e11b-11e8-835b-a0cf59270366.png) ![picture6](https://user-images.githubusercontent.com/44570277/48009106-46068880-e11b-11e8-8dc0-c63455184473.png)

### <pre>SIRT + Median filtering    SIRT + Gaussian Filtering   SIRT + Anisotropic Diffusion Filtering </pre>


## Experimental Results

![picture7](https://user-images.githubusercontent.com/44570277/48009624-6125c800-e11c-11e8-87e4-12f6df4a721d.png)
## <pre>                               ART    </pre>

![picture8](https://user-images.githubusercontent.com/44570277/48009653-697e0300-e11c-11e8-95bc-860f7ffb0e5c.png)

## <pre>                          SIRT-FISTA-TV    </pre>





