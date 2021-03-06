---
layout: post
title: SLIC Superpixels 
---

> "*Superpixel segmentation algorithms can be very useful as a preprocessing step for computer vision applications like object class recognition and medical image segmentation. To be useful, such algorithms should output high quality superpixels. There are few superpixel algorithms that can offer this and scale up for practical applications that deal with images greater than 0.5 million pixels. We present a novel O(N) complexity superpixel segmentation algorithm that is simple to implement and outputs better quality superpixels for a very low computational and memory cost...*"  
                                       Radhakrishna Achanta et al.
 


<iframe src="https://docs.google.com/a/dlsu.edu.ph/file/d/0B6GYu_QtcFzQemhPSXZFM2REZGc/preview" width="640" height="480"></iframe>


# Preliminaries


    import matplotlib.pyplot as plt
    from skimage.segmentation import slic
    from skimage.segmentation import mark_boundaries
    from skimage.util import img_as_float
    from skimage import io
    
    %pylab inline
    %matplotlib inline 

    Populating the interactive namespace from numpy and matplotlib


# Input image


    img = img_as_float(io.imread('/home/cobalt/Pictures/frances2.jpg'))
    io.imshow(img);


![_config.yml]({{ site.baseurl}}/images/Superpixel_3_0.png)


# Oversegmentation to produce the Superpixels


    for segs in (10, 50, 100, 300, 500, 1000):
        segments = slic(img, n_segments = segs, sigma = 4)
        fig = plt.figure(figsize=(12,4))
        ax = fig.add_axes([0, 0, 1, 1])
        ax.imshow(mark_boundaries(img, segments)) 
    plt.show()


![_config.yml]({{ site.baseurl}}/images/Superpixel_5_0.png)



![_config.yml]({{ site.baseurl}}/images/Superpixel_5_1.png)



![_config.yml]({{ site.baseurl}}/images/Superpixel_5_2.png)



![_config.yml]({{ site.baseurl}}/images/Superpixel_5_3.png)



![_config.yml]({{ site.baseurl}}/images/Superpixel_5_4.png)



![_config.yml]({{ site.baseurl}}/images/Superpixel_5_5.png)


# Comparison of segmentation and superpixel algorithms

http://scikit-image.org/docs/dev/auto_examples/plot_segmentations.html


    from __future__ import print_function
    
    import matplotlib.pyplot as plt
    import numpy as np
    
    from skimage.data import astronaut
    from skimage.segmentation import felzenszwalb, slic, quickshift
    from skimage.segmentation import mark_boundaries
    from skimage.util import img_as_float
    
    segments_fz = felzenszwalb(img, scale=100, sigma=0.5, min_size=50)
    segments_slic = slic(img, n_segments=250, compactness=10, sigma=1)
    segments_quick = quickshift(img, kernel_size=3, max_dist=6, ratio=0.5)
    
    print("Felzenszwalb's number of segments: %d" % len(np.unique(segments_fz)))
    print("Slic number of segments: %d" % len(np.unique(segments_slic)))
    print("Quickshift number of segments: %d" % len(np.unique(segments_quick)))
    
    fig, ax = plt.subplots(1, 3)
    fig.set_size_inches(16, 8, forward=True)
    fig.subplots_adjust(0.05, 0.05, 0.95, 0.95, 0.05, 0.05)
    
    ax[0].imshow(mark_boundaries(img, segments_fz))
    ax[0].set_title("Felzenszwalbs's method")
    ax[1].imshow(mark_boundaries(img, segments_slic))
    ax[1].set_title("SLIC")
    ax[2].imshow(mark_boundaries(img, segments_quick))
    ax[2].set_title("Quickshift")
    for a in ax:
        a.set_xticks(())
        a.set_yticks(())
    plt.show()

    Felzenszwalb's number of segments: 2879
    Slic number of segments: 247
    Quickshift number of segments: 1852



![_config.yml]({{ site.baseurl}}/images/Superpixel_7_1.png)


#### References:
    
    [1.] Radhakrishna Achanta, Appu Shaji, Kevin Smith, Aurelien Lucchi, Pascal Fua, and Sabine Süsstrunk, SLIC Superpixels Compared to State-of-the-art Superpixel Methods, TPAMI, May 2012.
    [2.] Adrian Rosebrock, Segmentation: A SLIC Superpixel Tutorial using Python. http://www.pyimagesearch.com/2014/07/28/a-slic-superpixel-tutorial-using-python
    [3.] Felzenszwalb, P.F. and Huttenlocher, D.P., Efficient graph-based image segmentation, International Journal of Computer Vision, 2004
    [4.] A. Vedaldi and S. Soatto, Quick shift and kernel methods for mode seeking, European Conference on Computer Vision, 2008
    [5.] http://ivrg.epfl.ch/research/superpixels#SLICO
    [6.] http://scikit-image.org/docs/dev/api/skimage.segmentation.html#skimage.segmentation.slic
