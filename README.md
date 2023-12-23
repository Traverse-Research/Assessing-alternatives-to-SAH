# 🏗️ Assessing Alternatives to the Surface Area Heuristic for Bounding Volume Hierarchy Construction
![image](https://github.com/Traverse-Research/Assessing-alternatives-to-SAH/assets/7345604/85e44a7f-a629-4488-98cd-402042b51167)

In this repository you can find the raw testing data and Master thesis by Athos van Kralingen on "Assessing Alternatives to the Surface Area Heuristic for Bounding Volume Hierarchy Construction". The final thesis can also be found [in here](https://github.com/Traverse-Research/Assessing-alternatives-to-SAH/blob/main/master_thesis_bvhs.pdf).

## Data
### Globally Optimal SAH 
The part of the thesis that researches the non-greedy SAH construction also has a dump of raw data that will be uploaded here soon.

### Existing Heuristic Analysis
The raw collected data with detailed timings and number of rays per frame per ray type, can be found in json format in `heuristic_analysis_raw_data`. Note that there is some mixing and matching of data and that while sometimes there is more data than processed for the thesis, this is not always complete. One example for this is the build statistics (SAH & EPO), which are not fully available for animated test runs that rebuilt their BVH every frame nor 3 frames for every scene. The naming scheme for the raw data works can be described as this (`?` indicates optional, `|` indicates an option): 

`(animated-no-rebuild|animated-rebuild-[interval]|static)(-ray-configuration-[configuration])?(-with-build-statistics)?(-build-only)?-[scene_name]-[build_heuristic]-(binned|guided)-statistics.json

- animated-no-rebuild|animated-rebuild-\[interval\]|static - Whether the test scene was tested in its static setting (i.e. from one position) or animated (i.e. from the given camera spline), whether the latter optionally rebuilds the BVH every \[interval\] frames. Note that the interval-based builds are only available for RDH and OSAH, as they are irrelevant for others
- ray-configuration-\[configuration\] - Optionally describes using which input ray distributions where used to construct the BVH. Data only available for RDH and OSAH (others have no input ray sets). One of \[primary, diffuse (first and second bounce), diffuse1st (first bounce only), diffuse2nd (second bounce only), shadow, ao]. If not specified, all ray distributions are used for the input set of rays.
- with-build-statistics - Optionally calculates build statistics (EPO + SAH) for _every_ constructed BVH. 
- build-only - Same as `with-build-statistics`, except no tracing data is in this raw data. This was used mostly for submitting a fix to the BVH data, so it should be combined with other frame data files.
- scene_name - The tested scene. One of \[bunny, dragon, sponza, bistro, sibenik, san_miguel, soda_hall, conference_room]
- build_heuristic - The heuristic used for construction. One of \[sah, perspective-projected-sah, scene-interior-ray-origin-metric-approx, scene-interior-ray-origin-metric-full, osah, rdh]
- binned|guided - The research ended up discussing and processing BVH builds using binning only, but there is also some data left from non-binned BVH construction. The quality should be higher and timings should be lower, though they are not guaranteed to be.
