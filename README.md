# Quantitative: cell characterization in agar pad

### Summary

We developed customized image processing scripts based on deep learning algorithms. The processing pipeline can be summarized in four steps: first, segmenting individual cells using U-Net; second, determining edge details using Otsu's thresholding; third, calculating the midlines of cells through interpolation as a initial guess for cell size parameters determination; and lastly, calculating size parameters including length, width, and area[Ref. 1].

### Cell segmentation

U-Net model[Ref. 2] was used to detect cell objects. 

### Cell Parameters measurement

After detect the cell objects, The Otsu’s thresholding was used to trim the mask of the pre-detected cell (middle panel in Fig. 1). Otsu’s method chooses an optimal value automatically according the histogram of image, it avoids choosing the value for global thresholding, since variability of image brightness and contrast from different batch of experiments.

![Fig.1, Cell segmentation process. Left panel is the phase contrast image of a Escherichia coli cell. Middle panel represents a cell mask that generated via Otsu’s thresholding. Right Panel is the optimized cell mask that using cell coordinate system.](README.assets/Untitled.png)

Fig.1, Cell segmentation process. Left panel is the phase contrast image of a Escherichia coli cell. Middle panel represents a cell mask that generated via Otsu’s thresholding. Right Panel is the optimized cell mask that using cell coordinate system.

Finally, we use cell coordinate system to calculate the cell parameters. It supposes the bacterial cell is rod-sphere shape which was determined by longitudinal coordinate $l_c$ , radius of the cell $r_c$. The parameters of the cell coordinate system are optimized for minimizing the difference between the calculated cell mask(right panel in Fig. 1) and ground-truth binary image(middle panel in Fig. 1).

The fig. 2 is an example of the final result of cell segmentation.

<img src="README.assets/Untitled 1.png" alt="Untitled" style="zoom:50%;" />

<img src="README.assets/Untitled 2.png" alt="Untitled" style="zoom:50%;" />

Ref

1. Smit, J. H., Li, Y., Warszawik, E. M., Herrmann, A. & Cordes, T. ColiCoords: A Python package for the analysis of bacterial fluorescence microscopy data. *Plos One* **14**, e0217524 (2019).
2. Ronneberger, O., Fischer, P. & Brox, T. U-Net: Convolutional Networks for Biomedical Image Segmentation. *Arxiv* (2015).