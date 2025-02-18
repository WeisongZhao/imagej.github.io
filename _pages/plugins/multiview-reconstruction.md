---
mediawiki: Multiview-Reconstruction
title: Multiview-Reconstruction
project: /software/fiji
categories: [Transform,Registration,Deconvolution,ImgLib,Integral Image]
artifact: sc.fiji:SPIM_Registration
---

 

## Download

The integration of the **Multiview Reconstruction** and the [BigDataViewer](/plugins/bdv) is available through the Fiji Updater. Simply update Fiji and the Multiview-Reconstruction pipeline will be available under {% include bc path='Plugins | Multiview Reconstruction | Multiview Reconstruction Application'%}. The source code is available {% include github org='bigdataviewer' repo='SPIM_Registration' %}, please also report feature requests & bugs there.

To enable GPU hardware accelerated processing, you might want to download the **native CUDA code** for:

-   Separable Convolution: Used for the Difference-of-Gaussian segmentation, available on [GitHub](https://github.com/StephanPreibisch/SeparableConvolutionCUDALib)
-   Non-Separable Convolution: Used for the [MultiView Deconvolution](/plugins/multi-view-deconvolution), available on [GitHub](https://github.com/StephanPreibisch/FourierConvolutionCUDALib)

## Citation

Please note that the SPIM registration plugin available through Fiji, is based on a publication. If you use it successfully for your research please be so kind to cite our work:

-   S. Preibisch, S. Saalfeld, J. Schindelin and P. Tomancak (2010) "Software for bead-based registration of selective plane illumination microscopy data", *Nature Methods*, **7**(6):418-419. [Webpage](http://www.nature.com/nmeth/journal/v7/n6/full/nmeth0610-418.html) [PDF](/media/nmeth0610-418.pdf) [Supplement](/media/nmeth0610-418-s1.pdf)
-   S. Preibisch, F. Amat, E. Stamataki, M. Sarov, R.H. Singer, E. Myers and P. Tomancak (2014) "Efficient Bayesian-based Multiview Deconvolution", *Nature Methods*, **11**(6):645-648. [Webpage](http://www.nature.com/nmeth/journal/v11/n6/full/nmeth.2929.html)

For technical details about the registration method and SPIM imaging see also [SPIM Registration Method](/plugins/spim-registration/method).

## Introduction & Overview

The **Multiview Reconstruction** software package enables users to *register, fuse, deconvolve and view* multiview microscopy images (first box). The software is designed for lightsheet fluorescence microscopy (LSFM, second box), but is applicable to any form of three or higher dimensional imaging modalities like confocal timeseries or multicolor stacks.

Interactive viewing and annotation of the data is provided by integration with Tobias Pietzsch's [BigDataViewer](/plugins/bdv). Both projects share a common XML data model to describe multiview datasets.

### History

This software package is the successor to the [SPIM Registration](/plugins/spim-registration) package. While the SPIM Registration will continue to live within Fiji for the time being, we will mostly offer support only for this new software package. It has all the functionality the SPIM Registration offered, but is much more flexible and supports many more types of registration, fusion and data handling.

### Examples

{::nomarkdown}
<table>
  <thead>
    <tr class="header">
      <th>
        <p>What does 'multiview' mean exactly?</p>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>When we speak of <strong>multiview</strong> datasets we generally mean that per timepoint there <em>n</em> image stacks, which could be different:</p>
        <ul>
          <li>Channels</li>
          <li>Illumination Directions</li>
          <li>Rotation Angles</li>
        </ul>
        <p>Note that even if <em>n</em>=1, i.e. there is only one stack per timepoint, this software can be used to stabilize the timeseries (drift-correction).</p>
      </td>
    </tr>
  </tbody>
</table>
{:/}

Two examples of multiview datasets reconstructed with this software package are shown as YouTube videos below. Both datasets were registered using the bead-based registration ([*Nature Methods*, **7**(6):418-419](http://www.nature.com/nmeth/journal/v7/n6/full/nmeth0610-418.html)) and the Multiview Deconvolution ([*Nature Methods*, **11**(6):645-648](http://www.nature.com/nmeth/journal/v11/n6/full/nmeth.2929.html)), which are part of this software package. Please check out the Citation section for information on how to cite this software package.

The first video shows a developing *Drosophila* embryo expressing His-YFP in all cells. The entire embryogenesis was acquired using the Zeiss Demonstrator B. The top row shows the multiview deconvolution of this seven-view dataset, the lower row the content-based fusion.

{::nomarkdown}
<table>
  <thead>
    <tr class="header">
      <th>
        <p>Lightsheet fluorescence microscopy</p>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <p>Lightsheet fluorescence microscopy entered the world of modern biology in 2004 when <strong>Selective Plane Illumination Microscopy</strong> (<a href="http://www.sciencemag.org/content/305/5686/1007"><strong>SPIM</strong></a>) was published. It allows <em>in toto</em> imaging of large specimens by acquiring image stacks from multiple angles with high spatial and temporal resolution. Many impressive variations and extensions have been published, some of them using new variations or entirely new naming schemes:</p>
        <ul>
          <li>OpenSPIM</li>
          <li>Digital scanned laser light-sheet fluorescence microscopy (DSLM)</li>
          <li>DSLM and structured illumination (DSLM-SI)</li>
          <li>Two-photon versions of SPIM and DSLM</li>
          <li>MuVi-SPIM</li>
          <li>Two-photon light sheet microscopy (2P-LSM)</li>
          <li>Bessel-Beam illumination and DSLM</li>
          <li>Ultramicroscopy</li>
          <li>Orthogonal-plane fluorescence optical sectioning microscopy (OPFOS)</li>
          <li>Multidirectional selective plane illumination microscopy (mSPIM)</li>
          <li>Thin-sheet laser imaging microscopy (TSLIM)</li>
          <li>...</li>
        </ul>
        <p>During the 2012 Lightsheet fluorescence microscopy meeting in Dublin, organized by Emmanuel Reynaud, it was voted to summarize most of these developments under the name of <strong>Lightsheet fluorescence microscopy (LSFM)</strong>.</p>
      </td>
    </tr>
  </tbody>
</table>
{:/}

{% include video platform='youtube' id='NJHoP8RBIaw'%}

The second video shows a fixed *C. elegans* larvae in L1 stage expressing Lamin-GFP and stained with Hoechst. The four-view dataset was acquired using the Zeiss Lightsheet Z.1 microscope. It illustrates the increase in resolution that can be achieved through multiview imaging combined with multiview deconvolution. The top row shows one of the four input views, the bottom row the result of the multiview deconvolution.

{% include video platform='youtube' id='16gq2WUm-50'%}

## Detailed Tutorials

Using this software package consists of several steps. Please note that this software is more flexible and that this order is just a suggestion of how to use it in a more-or-less standard case.

-   **[Dataset Definition](/plugins/mvr-definedataset)**
    -   The first step in every reconstruction is to define the dataset and thereby create the XML file. This has to be done only once, all consecutive steps are based on this definition, i.e. the XML file.

<!-- -->

-   **[Resave the dataset as HDF5/TIFF](/plugins/mvr-resavedataset)**
    -   Once the dataset is defined, you might want to resave all the image data as HDF5 (to be able to view it using the [BigDataViewer](/plugins/bdv)) or simply as TIFF to enable fast loading of the image data. Also note that those two formats are the only ones that allow to extend the dataset/XML with newly fused data.

<!-- -->

-   **[Detect Interest Points](MVR-InterestPointDetection)**
    -   Based on an existing dataset definition (XML file), the first step is typically to find interest points in the images that will be used for registration. In this step it is possible to look for multiple types of detections, e.g. fluorescent beads, nuclei or membrane markers. All of them can be stored in parallel.

<!-- -->

-   **[Interest Point Registration](MVR-InterestPointRegistration)**
    -   Once interest points are detected, they can be used to register/align multiple views over time. To find corresponding detection the registration module supports the following modules:
        -   *Rotation-invariant matching* using fluorescent beads (no prior transformation knowledge necessary)
        -   *Translation-invariant matching* using any kind of detections (an approximate knowledge of the rotation is required, e.g. 45 degrees around the x-axis. Check the [Tools-Section](/plugins/multiview-reconstruction#tools) for how to provide approximate transformations.)
        -   *Precise matching* using the Iterative-Closest Point (ICP) algorithm (the dataset needs to be aligned using for example any of the above methods).
    -   The different views (or timepoints) can be aligned using *Translation*, *Rigid* or *Affine* transformation models. We also support *regularized transformation models* developed by Stephan Saafeld.
    -   Alignment over time can be performed in different ways
        -   If there is no drift, every timepoint can be simply registered individually. Please note that it is possible to register each timepoint and later on treat it as a *rigid unit*. In this way it is possible to first register each timpoint using an *affine* transformation model and consecutively stabilize over time just using a *translation* model.
        -   A reference timepoint that is individually registered first can serve as basis for all other timepoints. This kind of alignment usually only works with external landmarks like fluorescent beads.
        -   Alternatively, it is possible to align timepoints using a sliding window of +-n timepoints, in which all views are matched against each other. This will work on any kind of detections.
    -   In general, it is possible to stack up as many rounds of transformations as you want. They will be summarized in a list transformations that are concatenated to one single *affine* transformation before fusion/deconvolution/viewing. A typical list of transformations looks like:
        -   Apply calibration (difference in xy and z resolution per pixel)
        -   Affine bead-based registration
        -   ICP registration based on nuclei

<!-- -->

-   **[Fusion/Deconvolution](/plugins/mvr-fusiondeconvolution)**
    -   Once the dataset is entirely aligned it can be fused or deconvolved into a single image per timepoint and channel. Deconvolution requires the knowledge of point spread functions (PSF's), which can be extracted from matched beads directly or can be provided by the user.
    -   Alternatively, there is no need to fuse the data and you can interactively look at the data using the [BigDataViewer](/plugins/bdv) if you resaved it as HDF5. You can still do that now after the registration is complete.

### Tools

Apart from this potential processing outline there are many **tools** available to help process multiview timelapse datasets.

-   **[Apply Transformations](MVR-ApplyTransformations)**
    -   This tool can be used to apply any kind of transformations to individual views, or all views at once. This allows the user to specify a know rotation of different acquisition angles around an axis or to simply re-orient the entire dataset after the registration is complete.

<!-- -->

-   **[Duplicate Transformations](MVR-DuplicateTransformations)**
    -   It can be used to apply transformations that have been computed (or defined) for a certain subset of views/timepoints to other views/timepoints. Typical scenarios where this is required are:
        -   Fluorescent beads are only visible in one channel, but the user wants to do apply the same transformation for all other channels
        -   The user registered one timepoint and wants to apply the same transformation for all other timepoints

<!-- -->

-   **[Display View](MVR-DisplayView)**
    -   It allows to simply load and display one of the views as defined in the dataset

<!-- -->

-   **[Specify Calibration](MVR-SpecifyCalibration)**
    -   This enables the user to change the calibration of individual or all views after having defined them. Note that all registrations need to be recomputed if it should reflect the new calibration.

<!-- -->

-   **[Visualize Detections](MVR-VisualizeDetections)**
    -   Detections as identified by [Detect Interest Points](MVR-InterestPointDetection) can be visualized. It is possible to visualize all detections or only those that are found to be corresponding with other detections and were therefore used for registration. This helps to identify potential misalignments if corresponding detections are not equally distributed around the sample as they should be. One can also load the input view at the same time to overlay the detections with the image data

## Video Tutorials & Scientific Talks

During the [EMBO Practical Course on Lightsheet Microscopy](http://openspim.org/EMBO_practical_course_Light_sheet_microscopy) two of my talks were recorded:

### Talk: Registration of Multiview Lightsheet Fluorescence Microscopy (LSFM) Images

{% include video platform='youtube' id='IupXS_On2rg'%}

This 30-minute talk by {% include person id='StephanPreibisch' %} covers the theory behind registration of multiview lightsheet microscopy data and it also quickly addresses the problem of multiview fusion & deconvolution.

### Tutorial: Fiji Multiview Lightsheet Reconstruction Software

{% include video platform='youtube' id='0IkaSwfPYw0'%}

This one hour tutorial by {% include person id='StephanPreibisch' %} covers the basic usage of this multiview reconstruction software for Fiji. Documentation, source code, bug reports and feature requests can be found [on SourceForge](https://sourceforge.net/projects/multiviewreconstruction/).

## Comments, Bugs & Feature Requests

There is a webpage on [GitHub](https://github.com/bigdataviewer/SPIM_Registration) and [SourceForge](https://sourceforge.net/projects/multiviewreconstruction/) dedicated to this project. It contains links to this documentation, the source code and other related things. All comments, bugs & feature requests should be posted in the [GitHub issues](https://github.com/bigdataviewer/SPIM_Registration/issues) or the [SourceForge discussion board](https://sourceforge.net/p/multiviewreconstruction/discussion/?source=navbar).

## Downloading example dataset

There is a 7-angle SPIM dataset of *Drosophila* available for download [here](http://fly.mpi-cbg.de/preibisch/nm/HisYFP-SPIM.zip). Other datasets can be provided upon request.

## System requirements

Multi-view SPIM datasets are typically rather large, therefore it is recommended to use the registration plugin on a computer with a lot of RAM. The minimal requirement for the example dataset is **at least 4Gb** of memory however we recommend an **16Gb+** system, ideally at least **64Gb** and a CUDA capable graphics card. You may need to increase the Fiji memory limit by going to {% include bc path="Edit|Options|Memory & Threads" %}.

## Cluster processing

See the dedicated [page](/plugins/automated-workflow-for-parallel-multiview-reconstruction) describing an automated workflow for processing SPIM data from Lighsheet.Z1 and OpenSPIM on the MPI-CBG cluster.

      
