In [notebook_02.ipynb](/notebook_02.ipynb) tried mutliple pipelines different combination of control net conditioning such as :
- depth
- depth, canny
- depth, normal
- depth, canny, normal
- depth , normal , canny
- canny, depth, normal

Some input depth images, such as 168x168 or 177x177, result in distorted outputs, sometimes even generating NSFW content. 
Additionally, a depth image with a resolution of 2668x2668 produces very noisy outputs. 
Therefore, decided to resize all inputs to a standard size of 512x512.

Also normalized input depth image to (0,255)


## Final Pipeline
1. Normalize each depth image such that its pixel values are scaled between 0 and 255. This normalization ensures that all depth images are on a comparable scale for visualization and processing.
2. Resize all depth images to a standard size of 512x512xch pixels to ensure uniform input to the model and ease of comparison across various images. Using this fixed size simplifies the processing pipeline.
3. Convert depth image to normals, then use ControlNet pipeline to apply depth conditioning followed by normals conditioning for improved generation.

-----------------

Here for each text prompt, provide three set of images
- one is input depth image, canny edge image followed by normal image extracted from given depth image.
- generated output image
- comparison shown between input depth image vs depth image extracted from generated output image

### beautiful landscape, mountains in the background
-----------------
<img src="./outputs/depth_canny_normal_0.png" alt="Logo" width="500"/>
<img src="./outputs/depth_output_0.png" alt="Logo" width="250"/>
<img src="./outputs/depth_comparison_0.png" alt="Logo" width="400"/>

-----------------
### luxury bedroom interior
<img src="./outputs/depth_canny_normal_1.png" alt="Logo" width="500"/>
<img src="./outputs/depth_output_1.png" alt="Logo" width="250"/>
<img src="./outputs/depth_comparison_1.png" alt="Logo" width="400"/>

-----------------

### Beautiful snowy mountains
<img src="./outputs/depth_canny_normal_2.png" alt="Logo" width="500"/>
<img src="./outputs/depth_output_2.png" alt="Logo" width="250"/>
<img src="./outputs/depth_comparison_2.png" alt="Logo" width="400"/>

-----------------


### luxurious bedroom interior
<img src="./outputs/depth_canny_normal_3.png" alt="Logo" width="500"/>
<img src="./outputs/depth_output_3.png" alt="Logo" width="250"/>
<img src="./outputs/depth_comparison_3.png" alt="Logo" width="400"/>

-----------------


### walls with cupboard
<img src="./outputs/depth_canny_normal_4.png" alt="Logo" width="500"/>
<img src="./outputs/depth_output_4.png" alt="Logo" width="250"/>
<img src="./outputs/depth_comparison_4.png" alt="Logo" width="400"/>

-----------------


### room with chair
<img src="./outputs/depth_canny_normal_5.png" alt="Logo" width="500"/>
<img src="./outputs/depth_output_5.png" alt="Logo" width="250"/>
<img src="./outputs/depth_comparison_5.png" alt="Logo" width="400"/>

-----------------


### House in the forest
<img src="./outputs/depth_canny_normal_6.png" alt="Logo" width="500"/>
<img src="./outputs/depth_output_6.png" alt="Logo" width="250"/>
<img src="./outputs/depth_comparison_6.png" alt="Logo" width="400"/>

-----------------



Also extracted depth from generated output using [Monocular depth estimation](https://huggingface.co/docs/transformers/en/tasks/monocular_depth_estimation) and verified visually.
It is visually almost same. 

See [final_pipeline.ipynb](/final_pipeline.ipynb) for the final output.

## Aspect ratio 

In [aspect_ratio.ipynb](/aspect_ratio.ipynb), it was demonstrated that for a given text prompt, we have two different depth images: 
one with an aspect ratio of 1:1 and the other with an aspect ratio close to 16:9.

Yes we can generate different aspect ratio image from Stable Diffusion.




## Reducing Generation Latency

In this [reducing generation latency](/reducing_generation_latency.ipynb) notebook, we demonstrate methods to quickly reduce generation latency. The image below was generated with the default number of inference steps (i.e., 50) and default resolution, taking 3.36 seconds to produce. 

<img src="./outputs/original_latency.png" alt="Logo" width="300"/>



One way to reduce generation time is by decreasing the number of inference steps in the Stable Diffusion pipeline. In this case, the generation time was reduced to 2.1 seconds. 

<img src="./outputs/reduce_inference_steps.png" alt="Logo" width="300"/>



Another approach is to reduce the resolution of the generated output image, which resulted in a generation time of 2.7 seconds. 

<img src="./outputs/reduce_resolution.png" alt="Logo" width="300"/>

From a visual inspection, we can conclude that reducing latency also reduces the quality of the generated image.








