Here is a more complete resource collection for 3D human motion reconstruction from wearable IMUs, organized around datasets, papers, open-source implementations, and the tools needed to turn predicted poses into an animated 3D human.

### 1\. Essential datasets

![DIP](https://images.openai.com/static-rsc-4/zaaIK3CqcDz-wIuD8AfaciPq_uezcXcvMpEZhgn76e8XviVGxbwIyRzmpE-n9ygHpEzatdqq_GdQrTmXsSq1a-obyxgUkVEb_yMTxQDfYjOwhwlJRofAm4dMKnfShfOulLMe4SK0trjcCaWsuVqzQLgOGVXZgSMa0YXLaSpy7n70wxaAb-QTMRAqErApRw7z?purpose=fullsize)

DIP-IMU — sparse inertial pose estimation

A classic starting benchmark with IMU measurements and reference poses. Useful for reproducing an established method and evaluating unseen-subject generalization.

[Official dataset and paper](https://dip.is.tuebingen.mpg.de/?utm_source=chatgpt.com)

![Real-Time Multi-person Motion Capture from Multi-view Video and IMUs | International Journal of Computer Vision | Springer Nature Link](https://images.openai.com/static-rsc-4/mZ9Lx-ddkEQxawxugZWLJZv0z7bQVoZMDEAE2FPRB9N3u6poJG3n4vI7VeoOrdF5dimANtDMLmFQKrqxN2CWPwgELL7o1BhQI_1vuJVKO9ekeRMGVArZZxwU1N3AvAOkMCG-GG6Dhh7eWCkCyD0sm-9L3P1hAde_Lr2SDQcqDbWRgrbrKacivOyA8IlQ2Tyt?purpose=fullsize)

TotalCapture — sensors plus video

Synchronized video, IMUs, and Vicon motion-capture labels. Particularly useful for comparing sensor-only reconstruction with multimodal methods.

[Official dataset](https://cvssp.org/data/totalcapture/?utm_source=chatgpt.com)

Registration and research-use restrictions apply.

![iPhoneとApple WatchとAirPodsでVRにダイブできる？ | ギズモード・ジャパン](https://images.openai.com/static-rsc-4/Q3pchz_j4UiqnKA8KaT6HQx8VEpBawwuZXTN_Q-zQVkrNVvOpGv0RCYn3k7EmXQeoyr786-dDiqCnmDRhetL85C6B-GW7JhwqYuBqBFQ2kf-F8w0Lue7d8bay_ic3SBW5ofZv5hoU4ceZpCpRdviqjJaWgWEh5gwB-v_sFFs2cP2ZmCQJiCKXi5pyLj3YOL0?purpose=fullsize)

IMUPoser — sparse wearable sensing

Focuses on reconstructing full-body movement from a small number of IMUs, closer to practical wearable configurations.

[Official research repository](https://github.com/FIGLAB/IMUPoser?utm_source=chatgpt.com)

![精读AMASS论文解析MoSh++方法统一动捕数据集-开发者社区-阿里云](https://images.openai.com/static-rsc-4/ufQ8jw17NK_CYKbHAEIF8VGQjWejuGYB3j-0Qzvrrslk-8LpEVDETmjWWLRRTp-67o1qnb8MbW5A7pwMw193PyqukKjCdESH8SAR_GY0Y2FrhuFt2OJtkEMeiXjidbOOaFDDRF30-sHY20-Q18t-L1l1FuLO5yRhCiFJGH2wtR-KG64KkC8ncHeKobFe5QJe?purpose=fullsize)

AMASS — large-scale 3D motion data

A collection of motion-capture datasets represented using a common SMPL-family body model. Excellent for pretraining and generating synthetic sensor inputs.

[Official dataset](https://amass.is.tue.mpg.de/?utm_source=chatgpt.com)

AMASS primarily supplies motion-capture data, not measured IMU signals for every sequence.

### 2\. Research papers to read

Read these in order, from the foundational problem to more advanced research directions.

### 1\. Deep Inertial Poser (DIP), SIGGRAPH Asia 2018

Start here · Foundational paper

Deep Inertial Poser: Learning to Reconstruct Human Pose from Sparse Inertial Measurements in Real Time

Explains how to estimate full-body pose from sparse IMU signals with a learned temporal model.

[Paper, dataset, and project page](https://dip.is.tuebingen.mpg.de/?utm_source=chatgpt.com)

### 2\. 3D Human Pose Estimation from Sparse IMUs through Temporal Encoder and Regression Decoder

Architecture and temporal modeling

Studies temporal encoding and hierarchical regression using human skeletal structure.

[Full paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC10098669/?utm_source=chatgpt.com)

### 3\. Fast Human Motion Reconstruction from Sparse IMUs Considering the Human Shape

Body shape and motion reconstruction

Useful for investigating whether modeling body shape improves reconstructed motion.

[Full paper](https://pmc.ncbi.nlm.nih.gov/articles/PMC10948800/?utm_source=chatgpt.com)

### 4\. Ultra Inertial Poser (2024)

Advanced · Drift reduction

Combines sparse IMUs with ultra-wideband ranging to improve position tracking and reduce motion jitter.

[Paper](https://arxiv.org/abs/2404.19541?utm_source=chatgpt.com)

### 5\. IMUCoCo (UIST 2025)

Advanced · Flexible sensor placement

Investigates pose estimation and activity recognition with more flexible IMU placement configurations.

[Research code and checkpoints](https://github.com/cmusmashlab/IMUCoCo?utm_source=chatgpt.com)

### 6\. Lightweight wearable IMU human pose estimation (2026)

Recent research · Efficient deployment

Explores knowledge distillation and lightweight architectures for low-latency pose estimation.

[Open-access paper](https://www.nature.com/articles/s41598-026-41004-5?utm_source=chatgpt.com)

### 3\. Open-source code you can run

These repositories help bridge the gap between reading a paper and building a working reconstruction system.

MobilePoser

Full-body pose estimation and 3D translation from IMUs on mobile consumer devices. A useful reference for an end-to-end implementation.

[GitHub repository](https://github.com/SPICExLAB/MobilePoser?utm_source=chatgpt.com)

Sparse IMU design-space exploration

An implementation exploring the trade-off between accuracy, sensor configurations, and efficiency.

[GitHub repository](https://github.com/itiv-kit/dse-sparse-imu?utm_source=chatgpt.com)

SMPL body model

A parametric 3D human body representation that converts pose and shape parameters into a mesh. This is useful when you want a realistic avatar rather than only joint coordinates.

[SMPL project](https://smpl.is.tue.mpg.de/?utm_source=chatgpt.com)

### 4\. Tools for the 3D visualization pipeline

![Creating an Avatar | MSquared Docs](https://images.openai.com/static-rsc-4/rIKf1iPONWwQb-4Zkz7yAv9tJRYkIc7MIAsNVbslNMzkUOuUnJYs1dSAumHbt1o19S4zNDdJ90rU0yHx2eXqdRc-YQP8G2uV3lNFfCU1lUt2VvuGo1qT9Y1TV9kqKQp5ydpaHtkDmSgKVOqwiTlwTdDJIvo0R7JPG5OL4I7fLAZu_969k0j9JF-B83wzFxoS?purpose=fullsize)

Blender

Use for rigging a human avatar, animating joint rotations, and exporting rendered motion sequences.

[blender.org](https://www.blender.org/?utm_source=chatgpt.com)

![WebGL Skeletal Animation](https://images.openai.com/static-rsc-4/wHenmUJ7TRjKf7bSVlQqZZznKe8jmjs7omdg2i0yb6Q2Yb3OStcsveJZF4tIPqYCHjW9hb6GZLV4AUE-r7u5D5Qa0CZqnOUXfY6D8y7LsezvWcTi2OBMtEEIhfgO-9QWeFq9ghrD2apoWdX54jfoVEAzzbntFuAtInZfqmOKxyEnEH1u3_AIKUUyRowVyP_p?purpose=fullsize)

Three.js

Use for building an interactive browser-based 3D viewer with joint controls, playback, and synchronized sensor plots.

[threejs.org](https://threejs.org/?utm_source=chatgpt.com)

![The story of SMPL. In the summer of 2014 I was the one… | by Naureen Mahmood | Meshcapade | Medium](https://images.openai.com/static-rsc-4/v8n9lhjbTbdJtt3VXIUu-JWEDMg0RNexwehBUdy1PGwl_yPp3DYXD0xCWBV-TFprXYdQXAtOTG4uMAequ5fbb2x8JZ_3O9HGN6cGXGEiSgG3BmdscjCP6AgJikGaqafFHBIWlyNiLjaTLIyn2DworkpexIj-z1MXgssAZ-iAc8lNM1xzVGfXOtpQMXUKR-3Q?purpose=fullsize)

SMPL body models

Useful for converting predicted skeletal poses into a consistent human mesh. Review model access and licensing before use.

### 5\. A practical roadmap

For your background, I would follow this sequence:

* Reproduce DIP. Understand IMU orientation, acceleration, coordinate systems, and the pose output representation.

* Build a 3D viewer. Animate predicted joint positions or rotations using Blender or Three.js.

* Establish a subject-independent baseline. Make sure test subjects do not appear in training data.

* Test sparse sensing. Compare different sensor subsets and quantify the accuracy lost when sensors are removed.

* Investigate one research question. My preferred options are flexible sensor placement, unseen-activity generalization, or temporal stability and drift.

For evaluation, track MPJPE (mean per-joint position error), joint-angle error, and temporal jerk. If you estimate global translation, evaluate trajectory drift separately. A smooth animation alone is not evidence of accurate reconstruction.

Best starting combination: DIP-IMU + the DIP paper + MobilePoser + a Blender viewer. This gives you a full path from raw wearable signals to an animated 3D human, with a reproducible baseline for further research.
