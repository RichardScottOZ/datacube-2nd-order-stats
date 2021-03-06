# 2nd-Order Robust Temporal Statistics of Earth Observations

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) ![Release](https://img.shields.io/badge/Release-Private-ff69b4.svg)

This [datacube-stats](https://github.com/GeoscienceAustralia/datacube-stats) plug-in generates outputs to robustly understand variation in the landscape. 

The core concept of our approach is to extend the classic concept of [median absolute deviation](https://en.wikipedia.org/wiki/Median_absolute_deviation) to the multidimensional case by replacing the absolute value in the definition by a vector distance. There are many possible choices for vector distances and we choose three that are structurally different. These are the [cosine distance](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.cosine.html), the [Euclidean distance](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.euclidean.html#scipy.spatial.distance.euclidean), and the [Bray-Curtis distance](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.braycurtis.html#scipy.spatial.distance.braycurtis).

## Example Outputs

The `TernaryMAD` 3-band output demonstrates a rainbow opal-like coloring of a cropping area which means the 3 bands are uncorrelated (a highly desirable property). 
<img src="https://github.com/daleroberts/datacube-2nd-order-stats/raw/master/docs/2ndorder-ternary.png" width="800">

Visualising the `BrayCurtisDistanceMAD` over the Menindee lakes, Australia.

<img src="https://github.com/daleroberts/datacube-2nd-order-stats/raw/master/docs/2ndorder-braycurtis.png" width="800">

## Temporal Statistics

The following temporal statistics models are available:

 - `CosineDistanceMAD` (or `SMAD`) generates a single-band output where the cosine distance MAD is computed through time for every pixel.

 - `EuclideanDistanceMAD` (or `EMAD`) generates a single-band output where the Euclidean distance MAD is computed through time for every pixel.

 - `BrayCurtisDistanceMAD` (or `BCMAD`) generates a single-band output where the Bray-Curtis distance MAD is computed through time for every pixel.

 - `TernaryMAD` generates a 3-band output where the cosine distance MAD (Band 1), the Euclidean distance MAD (Band 2), the Bray-Curtis distance MAD (Band 3) is computed through time for every pixel. For this output, the distances are transformed by -log(x).


## Installation

```
git clone https://github.com/daleroberts/datacube-2nd-order-stats
```

## Continental-scale or large area

Some additional tools are contained in this repository:

  - `job.pbs` is a PBS job script that reads the `tiles` file (tiles specified in Australian Albers) and parallelises across multiple nodes.

  - `retile` is a python script (used by `job.pbs`) that reads the `config.yaml` and generates a new tiling number scheme for `datacube-stats`
     that is based on the `tile_size` parameter in `config.yaml`.

  - `stat` is a python script that gives information about how many of the output tiles have been generated so far. It is useful for checking
      the status of continental runs.

## Testing

The unittests for the package can be found in `model/test_.py`. You can use `pytest` in the root of the repository to run them.

## References

 - Roberts, D., Dunn, B., & Mueller, N. (2018, July). [Open Data Cube Products Using High-Dimensional Statistics of Time Series](https://ieeexplore.ieee.org/abstract/document/8518312). IEEE International Geoscience and Remote Sensing Symposium 2018. 8647-8650.

 - Roberts, D., Mueller, N., & Mcintyre, A. (2017). [High-dimensional pixel composites from earth observation time series](https://ieeexplore.ieee.org/abstract/document/8004469). IEEE Transactions on Geoscience and Remote Sensing, 55(11), 6254-6264.

