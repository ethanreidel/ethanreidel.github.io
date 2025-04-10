---
title: "image registration 1"
date: 2025-03-26T14:40:53-07:00
summary: "initial blog post entry detailing image registration techniques and its application to astronomical image stacking"
#draft: true
---

#### blog 1: foundations of image registration

###### published March 26 2025

<span style="font-size:14px">
This is my initial entry for a series of blogs intended to deepen my understanding of image registration applied to astrophotography. Based heavily off of 
 <a href="https://gregorygundersen.com/">Gregory Gundersen's blog</a>. 
</span>

#### introduction: what is image registration?

<span style="font-size:14px">
Image registration is the process of finding an appropriate transformation <i>T</i> given two images: a fixed image (<i>I<sub>F</sub></i>) and a moving image (<i>I<sub>M</sub></i>), such that <i>I<sub>M</sub></i> is spatially aligned with <i>I<sub>F</sub></i>. In general, we choose a fixed image <i>I<sub>F</sub></i> and transform <i>I<sub>M</sub></i> onto <i>I<sub>F</sub></i>.

I like to think of this process using an example from astro imaging. Given two mis-aligned images of the night sky, how do we find an appropriate series of transformations such that the two images stacked present a natural image. I naturally think that this problem could be solved through deep learning algorithms. I will touch on that topic later. Back to the basics.
</span>

#### types of transformation models
<span style="font-size:14px">
Depending on the problem at hand, we may choose different types of transformation models. A transformation model describes the mathematical framework that constrains how the moving image can be aligned with the fixed image. One of the simplest transformation models is the rigid transformation, where we are limited to only translations and rotations, which preserve distances and angles. 
<p></p>


DISCUSS INTERPOLATION METHODS IN THIS AT SOME POINT

We can represent rotations and translations in 2D with a singular matrix:


in order to optimize/minimize the SSD, we need to perform a few steps:
take partials of ssd w.r.t to P where P_i is each transform parameter (tx, ty, theta)





$$
M_{rigid}=
\begin{pmatrix}
1 & 0 & 0 \\\
0 & \cos\theta_x & -\sin\theta_x \\\
0 & \sin\theta_x & \cos\theta_x
\end{pmatrix}
\begin{pmatrix}
\cos\theta_y & 0 & \sin\theta_y \\\
0 & 1 & 0 \\\
-\sin\theta_y & 0 & \cos\theta_y
\end{pmatrix}
\begin{pmatrix}
\cos\theta_z & -\sin\theta_z & 0 \\\
\sin\theta_z & \cos\theta_z & 0 \\\
0 & 0 & 1
\end{pmatrix}.
$$

</span>




#### posing image registration as an optimization problem
<span style="font-size:14px">
Traditional image registration algorithms can be posed as an optimization problem, where given a cost function, we try and optimize the output of it. Formally, let <i>I<sub>F</sub></i> and <i>I<sub>M</sub></i> represent our fixed and moving images respectively. In two-dimensional space, our image coordinates are represented by <b>x</b> = <i>(x, y)</i> and <b>x'</b> = <i>(x', y')</i>. We want to approximate a transformation <b>T</b> : <b>&#8477</b><sup><i>d</i></sup> &#8594; <b>&#8477</b><sup><i>d</i></sup> (d is two in our case) such that <i>I<sub>M</sub></i>(<b>T</b>(<b>x</b>)) &#8776 <i>I<sub>F</sub></i><i></i>(<b>x</b>), for all <b>x</b> &#8712; &#937; where &#937; is our spatial domain (space in which our coordinates live). While thinking about how image coordinates are represented, I think it is interesting to touch on how the spatial domain of coordinates behaves more like an <i>affine space</i> than a strict vector space. Since translations break the origin preserving axiom of vector spaces, an affine space, which disregards the origin, is a more appropriate representation.

</span>

DISCUSS OPTIMIZATION TECHNIQUES (GAUSS-NEWTON/GRADIENT DESCENT)
#### common loss functions










sources (format later): https://www.ncbi.nlm.nih.gov/books/NBK597490/
https://staff.fnwi.uva.nl/r.vandenboomgaard/IPCV20162017/LectureNotes/IP/Images/ImageDefinition.html