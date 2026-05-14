# Nuclear Image Analysis: Human vs. AI Benchmark

[UCT-Advanced-Image-Analysis/semester-project-2026](https://github.com/UCT-Advanced-Image-Analysis/semester-project-2026)

Welcome to our collaborative research project! This semester, we are benchmarking various image analysis workflows—ranging from manual counting to Deep Learning—to quantify how object overlap (0%–45%) impacts scientific data integrity. You will learn what are the challenges and benefits of each approach.

Your contributions will serve as the foundation for a comparative study on **Inter-rater variability and Model Robustness**.

---

## Project Structure

Each student is assigned a unique ID (`student_01` and so on). Your workspace consists of:
* **`images/`**: Your assigned 15 TIFF images.
* **`images/student_XY/masks/`**: A subfolder for your Phase 4 pixel-wise segmentations.
* **`student_XY_counts.csv`**: Your master reporting table. (Copy the template to your folder and replace the XY by your ID)

---

## The Reporting Table

Update your `.csv` file incrementally. **Do not change column names or the file structure.** 
| Column | Description |
| :--- | :--- |
| **image_id** | Filename of the image (e.g., `img_01.tif`). |
| **manual_count** | Points clicked manually in ImageJ/Fiji. |
| **script_own** | Results from your custom-tuned Fiji macro. |
| **[script_simple](https://raw.githubusercontent.com/UCT-Advanced-Image-Analysis/semester-project-2026/refs/heads/main/scripts/ms_simple_macro.ijm)** | Results from basic global thresholding (Class Workshop, same script for everyone). |
| **script_watershed** | Results from classic Watershed segmentation (Class Workshop). |
| **[script_own_sparse](https://raw.githubusercontent.com/UCT-Advanced-Image-Analysis/semester-project-2026/refs/heads/main/scripts/weka-Macro.ijm)** | WEKA egmantation based - with own sparse training |
| **[script_StarDist](https://raw.githubusercontent.com/UCT-Advanced-Image-Analysis/semester-project-2026/refs/heads/main/scripts/StarDist-Macro.ijm)** | Results using the **Pre-trained StarDist model**, available in plugin. |
| **YOLO_count** | Number of bounding boxes detected (Phase 5 - Optional). |

---

## Semester Phases & Instructions

### Phase 1: Manual Baseline
* **Task:** Perform manual point counting in Fiji/ImageJ.
* **Goal:** Establish a "Human Gold Standard" and measure inter-rater variability.
* **Note:** Some images are hidden duplicates to test your individual consistency (Intra-rater test).

### Phase 2: Classic Computer Vision
* **Task:** Apply global thresholding and Watershed. Compare your own script vs script we make together in class.
* **Focus:** Identify the "breaking point" where classic algorithms fail to separate overlapping nuclei. Test limits of reproducibility.

### Phase 3: Pre-trained StarDist
* **Task:** Run the pre-trained **StarDist** model (instance segmentation).
* **Focus:** Observe how Star-convex polygons handle the 30% and 45% overlap cases compared to Watershed.

### Phase 4: Pixel-wise Annotation
* **Task:** Create precise binary masks for your unique image set.
* **Output:** Save results as `.tif` files in your `/mask` subfolder.
* **Format:** Name them identically to the source image (e.g., `img_01.tif` source $\rightarrow$ `img_01.tif` mask). These will be used to evaluate pixel-level accuracy (Jaccard/Dice indices).
* **Focus:** Pixel-wise comparison, differences in anotation, challenges in annotation and model training.



### Phase 5: YOLO Detection (Optional / Bonus) - Not finished
* **Task:** Annotate Bounding Boxes and train a **YOLO** object detection model.
* **Focus:** Compare detection-only accuracy against full instance segmentation.

---

## Licencing

The original image data and ground truth masks are from "image set [BBBC004v1](https://bbbc.broadinstitute.org/BBBC004) [Ruusuvuori et al., in Proc. of the 16th European Signal Processing Conference (EUSIPCO-2008), 2008] from the Broad Bioimage Benchmark Collection [Ljosa et al., Nature Methods, 2012](http://dx.doi.org/10.1038/nmeth.2083)." This data is licenced udner a [Creative Commons Attribution-NonCommercial-ShareAlike 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/) [Unported License](http://creativecommons.org/licenses/by-nc-sa/3.0/) by [Pekka Ruusuvuori](pekka.ruusuvuori@tut.fi).

Rest of the content is under [Creative Commons Attribution 4.0 International](https://creativecommons.org/licenses/by/4.0/) licence.

---
**Contact:** If you find corrupted images or have issues with the StarDist plugin, please open an "Issue" in this repository.

---

### Contributors

<table>
<tr>
    <td align="center" style="word-wrap: break-word; width: 150.0; height: 150.0">
        <a href=https://github.com/martinschatz-cz>
            <img src=https://avatars.githubusercontent.com/u/61615369?v=4 width="100;"  style="border-radius:50%;align-items:center;justify-content:center;overflow:hidden;padding-top:10px" alt=Martin Schätz/>
            <br />
            <sub style="font-size:14px"><b>Martin Schätz</b></sub>
        </a>
    </td>
    <td align="center" style="word-wrap: break-word; width: 150.0; height: 150.0">
        <a href=https://github.com/slonkovl>
            <img src=https://avatars.githubusercontent.com/u/263561715?v=4 width="100;"  style="border-radius:50%;align-items:center;justify-content:center;overflow:hidden;padding-top:10px" alt=Lucie Slonková/>
            <br />
            <sub style="font-size:14px"><b>Lucie Slonková</b></sub>
        </a>
    </td>
    <td align="center" style="word-wrap: break-word; width: 150.0; height: 150.0">
        <a href=https://github.com/krenkovm>
            <img src=https://avatars.githubusercontent.com/u/263197032?v=4 width="100;"  style="border-radius:50%;align-items:center;justify-content:center;overflow:hidden;padding-top:10px" alt=Martina Krenkova/>
            <br />
            <sub style="font-size:14px"><b>Martina Krenkova</b></sub>
        </a>
    </td>
    <td align="center" style="word-wrap: break-word; width: 150.0; height: 150.0">
        <a href=https://github.com/matusuklara>
            <img src=https://avatars.githubusercontent.com/u/263565769?v=4 width="100;"  style="border-radius:50%;align-items:center;justify-content:center;overflow:hidden;padding-top:10px" alt=Klára Matúšů/>
            <br />
            <sub style="font-size:14px"><b>Klára Matúšů</b></sub>
        </a>
    </td>
    <td align="center" style="word-wrap: break-word; width: 150.0; height: 150.0">
        <a href=https://github.com/zuzkito>
            <img src=https://avatars.githubusercontent.com/u/247555077?v=4 width="100;"  style="border-radius:50%;align-items:center;justify-content:center;overflow:hidden;padding-top:10px" alt=Zuzka/>
            <br />
            <sub style="font-size:14px"><b>Zuzka</b></sub>
        </a>
    </td>
    <td align="center" style="word-wrap: break-word; width: 150.0; height: 150.0">
        <a href=https://github.com/Jingr33>
            <img src=https://avatars.githubusercontent.com/u/173592834?v=4 width="100;"  style="border-radius:50%;align-items:center;justify-content:center;overflow:hidden;padding-top:10px" alt=Jiří Ingr/>
            <br />
            <sub style="font-size:14px"><b>Jiří Ingr</b></sub>
        </a>
    </td>
</tr>
<tr>
    <td align="center" style="word-wrap: break-word; width: 150.0; height: 150.0">
        <a href=https://github.com/mokrith>
            <img src=https://avatars.githubusercontent.com/u/158511077?v=4 width="100;"  style="border-radius:50%;align-items:center;justify-content:center;overflow:hidden;padding-top:10px" alt=mokrith/>
            <br />
            <sub style="font-size:14px"><b>mokrith</b></sub>
        </a>
    </td>
    <td align="center" style="word-wrap: break-word; width: 150.0; height: 150.0">
        <a href=https://github.com/Annalisik>
            <img src=https://avatars.githubusercontent.com/u/184008534?v=4 width="100;"  style="border-radius:50%;align-items:center;justify-content:center;overflow:hidden;padding-top:10px" alt=Annalisik/>
            <br />
            <sub style="font-size:14px"><b>Annalisik</b></sub>
        </a>
    </td>
</tr>
</table>

This project is a collaborative effort by students in the Advanced Image Analysis course at [UCT](https://www.vscht.cz).

