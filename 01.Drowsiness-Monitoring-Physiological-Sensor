# Towards Generalizable Drowsiness Monitoring with Physiological Sensors: A Preliminary Study (2025)

> **Paper:** https://arxiv.org/abs/2506.06360

## সারসংক্ষেপ

এই গবেষণার মূল উদ্দেশ্য ছিল বিভিন্ন পরিস্থিতিতে (যেমন ঘুমের অভাব, মানসিক ক্লান্তি, শারীরিক ক্লান্তি বা একঘেয়ে পরিবেশ) **কোন physiological signal গুলো ধারাবাহিকভাবে drowsiness নির্দেশ করে**, অর্থাৎ কোনগুলো নির্ভরযোগ্য **Digital Biomarker** হতে পারে তা খুঁজে বের করা।

গবেষণাটি নতুন কোনো Deep Learning মডেল তৈরির উপর নয়; বরং বিভিন্ন wearable sensor থেকে সংগৃহীত physiological data বিশ্লেষণ করে সাধারণভাবে কার্যকর biomarker শনাক্ত করার উপর গুরুত্ব দিয়েছে।

---

# গবেষণার উদ্দেশ্য

বর্তমান অধিকাংশ drowsiness detection গবেষণা নির্দিষ্ট একটি পরিস্থিতির জন্য তৈরি, যেমন Driving Drowsiness Detection।

কিন্তু বাস্তবে মানুষ শুধু গাড়ি চালানোর সময় নয়, বরং—

- ক্লাসে
- মিটিংয়ে
- অফিসে
- পড়াশোনার সময়
- টিভি দেখার সময়

এবং অন্যান্য দৈনন্দিন কাজের মধ্যেও doze off করতে পারে।

এই গবেষণার উদ্দেশ্য ছিল এমন physiological biomarker খুঁজে বের করা যা বিভিন্ন পরিস্থিতিতেই কার্যকর।

---

# ব্যবহৃত Physiological Signals

গবেষণায় তিন ধরনের wearable-friendly signal ব্যবহার করা হয়েছে।

## ECG (Electrocardiogram)

ECG থেকে বিশ্লেষণ করা হয়েছে—

- Heart Rate (HR)
- Heart Rate Variability (HRV)

---

## EDA (Electrodermal Activity)

EDA দ্বারা পরিমাপ করা হয়েছে—

- Skin Conductance
- Tonic EDA
- Phasic EDA

---

## Respiration (RESP)

Respiration signal থেকে নেওয়া হয়েছে—

- Respiratory Rate
- Respiratory Amplitude
- Respiratory Variability

---

# ব্যবহৃত Dataset

একটি নয়, মোট চার ধরনের Dataset ব্যবহার করা হয়েছে।

| Dataset | Drowsiness এর কারণ |
|----------|---------------------|
| Physical Fatigue | শারীরিক ক্লান্তি |
| Mental Fatigue | মানসিক ক্লান্তি |
| Low Arousal | একঘেয়ে পরিবেশ |
| Sleep Deprivation | ঘুমের অভাব |

এর ফলে গবেষকরা বিভিন্ন ধরনের drowsiness একসাথে বিশ্লেষণ করতে পেরেছেন।

---

# Drowsiness Label

দুই ধরনের Label ব্যবহার করা হয়েছে।

## Subjective Label

Participant নিজে তার ঘুম ঘুম লাগার মাত্রা জানিয়েছে।

উদাহরণ:

- Karolinska Sleepiness Scale (KSS)

### সীমাবদ্ধতা

- ব্যক্তি নিজে সবসময় সঠিকভাবে নিজের drowsiness বুঝতে পারে না।

---

## Objective Label

দৃষ্টিগ্রাহ্য আচরণ বা physiological measurement এর ভিত্তিতে drowsiness নির্ধারণ করা হয়েছে।

গবেষণায় দেখা গেছে Objective Label বেশি নির্ভরযোগ্য।

---

# Methodology

এই গবেষণায় Deep Learning ব্যবহার করা হয়নি।

বরং **Binary Logistic Regression** ব্যবহার করে দেখা হয়েছে কোন physiological feature-এর সাথে drowsiness-এর সবচেয়ে শক্তিশালী সম্পর্ক রয়েছে।

মূল লক্ষ্য ছিল **Digital Biomarker শনাক্ত করা**, classifier তৈরি করা নয়।

---

# প্রধান ফলাফল

গবেষণায় তিনটি biomarker সবচেয়ে গুরুত্বপূর্ণ হিসেবে পাওয়া গেছে।

## 1. Heart Activity

বিশেষ করে

- Heart Rate
- Heart Rate Variability (HRV)

drowsiness-এর সাথে ধারাবাহিক সম্পর্ক দেখিয়েছে।

---

## 2. Respiratory Amplitude

ঘুম ঘুম ভাব বাড়লে

- শ্বাস ধীরে হয়
- শ্বাস অগভীর হয়

অর্থাৎ Respiratory Amplitude কমে যায়।

---

## 3. Tonic EDA

Drowsiness বাড়ার সাথে সাথে

- Skin Conductance কমে যায়
- Sympathetic Nervous System-এর কার্যকলাপও কমে যায়

---

# গুরুত্বপূর্ণ পর্যবেক্ষণ

সব ধরনের drowsiness একই রকম নয়।

উদাহরণস্বরূপ—

- Sleep deprivation
- Mental fatigue
- Physical fatigue
- Low arousal

প্রতিটির physiological response কিছুটা ভিন্ন।

অর্থাৎ একটি মাত্র biomarker দিয়ে সব ধরনের drowsiness শনাক্ত করা কঠিন।

---

# গবেষণার সীমাবদ্ধতা

- পূর্বের Dataset ব্যবহার করা হয়েছে।
- অধিকাংশ Data Laboratory Environment-এ সংগ্রহ করা।
- বিভিন্ন Dataset-এর Protocol এক ছিল না।
- বাস্তব জীবনে আরও Validation প্রয়োজন।

---

# এই গবেষণা থেকে শেখা বিষয়

এই গবেষণা অনুযায়ী wearable device ব্যবহার করে নিচের biomarker গুলো সবচেয়ে সম্ভাবনাময়—

- ❤️ Heart Rate (HR)
- ❤️ Heart Rate Variability (HRV)
- 🌡️ Electrodermal Activity (EDA)
- 🫁 Respiratory Amplitude

---

# আমার গবেষণার সাথে সম্পর্ক

আমার গবেষণার লক্ষ্য শুধুমাত্র **Driving Drowsiness Detection** নয়।

বরং এমন একটি Wearable-based Dozing Off Detection System তৈরি করা যা—

- Meeting
- Classroom
- Office
- Watching TV
- Studying
- Reading

সহ দৈনন্দিন বিভিন্ন পরিস্থিতিতে মানুষের **Dozing Off** শনাক্ত করতে পারে।

এই পেপারটি দেখায় যে শুধুমাত্র একটি পরিস্থিতির উপর নির্ভর না করে **Generalizable Digital Biomarker** নির্বাচন করা ভবিষ্যতের wearable drowsiness detection system তৈরির জন্য অত্যন্ত গুরুত্বপূর্ণ।

---

# Key Takeaway

> **এই গবেষণার মূল অবদান হলো—একটি নতুন AI model তৈরি করা নয়; বরং বিভিন্ন পরিস্থিতিতে ধারাবাহিকভাবে কার্যকর physiological Digital Biomarker শনাক্ত করা, যা ভবিষ্যতে বাস্তব জীবনের wearable-based dozing-off detection system তৈরির ভিত্তি হতে পারে।**
