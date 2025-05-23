---
title: "Generalizable Unsupervised Microscopy Video Denoising via Weighted SpatioTemporal Sampling"
---


<!-- ✅ MathJax injection for LaTeX rendering -->
<script type="text/javascript" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js">
</script>

<!-- ✅ Add in your index.md just after the front matter `---` -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
<link href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.3/font/bootstrap-icons.css" rel="stylesheet">


<style>
.link_button {
  display: inline-block;
  padding: 10px 16px;
  margin: 5px;
  font-size: 16px;
  background-color: #007bff;
  color: white;
  border-radius: 6px;
  text-align: center;
  text-decoration: none;
}
.link_button:hover {
  background-color: #0056b3;
}
</style>


<center>

<h1>Generalizable Unsupervised Microscopy Video Denoising via</h1>
<h1>Weighted SpatioTemporal Sampling</h1>

<!-- <h1 style="display: block;">Unsupervised Microscopy Video Denoising</h1> -->
<table style="border: none; display: initial;">
<tr style="border: none;">
<td style="border: none;"><a href="https://maryaiyetigbo.github.io/">Mary Damilola Aiyetigbo</a><sup>1</sup></td>
<td style="border: none;"><a href="mailto:wanqiy@clemson.edu">Wanqi Yuan</a><sup>1</sup></td>
<td style="border: none;"><a href="mailto:luofeng@clemson.edu">Feng Luo</a><sup>1</sup></td>
<td style="border: none;"><a href="mailto:xli48@albany.edu">Xin Li</a><sup>2</sup></td>
<td style="border: none;"><a href="mailto:ye7@clemson.edu">Tong Ye</a><sup>1</sup></td>
<td style="border: none;"><a href="mailto:nianyil@clemson.edu">Nianyi Li</a><sup>1</sup></td>
</tr>
</table>
<br>
<table style="border: none; display: initial;">
<tr style="border: none;">
<td style="border: none;"><sup>1</sup>Clemson University</td>
<td style="border: none;"><sup>2</sup>Department of Computer Science, University at Albany - State University of New York</td>
</tr>
</table>

<br>

<table style="border: none; display: initial;">
<tr style="border: none;">
<td style="border: none;">
<a href="#" style="color: #ffffff">
<div class="link_button">
<i class="bi bi-file-earmark-richtext"></i> Paper
</div>
</a>
</td>
<td style="border: none; display: initial;">
<a href="https://github.com/maryaiyetigbo/STS-UVD" style="color: #ffffff">
<div class="link_button">
<i class="bi bi-github"></i> Code
</div>
</a>
</td>
</tr>
</table>

</center>


<!-- ## Two Photon Calcium Imaging
 <img src="./assets/highActivityb.gif" width="1000"/> -->

# Abstract

Medical video denoising is essential for improving image quality and enhancing the reliability of clinical data. However, the limited availability of annotated datasets, the variability of noise patterns, and the absence of ground-truth reference frames present significant challenges for traditional supervised denoising approaches. On the other hand, current unsupervised video denoising methods often struggle to balance noise removal and motion preservation, leading to either excessive smoothing that degrades fine details or insufficient denoising that leaves residual noise.
To address these challenges, we propose STS-UVD, a novel unsupervised video denoising (UVD) method that removes noise while preserving motion integrity. By refining the optical flow, our method ensures temporal consistency without compromising important motion details. Additionally, STS-UVD demonstrates strong generalization across different noise conditions and datasets, making it a robust solution for medical video analysis. Extensive experiments validate its effectiveness in enhancing video quality while maintaining structural and temporal coherence.


## Architecture
<center>
<img src="./assets/pipeline.png" width="1000"/>
</center>

Given a noisy video sequence 
$$
\mathbf{I} \in\mathbb{R}^{T \times H \times W \times C}
$$
 where $$T,H,W$$ and $$C$$ are the video length, height, width and channel, respectively, the goal of STS-UVD is reconstruct a denoised video 
