<h1>Activity Recognition</h1>
<p>This repository contains the codebase for an advanced video analysis pipeline that combines the power of multiple state-of-the-art models and methodologies including YOLO V8, ByteTrack, Movenet, and Transformer encoders for high-accuracy activity recognition. The pipeline is trained on the Actitracker dataset provided by the WISDM Lab.</p>

<h2>Project Pipeline</h2>
<p>Below is a detailed description of each step in the pipeline:</p>

<h3>1. Frame Extraction</h3>
<p>In this step, individual frames are extracted from video input at different frame rates to obtain spatial and temporal features.</p>
<ul>
<li><b>Input</b>: Video frames</li>
<li><b>Action</b>: Frame extraction</li>
<li><b>Output</b>: Individual frames</li>
</ul>

<h3>2. ROI Extraction using YOLO and Subject Tracking</h3>
<p>The Region of Interest (ROI) is extracted using YOLO V8 for detecting the subject of interest in the first frame. Subsequently, the subject is tracked across the frames using a tracking algorithm such as DeepSort or ByteTrack.</p>
<ul>
<li><b>Input</b>: Individual frames</li>
<li><b>Action</b>:
<ul>
<li>Apply YOLO V8 for detecting the subject in the first frame</li>
<li>Track the subject across the frames using DeepSort or ByteTrack</li>
</ul>
</li>
<li><b>Output</b>: ROI images with consistent subject</li>
</ul>

<h3>3. Pose Estimation using Movenet</h3>
<p>Using the Movenet model, the pose of the subject is estimated from the ROI images.</p>
<ul>
<li><b>Input</b>: ROI images</li>
<li><b>Action</b>: Pose estimation using Movenet</li>
<li><b>Output</b>: Skeleton poses</li>
</ul>

<h3>4. Conversion of Skeleton Poses to Joint-Limb Skeleton Heatmap</h3>
<p>The skeleton poses obtained from Movenet are then converted to joint-limb skeleton heatmaps.</p>
<ul>
<li><b>Input</b>: Skeleton poses</li>
<li><b>Action</b>: Conversion to joint-limb skeleton heatmap</li>
<li><b>Output</b>: Joint-limb skeleton heatmaps</li>
</ul>

<h3>5. Feature Engineering</h3>
<p>The feature engineering stage consists of two streams - spatial and temporal feature extraction. The spatial stream operates on the ROI images and the temporal stream operates on the skeleton heatmaps. A Transformer encoder model is used in both streams with varying degrees of self-attention based on the frame rate.</p>

<h4>Spatial Feature Extraction Stream</h4>
<ul>
<li><b>Input</b>: ROI images</li>
<li><b>Action</b>: Apply Transformer encoder with fewer self-attention (lower frame rate)</li>
<li><b>Output</b>: Spatial features</li>
</ul>

<h4>Temporal Feature Extraction Stream</h4>
<ul>
<li><b>Input</b>: Joint-limb skeleton heatmaps</li>
<li><b>Action</b>: Apply Transformer encoder with more self-attention (higher frame rate)</li>
<li><b>Output</b>: Temporal features</li>
</ul>

<h3>6. Fusion of Spatial and Temporal Features</h3>
<p>The extracted spatial and temporal features are then fused together. This can be done either as an early fusion (before encoding and classification) or as a late fusion (after separate encoding and classification).</p>
<ul>
<li><b>Input</b>: Spatial features, Temporal features</li>
<li><b>Action</b>:
<ul>
<li>Early Fusion: Combine features before encoding and classification</li>
<li>Late Fusion: Encode features separately, generate individual classifications, and then fuse for final decision</li>
</ul>
</li>
<li><b>Output</b>: Combined features</li>
</ul>

<h3>7. Classification Model</h3>
<p>The final step of the pipeline involves using a classification model to predict the activity class based on the combined features.</p>
<ul>
<li><b>Input</b>: Combined features</li>
<li><b>Action</b>: Classification using a suitable model</li>
<li><b>Output</b>: Activity class</li>
</ul>

<h2>Dataset</h2>
<p>The model is trained on the Actitracker dataset by WISDM Lab.</p>
