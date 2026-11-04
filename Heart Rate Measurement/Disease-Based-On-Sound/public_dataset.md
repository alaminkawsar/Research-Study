I found several resources that are particularly relevant to your research. The strongest options are BMD-HS and the 2025 Heart Sound Regurgitation Dataset because they provide disease-specific WAV recordings rather than only normal/abnormal labels.

### 1\. Best datasets and direct download links

1\. BMD-HS Dataset

Top priority

![Explainable attention-based deep learning for classification and interpretation of heart murmurs using phonocardiograms | Scientific Reports](https://images.openai.com/static-rsc-4/8k8vqPk850k4kVieE_CdzChjpoBxmMgH2BgD27pzjqpz4t_BVIJSTv54oNkL3z_ONb_xR9d9JUyHpGCu3tOZ1_6VHp8wwNuTUeqA9WfI641QLtmFOznQ6RBVhrYZzMiYutS38sihIkYtNLT9q33Yjcoc0_Z3y43GBJ5WQTUPhPtM-Y_FwgLrUfkFZOfO_roW?purpose=fullsize)

Bangladesh – National Institute of Cardiovascular Diseases

* 872 WAV recordings.

* 59 patients, eight recording positions.

* 4 kHz sampling rate; 20 seconds per recording.

* Labels: AS, AR, MR, MS, multi-disease, normal.

* Patient-level CSV annotations.

[Download BMD-HS on GitHub](https://github.com/sani002/BMD-HS-Dataset?utm_source=chatgpt.com)[Read research paper](https://arxiv.org/abs/2409.00724?utm_source=chatgpt.com)

2\. Heart Sound Regurgitation Dataset (2025)

Top priority

* WAV recordings.

* Labels: Aortic regurgitation, mitral regurgitation, tricuspid regurgitation, normal.

* Echocardiography-supported clinical diagnoses.

* Includes disease severity metadata.

[Direct Mendeley Data download](https://data.mendeley.com/datasets/jfbdvjw6sf/1?utm_source=chatgpt.com)[Read research paper](https://doi.org/10.1016/j.dib.2025.112081?utm_source=chatgpt.com)

3\. CirCor DigiScope

* Pediatric heart sounds.

* WAV recordings and CSV annotations.

* Murmur characteristics and clinical outcomes.

[Download from PhysioNet](https://physionet.org/content/circor-heart-sound/1.0.1/?utm_source=chatgpt.com)[Read research paper](https://doi.org/10.1109/JBHI.2021.3137048?utm_source=chatgpt.com)

4\. PhysioNet Challenge 2016

* WAV recordings, 2 kHz.

* Normal, abnormal, and unsure.

* Useful for binary classification, not disease-specific training.

[Download dataset](https://physionet.org/content/challenge-2016/1.0.0/?utm_source=chatgpt.com)[Read research paper](https://doi.org/10.1088/0967-3334/37/12/2181?utm_source=chatgpt.com)

### 2\. Resources for ASD, VSD and PDA

These are harder to find as research-grade WAV datasets.

| Disease | Additional resource         |
| ------- | --------------------------- |
| ASD     | Teaching Heart Auscultation |
| VSD     | Teaching Heart Auscultation |
| PDA     | Teaching Heart Auscultation |

[Download congenital heart disease sound examples](https://teachingheartauscultation.com/heart-sounds-mp3-downloads?utm_source=chatgpt.com)MP3, not WAV

These are teaching recordings, not a large clinically labelled research cohort. Also, I could not independently verify the previously mentioned CHD-HSY dataset's primary download source, so I have not treated it as a confirmed resource.

### 3\. Your README file

heart_sound_disease_dataset_resources_README.md

Markdown file · Research resource collection

Created

Download your README.md file

It contains:

* Dataset names and download links.

* Disease categories and audio formats.

* Research paper references.

* Dataset comparison table.

* Suggested project directory structure.

* Data preprocessing and model evaluation recommendations.

* Important notes about dataset licenses and clinical labels.

### 4\. My suggested research direction

I would organize your project around these disease classes:

| Category   | Disease                 |
| ---------- | ----------------------- |
| Normal     | Healthy                 |
| Congenital | ASD                     |
| Congenital | VSD                     |
| Congenital | PDA                     |
| Valvular   | Aortic stenosis         |
| Valvular   | Aortic regurgitation    |
| Valvular   | Mitral stenosis         |
| Valvular   | Mitral regurgitation    |
| Valvular   | Tricuspid regurgitation |

Not all these classes currently have verified WAV datasets in the resources above. You will need additional clinically labelled recordings for ASD, VSD and PDA.

One important recommendation: Use patient-level train/test splitting, not recording-level splitting. Otherwise, multiple recordings from the same patient could leak into both training and testing, producing misleading accuracy.

Your best starting combination is BMD-HS + the 2025 Regurgitation Dataset + CirCor.
