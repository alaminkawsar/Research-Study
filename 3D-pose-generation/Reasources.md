# 3D-Pose-from-IMPU's sensor
![Ultra Inertial Poser: Scalable Motion Capture and Tracking from Sparse Inertial Sensors and Ultra-Wideband Ranging · Sensing, Perception & Interaction Lab](https://images.openai.com/static-rsc-4/NWdLWoURTmf-tSXDP8xTnJh4sVcH4NSQevrL9ZXJQ7r8NLMiJZAaHzgyv-aBRLEFVBm97noFyE4JZogfphSKymyVRt8jL-ZgDAp8vxtB6-6O_suYmVfW2mOEFJz8SjESDVl9ui6SRDK-IA05grswVFc9TY-ZQahxTfNoQHX27QnY6Qsrw3PP6wJ6KGhzlnUR?purpose=fullsize)

![NoahYacowar](https://images.openai.com/static-rsc-4/Nlyokmp7HSNiPZ0qs66lernniLCC1rkNPwQrOVTEQtuLa8d8wpN5xir4rHWyNqivJmV8JHo0lU8LpX2soclDK5KDIPGbKX2x5SvLPRZ692nV4JIMSqSkTacGVFOfsk9sWbb53j3yfxfZNChdjs-BNbrptwh67cpmZFSWhvbDGB3ykKKj2nkWelTHfu-ChG9V?purpose=fullsize)

![Best Mocap Full-Body Suit Manufacturer and Supplier | Virdyn](https://images.openai.com/static-rsc-4/JHd7rzWZcu5iK3o3W04XHTOXwbFzQZ89GuGuw1MjcE_wvL1l2pmLAldPawc0SKaGCHkVBbk7lhJgjORoK0Cd8Zwc_7O-vip86KEtwZqmeAOrOdVyOr9ZTnBGfMszvLlDvtVWtbKWeG0OYueF2UuN1Y0KSpbut6ThxSZwTBIGr5meNrh-tcsUdosCuyWppdFn?purpose=fullsize)

The key distinction is whether you want to visualize the activity or estimate the person's actual 3D body pose. The second is a much more interesting computer vision and machine learning problem.

### Three public datasets to start with

![DIP](https://images.openai.com/static-rsc-4/zaaIK3CqcDz-wIuD8AfaciPq_uezcXcvMpEZhgn76e8XviVGxbwIyRzmpE-n9ygHpEzatdqq_GdQrTmXsSq1a-obyxgUkVEb_yMTxQDfYjOwhwlJRofAm4dMKnfShfOulLMe4SK0trjcCaWsuVqzQLgOGVXZgSMa0YXLaSpy7n70wxaAb-QTMRAqErApRw7z?purpose=fullsize)

1\. DIP-IMU

Best starting point

Wearable IMU measurements paired with 3D motion-capture ground truth. Suitable for learning to reconstruct full-body pose from inertial signals.

[Dataset and download](https://dip.is.tuebingen.mpg.de/?utm_source=chatgpt.com) · [Research paper](https://doi.org/10.1109/ICCV.2017.336?utm_source=chatgpt.com)

![App rapidly gathers sophisticated movement data, at 1% of the usual cost](https://images.openai.com/static-rsc-4/734EYBqJKx-YtJWzEwPBLDs3jnRPGCOTG43tQKjy2y_slehTBvxivnUNPe_8oeNHlrPE5BGbQpe2a190UbHimxZ-hPgx2xQ1qXicVaIRwp9Rd0hlArUzjeHR7TpbwHQI7orJ290JvzXOcxf11NqyLJdVD7QIgNuSv3x9oT1obViyjRrxbPr2RwQ_-7s784hN?purpose=fullsize)

2\. TotalCapture

Combines synchronized multi-view video, wearable IMUs, and motion-capture ground truth. Particularly useful for comparing sensor-only and sensor-plus-vision approaches.

[Dataset and access](https://cvssp.org/data/totalcapture/?utm_source=chatgpt.com) · [Original paper](https://doi.org/10.1109/ICCV.2017.336?utm_source=chatgpt.com)

Access requires registration; check the research-only license.

![Vimal Mollyn](https://images.openai.com/static-rsc-4/2BI1LvyP4CPcxOVxTF3wYmH4uH3dCLlOoPpDNUffCipLEknaNghNeV-OtIFstk0Z1zy4kLQoZENCfHlq7hTB8E-BtUSz64ReBz5njyBHgGSEhvVqx16xZhWX9FEM0XPUCWs6zoe_q6m43IyIqqkWf_5dMhm2c-CTTBPqrKYEgd_leFu0mWURIo2pOxW8XvAJ?purpose=fullsize)

3\. IMUPoser

A useful option for investigating full-body pose reconstruction from a sparse arrangement of six IMUs.

[Dataset and research code](https://github.com/FIGLAB/IMUPoser?utm_source=chatgpt.com)

### What would you actually build?

### Wearable-to-3D Motion Reconstruction

Wearable sensor time series

Accelerometer + gyroscope + orientation

Temporal ML model

1D CNN / TCN / LSTM / Transformer

3D joint positions and rotations

Predicted skeleton for every time step

Animated 3D avatar

Visualize the reconstructed activity in a 3D viewer

### Where is the research opportunity?

Simply reproducing a 3D skeleton is already an established task. To make this a stronger research project, investigate one specific challenge:

* Sparse sensors: Can six or fewer IMUs reconstruct pose as accurately as a larger sensor setup?

* Sensor placement errors: Does the model still work when sensors are attached at slightly different angles or positions?

* Unseen activities: Can it reconstruct movements not represented in training?

* Long-term drift: Can you maintain stable global body movement over long sequences?

* Personalization: Can a model adapt to a new person's movement without extensive labeled data?

Sensor placement and calibration are particularly important real-world challenges; errors in attachment can degrade motion reconstruction.

My recommendation: Start with DIP-IMU, reproduce a baseline, and build a 3D animation pipeline. Then investigate robustness to sensor-placement errors or unseen subjects. Evaluate pose accuracy using MPJPE and joint-angle error, and separately assess temporal smoothness and generalization.

One important limitation: IMUs alone do not directly measure absolute position. They can estimate body pose and relative movement, but global translation and long-term drift require additional modeling or reference information.

12

12