$$
\hat{\mathbf{I}} \in\mathbb{R}^{T \times H \times W \times C}
$$.
Our method takes two inputs: video contaminated with unknown noise distribution and the optical flow maps computed using neighboring noisy frames. We denote the input frame as 
$$
\{\mathbf{I}_t\}_1^T
$$, where $$T$$ is the total number of frames in the input video, and the initial optical flow maps as 
$$
\{\mathbf{F}_{t \rightarrow t + 1} \}
$$. 
Our weighted SpatioTemporal Sampling (STS) based unsupervised video denoising method utilizes the coarse 
$$
\{\mathbf{F}_{t \rightarrow t+ 1} \}
$$
 to determine the hyperparameters of the temporal sampling kernel $$\mathcal{T}$$. 
In each iteration, we concatenate each noisy frame $$\mathbf{I}_t$$ with its contiguous neighboring frames, denoted as $$\{\mathbf{I}_{t + i} \}_{-N/2}^{+N/2}$$.
These frames are first processed through a shallow feature extraction module $$G_{\phi}$$, consisting of three layers of group convolutions with 21 channels each, capturing essential low-level features.
Next, we apply the initialized temporal sampling kernel $$\mathcal{T}$$ to refine temporal information, followed by spatial sampling kernel $$\mathcal{S}$$, which enhances spatial consistency in the sampled batch. The resulting features are then passed through the denoising network to reconstruct the clean frame $$\hat{\mathbf{I}}_t$$.
After each epoch, we employ an optical flow consistency check to the denoised video and use the loss to update the network weights in the next round. This recurrent optimization will stop when the optical flow-based consistency loss does not change anymore. 

## Results
<!-- Two Photon Calcium Imaging | Fluorescence Microscopy
:-------------------------:|:-------------------------:
<img src="./assets/standard.gif" width="400"/> | <img src="./assets/GOWT1.gif" width="400"/>

 Two Photon Calcium Imaging           |  Fluorescence Microscopy
:-------------------------:|:-------------------------:
![](./assets/standard.gif)  |  ![](./assets/GOWT1.gif) -->

<!-- ## Video SuperResolution -->
<center>
<table style="border: none;">
 <tr style="border: none;"><th align="left" style="border: none;"> Fluorescence Microscopy </th></tr>
 <tr style="border: none;"><td align="left" style="border: none;"> <img src="./assets/msc_02.png" width="1000"/> </td></tr>
 <tr style="border: none;"><td align="left" style="border: none;"> <img src="./assets/gowt1.png" width="1000"/> </td></tr>
</table> 
 </center>

<!-- <table>
 <tr>
  <th align="center"> Two Photon Calcium Imaging </th>
  <th align="center"> Fluorescence Microscopy </th>
 </tr>
 <tr>
  <td align="center"> <img src="./assets/standard.gif" width="500"/> </td>
  <td align="center"> <img src="./assets/GOWT1.gif" width="500"/> </td>
 </tr>
</table> -->




<!-- ## Results on Natural Videos
<table style="border: none;">
 <tr style="border: none;"><th align="left" style="border: none;"> Bobblehead </th></tr>
 <tr style="border: none;"><td align="left" style="border: none;"> <img src="./assets/YTHFR_Gaussian50_bobblehead.gif" width="1000"/> </td></tr>
 <tr style="border: none;"><th align="left" style="border: none;"> Runner </th></tr>
 <tr style="border: none;"><td align="left" style="border: none;"> <img src="./assets/YTHFR_Gaussian50_1Runner.gif" width="1000"/> </td></tr>
</table> -->




![result](./assets/qual_results.png)

Quantitative comparison of our method with SOTA video denoising techniques on simulated two-photon calcium imaging datasets with varying fields of view (FOV). Text highlighted in **bold** signifies the highest value, while underlined text denotes the second highest..