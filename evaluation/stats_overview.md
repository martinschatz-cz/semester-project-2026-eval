# Evaluation Chart Overview

This page embeds the evaluation charts stored in `../images/counts/`.

The chart images compare the following methods:

- `manual_count`: Points clicked manually in ImageJ/Fiji.
- `script_own`: Results from your custom-tuned Fiji macro.
- `script_simple`: Results from basic global thresholding (Class Workshop).
- `script_watershed`: Results from classic Watershed segmentation (Class Workshop).
- `script_own_sparse`: WEKA segmentation based on custom sparse training.
- `script_StarDist`: Results using the pre-trained StarDist model available in the plugin.

## Comparison Charts

### Manual Count
![Manual count distribution](../images/counts/manual_count_boxplot.png)
![Manual count evaluation](../images/counts/cv_manual_count.png)

Manual counts show mean values ranging from 56.0 (1GRAY_030-cropped, 30% overlap) to 79.25 (9GRAY_015-cropped, 15% overlap), with standard deviations from 1.93 to 4.78. The std_count tends to increase with higher overlap probability: lowest at 00% (4GRAY_000-cropped, std=2.83) and 15% (9GRAY_015-cropped, std=3.49), but higher at 30% (1GRAY_030-cropped, std=1.93) and 45% (16GRAY_045-cropped, std=4.78). This suggests that manual counting is more variable in images with moderate to high object overlap, likely due to difficulty in distinguishing touching objects.

### Custom Macro (`script_own`)

![Custom-tuned Fiji macro distribution](../images/counts/script_own_boxplot.png)
![Custom-tuned Fiji macro evaluation](../images/counts/cv_script_own.png)

The custom macro yields mean counts from 33.13 (16GRAY_045-cropped, 45% overlap) to 61.38 (4GRAY_000-cropped, 00% overlap), with std_count ranging from 4.23 to 6.09. Standard deviation is relatively stable across overlap levels, with slight increases at higher overlaps (e.g., 45% std=5.41, 30% std=4.23), indicating that the tuned macro handles varying overlap moderately well but still shows some sensitivity to object crowding.

### Basic Global Thresholding (`script_simple`)
![Basic thresholding distribution](../images/counts/script_simple_boxplot.png)
![Basic global thresholding evaluation](../images/counts/cv_script_simple.png)

Basic thresholding produces mean counts between 34.25 (16GRAY_045-cropped, 45% overlap) and 61.63 (4GRAY_000-cropped, 00% overlap), with std_count from 3.15 to 4.60. The std_count increases modestly with overlap: lowest at 30% (std=3.15) and highest at 45% (std=3.54), suggesting that global thresholding struggles more with overlapping objects, leading to higher variability in crowded images.

### Watershed Segmentation (`script_watershed`)

![Watershed distribution](../images/counts/script_watershed_boxplot.png)
![Watershed segmentation evaluation](../images/counts/cv_script_watershed.png)

Watershed segmentation results in mean counts from 53.29 (1GRAY_030-cropped, 30% overlap) to 74.71 (4GRAY_000-cropped, 00% overlap), with std_count between 2.93 and 4.91. Standard deviation is lowest at 00% overlap (std=3.90) and increases to 45% (std=3.46) and 15% (std=4.91), indicating that watershed handles low-overlap images well but becomes more variable with increasing object proximity, possibly due to oversegmentation.

### Sparse WEKA Segmentation (`script_own_sparse`)

![Sparse WEKA segmentation distribution](../images/counts/script_own_sparse_boxplot.png)
![Sparse WEKA segmentation evaluation](../images/counts/cv_script_own_sparse.png)

Sparse WEKA yields mean counts from 43.75 (16GRAY_045-cropped, 45% overlap) to 72.88 (4GRAY_000-cropped, 00% overlap), with std_count highly variable: from 0.35 (00% overlap) to 7.09 (15% overlap). This extreme range suggests the method is sensitive to overlap, with very low std at no overlap but spiking at higher overlaps, likely due to inconsistent training data handling in crowded regions.

### StarDist Model (`script_StarDist`)
![StarDist distribution](../images/counts/script_SarDist_boxplot.png)
![StarDist model evaluation](../images/counts/cv_script_SarDist.png)
StarDist produces mean counts between 51.71 (16GRAY_045-cropped, 45% overlap) and 74.57 (4GRAY_000-cropped, 00% overlap), with std_count from 1.13 to 3.30. Standard deviation is remarkably low and stable, with the highest at 15% overlap (std=3.30) and lowest at 00% (std=1.13), showing that StarDist maintains consistency even as overlap increases, making it robust to object crowding.

### Approach Ranking

Methods are ranked by standard deviation (std_count) for each overlap probability level, from lowest (most consistent) to highest (least consistent). Rankings are based on the calibration images with 00%, 15%, 30%, and 45% object overlap probabilities.

