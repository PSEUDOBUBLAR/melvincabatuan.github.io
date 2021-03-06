---
layout: post
title: Superpixels
---

> "*My research areas include computer vision and computer graphics. My particular interests are in using vision to automatically build 3-D models from images, computational photography, and image-based rendering...*"  
                                       Richard Szeliski



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


By: Melvin Cabatuan melvincabatuan@gmail.com

This ipython notebook is licensed under the CC-BY-NC-SA license: http://creativecommons.org/licenses/by-nc-sa/4.0/

![http://i.creativecommons.org/l/by-nc-sa/3.0/88x31.png](http://i.creativecommons.org/l/by-nc-sa/3.0/88x31.png)

References:
    
    [1.] Radhakrishna Achanta, Appu Shaji, Kevin Smith, Aurelien Lucchi, Pascal Fua, and Sabine Süsstrunk, SLIC Superpixels Compared to State-of-the-art Superpixel Methods, TPAMI, May 2012.
    [2.] Adrian Rosebrock, Segmentation: A SLIC Superpixel Tutorial using Python. http://www.pyimagesearch.com/2014/07/28/a-slic-superpixel-tutorial-using-python
    [3.] http://ivrg.epfl.ch/research/superpixels#SLICO
    [4.] http://scikit-image.org/docs/dev/api/skimage.segmentation.html#skimage.segmentation.slic
