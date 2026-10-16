### Two useful follow-up courses

![Building a Loan Default Prediction Model — A Step‑by‑Step Walkthrough | by Angelaekele | Medium](https://images.openai.com/static-rsc-4/KwIbAQbefMbKncDhbm9JGDKPotCSiGu4e21I39oPEOctFqEOkoHZJiLQq_8i62NhNB5Fis71bndtgzoPFUvxbvRYcLOU1HGn3wYwFZ4M6ZvCEoY5P4Op3mGXbCPf6dX-G2ubbCvfXT4ZITGF0bCT6Cv-1DtMJtxajk6KnTrIrJ0uxugHeyVk0-az1wm16UhE?purpose=fullsize)

6\. Feature Engineering for Machine Learning

4.6/5 · About 3,800 ratings in the retrieved listing

Useful after you extract PPG features, to learn missing-value handling, outlier treatment, feature transformations, and preparation for machine learning.

[View course on Udemy](https://www.udemy.com/course/feature-engineering-for-machine-learning/?utm_source=chatgpt.com)

!["Learn Machine Learning for Neuroscience with Python" | Ildar Rakhmatulin posted on the topic | LinkedIn](https://images.openai.com/static-rsc-4/_xgz4LxlehFfCTMRKBbcyQio_h5cgQbe04bTl5ykZUBYknbCCM7VslDj_53rYT1K2mPgus1vobhLAyw8XGGTMUNzJskqjWwD61N7DXzH9GxjWF-sIzd3gCCCeMEHszNikKfnPYAHPD-gX5WtK54VXdeGr5Yp4gGBe2mBl3HEJefMold8Wo5y6ede8f-cCw7i?purpose=fullsize)

7\. Machine Learning (Python) for Neuroscience Practical course

Teaches dataset preparation, signal feature extraction, and machine-learning workflows using EEG data. The signal is different from PPG, but many data-analysis techniques transfer.

[View course on Udemy](https://www.udemy.com/course/machine-learning-python-for-neuroscience-practical-course/?utm_source=chatgpt.com)

### The learning path I'd choose for you

Given your Galaxy Watch and biomarker research goal, I would not buy all seven courses. Start with this sequence:

* Digital signal processing: Signal processing problems, solved in MATLAB and in Python.

* Biomedical applications: Biomedical Signal Processing.

* Feature engineering: Feature Engineering for Machine Learning.

* Practical project: Apply what you learn to real PPG data using Python, SciPy, and NeuroKit2.

* Machine learning: Start with regression and leakage-safe validation after you have a reliable feature table.

One thing to keep in mind: I couldn't identify a Udemy course that comprehensively teaches Samsung Galaxy Watch raw PPG access plus glucose-biomarker feature discovery. The best route is to combine DSP and biomedical-signal courses with Samsung's official SDK documentation and your own experiments.

Your first project should be modest: obtain a raw PPG recording, filter it, detect pulse peaks, extract 5–10 features, and test whether those features are repeatable. That will give you a solid foundation for the more exciting biomarker research later.