#### 00% Overlap (4GRAY_000-cropped)
1. `script_own_sparse` (std=0.35) - Extremely consistent.
2. `script_StarDist` (std=1.13) - Very low variation.
3. `manual_count` (std=2.83) - Moderate consistency.
4. `script_watershed` (std=3.90) - Good performance.
5. `script_simple` (std=4.60) - Higher variation.
6. `script_own` (std=6.05) - Least consistent.

#### 15% Overlap (9GRAY_015-cropped)
1. `script_StarDist` (std=3.30) - Most stable.
2. `manual_count` (std=3.49) - Close to StarDist.
3. `script_simple` (std=4.41) - Moderate.
4. `script_watershed` (std=4.91) - Slightly higher.
5. `script_own` (std=6.09) - Variable.
6. `script_own_sparse` (std=7.09) - Highest variation.

#### 30% Overlap (1GRAY_030-cropped)
1. `manual_count` (std=1.93) - Lowest std.
2. `script_StarDist` (std=2.43) - Very consistent.
3. `script_watershed` (std=2.93) - Good.
4. `script_simple` (std=3.15) - Moderate.
5. `script_own` (std=4.23) - Higher.
6. `script_own_sparse` (std=6.70) - Most variable.

#### 45% Overlap (16GRAY_045-cropped)
1. `script_StarDist` (std=2.21) - Best consistency.
2. `script_own_sparse` (std=2.12) - Close second.
3. `script_watershed` (std=3.46) - Solid.
4. `script_simple` (std=3.54) - Similar.
5. `script_own` (std=5.41) - Variable.
6. `manual_count` (std=4.78) - Highest among top methods.

#### Overall Ranking (Average std across overlaps)
1. `script_StarDist` (avg std=2.27) - Consistently low variation across all overlaps.
2. `manual_count` (avg std=3.26) - Reliable, especially at higher overlaps.
3. `script_watershed` (avg std=3.80) - Good overall stability.
4. `script_simple` (avg std=3.92) - Moderate consistency.
5. `script_own` (avg std=5.45) - Higher variation.
6. `script_own_sparse` (avg std=4.07) - Inconsistent, with extremes.

## Consistency and Coefficient of Variation

Coefficient of variation (CV) is the ratio of the standard deviation to the mean count, expressed as a percentage. Lower CV values indicate more consistent results across repeated measurements for the same image.

### CV Values by Method and Image

| Method | 16GRAY_045-cropped | 1GRAY_030-cropped | 4GRAY_000-cropped | 9GRAY_015-cropped | Average CV (%) |
|---|---|---|---|---|---|
| `manual_count` | 7.66 | 3.44 | 3.80 | 4.41 | 4.83 |
| `script_own` | 16.33 | 10.93 | 9.85 | 12.60 | 12.42 |
| `script_simple` | 10.32 | 8.24 | 7.46 | 8.75 | 8.19 |
| `script_watershed` | 6.35 | 5.49 | 5.22 | 7.01 | 6.02 |
| `script_own_sparse` | 4.85 | 13.67 | 0.49 | 11.57 | 7.15 |
| `script_StarDist` | 4.28 | 4.40 | 1.52 | 4.67 | 3.72 |

### Interpretation

- `script_StarDist` is the most consistent overall, with the lowest average CV (about 3.7%) and low CV values for every image.
- `manual_count` is also quite consistent, especially for the calibration images, but it still shows more variation than `script_StarDist`.
- `script_watershed` performs moderately well, with average CV around 6.0%, making it the next most consistent automatic method.
- `script_simple` and `script_own_sparse` have larger variation, and `script_own_sparse` is particularly inconsistent across images despite one very low-CV case.
- `script_own` is the least consistent, with the highest CV values across all images and an average CV above 12%.

### Conclusion

For consistency in repeated count results, `script_StarDist` is the strongest choice. `manual_count` remains stable, but the automated StarDist approach is the most reliable across the calibration images in this set.

## Baseline Reproducibility and `script_simple`

The `script_simple` method was prepared centrally and distributed to every student as the standard calibration workflow. Students only needed to apply this script to their calibration images and report the resulting counts and CV values.

Because the script was already defined, the main sources of error are not algorithm design but execution and reporting:

- Students may have applied the script to the wrong image files or to images with different cropping or preprocessing than expected.
- The script may still require a correct Fiji/ImageJ environment and version; inconsistent plugin or macro execution across machines can change outcomes.
- Reported results may have been transcribed incorrectly from the software output into the submission table.
- Some users may have changed or extended the script accidentally when adapting it, which would invalidate the assumption of a common baseline.

The CV values suggest that `script_simple` did not behave as the most consistent baseline. That means the failure was likely in the process rather than the concept: the distributed script should have provided a reproducible benchmark, but the human workflow introduced variability.

This is important because it shows two different failure modes:

1. A reproducible method can still produce inconsistent submitted results if users do not apply it uniformly.
2. A baseline that is intended to be simple and robust still needs clear instructions, version control, and a check that everyone actually used the same script.

Therefore, while `script_simple` was the method that everyone should have applied, the observed inconsistency points to execution or reporting mistakes rather than a fundamental problem with the baseline algorithm itself.