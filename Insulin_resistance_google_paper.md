# Wearables ও Routine Blood Biomarkers দিয়ে Insulin Resistance Prediction

*Google Research — ৬ আগস্ট ২০২৫*

*Ahmed A. Metwally, Staff Research Scientist
A. Ali Heydari, Research Scientist
Google Research*

Google Research এমন একটি নতুন method নিয়ে গবেষণা করেছে, যেখানে wearable devices-এর data এবং routine blood tests ব্যবহার করে একজন মানুষের insulin resistance (IR) predict করার চেষ্টা করা হয়েছে।

এর মূল উদ্দেশ্য হলো—যে data অনেক মানুষের কাছেই আগে থেকেই available, যেমন smartwatch/fitness tracker-এর data এবং সাধারণ blood test-এর result, সেগুলো ব্যবহার করে type 2 diabetes-এর risk আগেভাগে শনাক্ত করা যায় কি না তা দেখা।

এই গবেষণাটি Nature-এ প্রকাশিত হয়েছে।

গবেষণায় দেখা গেছে, এই approach overall study population এবং একটি independent validation cohort—দুই জায়গাতেই insulin resistance predict করতে ভালো performance দেখিয়েছে। বিশেষ করে obesity এবং sedentary lifestyle-এর মতো high-risk group-এ performance আরও ভালো ছিল।

এছাড়া researchers Insulin Resistance Literacy and Understanding Agent, সংক্ষেপে একটি IR prototype agent, তৈরি করেছেন। এটি Gemini family-এর LLM ব্যবহার করে মানুষের insulin resistance সম্পর্কে বোঝার সুবিধা এবং personalized educational information দেওয়ার উদ্দেশ্যে তৈরি।

তবে এই model, prediction এবং IR Agent শুধু informational এবং research purposes-এর জন্য তৈরি; এগুলো medical diagnosis বা approved medical solution নয়।

---

প্রথমে বুঝি: **Insulin Resistance কী?**

Insulin হলো এমন একটি hormone যা blood glucose regulate করতে গুরুত্বপূর্ণ ভূমিকা রাখে।

স্বাভাবিক অবস্থায় insulin শরীরের cells-কে glucose ব্যবহার বা store করতে সাহায্য করে।

কিন্তু insulin resistance হলে শরীরের cells insulin-এর signal-এ আগের মতো ভালোভাবে respond করে না।

ফলে একই কাজ করার জন্য শরীরকে আরও বেশি insulin তৈরি করতে হতে পারে এবং সময়ের সঙ্গে metabolic সমস্যা তৈরি হতে পারে।

Chronic insulin resistance প্রায় 70% type 2 diabetes case-এর precursor হিসেবে উল্লেখ করা হয়েছে।

এটি সাধারণত একাধিক factor-এর combination-এর সঙ্গে সম্পর্কিত, যেমন:

- obesity
- inactive বা sedentary lifestyle
- genetic factors

তাই insulin resistance যদি early stage-এ detect করা যায়, তাহলে lifestyle পরিবর্তনের মাধ্যমে এটি অনেক ক্ষেত্রে reverse করা এবং type 2 diabetes-এর onset prevent বা delay করা সম্ভব হতে পারে।

---

সমস্যা কোথায়?

Insulin resistance accurately measure করার কিছু established method আছে।

এর মধ্যে একটি হলো euglycemic insulin clamp, যেটিকে insulin sensitivity measurement-এর “gold standard” হিসেবে ধরা হয়।

আরেকটি বহুল ব্যবহৃত measure হলো HOMA-IR (Homeostatic Model Assessment of Insulin Resistance)।

কিন্তু HOMA-IR বের করার জন্য specific insulin blood test প্রয়োজন।

এই ধরনের testing-এর সমস্যা হলো এগুলো হতে পারে:

- invasive
- expensive
- routine check-up-এ সবসময় available নয়

ফলে অনেক মানুষ insulin resistant হয়ে থাকলেও তারা সেটা জানেন না।

এখানেই researchers-এর প্রশ্ন:

«যে data মানুষের কাছে আগে থেকেই আছে—যেমন wearable data এবং common blood tests—সেগুলো ব্যবহার করে কি insulin resistance-এর risk estimate করা যায়?»

---

**Wearable data দিয়ে কী বোঝা যায়?**

বর্তমান wearable devices অনেক ধরনের physiological এবং lifestyle-related signal collect করতে পারে।

যেমন:

- resting heart rate
- step count
- sleep patterns
- activity-related information

এই research-এ Fitbit এবং Google Pixel Watch-এর মতো device থেকে পাওয়া data ব্যবহার করা হয়েছে।

Researchers-এর idea হলো, এই ধরনের digital signals-এর মধ্যে মানুষের lifestyle এবং metabolic health সম্পর্কে useful information থাকতে পারে।

এর সঙ্গে যদি routine blood test-এর information যোগ করা যায়, তাহলে insulin resistance predict করার জন্য আরও comprehensive picture পাওয়া যেতে পারে।

---

WEAR-ME Study

এই idea পরীক্ষা করার জন্য researchers একটি study design করেন, যার নাম WEAR-ME।

এখানে লক্ষ্য ছিল readily accessible data ব্যবহার করে HOMA-IR predict করা।

Routine blood biomarker data collection automate করার জন্য Google Quest Diagnostics-এর সঙ্গে partnership করে।

Study-তে মোট 1,165 remote participants US-এর বিভিন্ন জায়গা থেকে অংশগ্রহণ করেন।

তারা Google Health Studies app-এর মাধ্যমে study-তে enrol করেন।

Google Health Studies হলো digital studies-এর জন্য একটি secure consumer-facing platform।

Study-টি একটি Institutional Review Board (IRB)-এর approval নিয়ে করা হয়েছিল।

Enrollment-এর আগে প্রত্যেক participant Google Health Studies app-এর মাধ্যমে:

- electronic informed consent
- এবং specific HIPAA Authorization

দিয়েছিলেন।

---

**Participants কেমন ছিলেন?**

Study cohort বয়স, gender, geography এবং BMI-এর দিক থেকে diverse ছিল।

Participants-এর:

- Median BMI: 28 kg/m²
- Median age: 45 years
- Median HbA1c: 5.4%

ছিল।

Participants consent করেছিলেন নিচের data share করার জন্য।

---

১. Wearable Data

Participants-এর Fitbit অথবা Google Pixel Watch থেকে data নেওয়া হয়।

এর মধ্যে ছিল:

- resting heart rate
- step count
- sleep patterns
- অন্যান্য wearable-derived information

Individual privacy protect করার জন্য wearable data pseudonymized করা হয়েছিল।

অর্থাৎ researchers-এর analysis-এর জন্য data এমনভাবে process করা হয়েছিল যাতে সরাসরি participant identity-এর সঙ্গে data যুক্ত না থাকে।

---

২. Routine Blood Biomarkers

Participants-এর in-person visit-এর সময় Quest Diagnostics-এ routine blood tests করা হয়।

Research-এর জন্য specificভাবে test order করা হয়েছিল।

এর মধ্যে ছিল:

- fasting glucose
- fasting insulin
- lipid panel
- অন্যান্য routine blood biomarker

এই blood data ব্যবহার করে HOMA-IR এবং insulin resistance-এর সঙ্গে সম্পর্কিত information পাওয়া যায়।

---

৩. Demographics এবং Surveys

Participants study-এর শুরু এবং শেষে basic information ও health questionnaire পূরণ করেছিলেন।

এর মধ্যে ছিল:

- age
- weight
- height
- ethnicity
- race
- gender
- overall health সম্পর্কে perception
- fitness
- diet
- diabetes-এর history
- অন্যান্য comorbidity-এর history

অর্থাৎ researchers-এর কাছে wearable + blood biomarker + demographic + survey—এই কয়েক ধরনের information একসঙ্গে ছিল।

এই পুরো multimodal dataset-কে researchers “WEAR-ME data” বলেছেন।

---

এরপর Machine Learning Model তৈরি করা হলো

এই rich multimodal dataset ব্যবহার করে researchers deep neural network models develop এবং train করেন।

Model-এর লক্ষ্য ছিল:

Available data → HOMA-IR score predict করা

Researchers বিভিন্ন combination of input data ব্যবহার করে দেখতে চেয়েছেন:

«কোন ধরনের information একসঙ্গে ব্যবহার করলে insulin resistance prediction সবচেয়ে ভালো হয়?»

এখানে একটি গুরুত্বপূর্ণ বিষয় হলো, তারা শুধু prediction score বের করেননি; বরং model কোন features-কে বেশি গুরুত্ব দিচ্ছে সেটাও investigate করেছেন।

---

Results: শুধু Wearables কি যথেষ্ট?

Researchers prediction performance measure করতে area under the receiver operating characteristic curve (auROC) ব্যবহার করেছেন।

প্রথমে শুধু wearable এবং demographic information ব্যবহার করা হয়।

Wearables + Demographics

এই combination insulin resistance classify করার ক্ষেত্রে কিছু predictive power দেখিয়েছে।

auROC = 0.70

অর্থাৎ wearable data-তে সত্যিই insulin resistance সম্পর্কে useful signal ছিল।

---

Fasting Glucose যোগ করলে কী হলো?

এরপর wearable + demographic data-এর সঙ্গে fasting glucose যোগ করা হয়।

এতে performance উল্লেখযোগ্যভাবে improve করে।

Wearables + Demographics + Fasting Glucose

auROC = 0.78

অর্থাৎ একটি সাধারণ routine blood test—fasting glucose—model-এর prediction capability-তে significant improvement এনেছে।

---

সব Routine Blood Panel যোগ করলে

শেষে wearable data, demographics এবং routine blood panel—সব একসঙ্গে ব্যবহার করা হয়।

এতে researchers সবচেয়ে ভালো overall results পান।

HOMA-IR value prediction

R² = 0.50

অর্থাৎ model HOMA-IR-এর variation-এর একটি substantial অংশ explain/predict করতে পেরেছে।

Insulin Resistance classification

auROC = 0.80

এখানে:

- Sensitivity = 76%
- Specificity = 84%

ছিল।

এই classification-এর ক্ষেত্রে HOMA-IR ≥ 2.9 হলে participant-কে insulin resistant হিসেবে identify করা হয়েছিল।

---

Sensitivity এবং Specificity মানে কী?

এখানে দুটি metric খুব গুরুত্বপূর্ণ।

Sensitivity = 76%

যারা সত্যিই insulin resistant, তাদের মধ্যে model প্রায় 76%-কে identify করতে পেরেছে।

Specificity = 84%

যারা insulin resistant নয়, তাদের মধ্যে প্রায় 84%-কে model correctly non-resistant হিসেবে identify করতে পেরেছে।

এগুলো population-level research metrics—কোনো individual মানুষের diagnosis নিশ্চিত করার guarantee নয়।

---

Model কোন features-কে সবচেয়ে গুরুত্বপূর্ণ মনে করেছে?

Researchers model-এর feature importance-ও দেখেছেন।

Interesting বিষয় হলো, wearable data থেকে পাওয়া resting heart rate consistently গুরুত্বপূর্ণ predictor-গুলোর মধ্যে ছিল।

এর পাশাপাশি:

- BMI
- fasting glucose

এগুলোও গুরুত্বপূর্ণ predictor ছিল।

এখানে researchers-এর interpretation হলো, wearable থেকে পাওয়া lifestyle-related signals insulin resistance prediction-এর জন্য potentially valuable information বহন করে।

অর্থাৎ শুধু blood test নয়—মানুষের দৈনন্দিন physiological এবং lifestyle pattern-ও useful হতে পারে।

---

SHAP দিয়ে Feature Importance দেখা

Researchers nonlinear XGBoost models-এর জন্য SHAP (SHapley Additive exPlanations) values ব্যবহার করে feature importance analyse করেছেন।

এটি এমন একটি method যার মাধ্যমে বোঝার চেষ্টা করা যায় কোন feature model-এর prediction-এ কতটা contribution করছে।

তাদের analysis-এ বিভিন্ন feature-এর relative importance visualise করা হয়েছে একটি Sankey diagram দিয়ে।

এতে wearable-derived signals, BMI এবং blood biomarkers-এর contribution দেখা যায়।

---

High-Risk Group-এ কী হলো?

Researchers বিশেষভাবে এমন মানুষদের নিয়ে interested ছিলেন যাদের type 2 diabetes develop করার risk বেশি হতে পারে।

বিশেষ করে:

- obese participants
- sedentary participants
- যারা একই সঙ্গে obese এবং sedentary

এই subgroup-গুলো আলাদাভাবে evaluate করা হয়।

---

Obese Participants

Obese participants-এর ক্ষেত্রে model-এর performance overall population-এর তুলনায় improved ছিল।

Sensitivity:

86% বনাম overall 76%

অর্থাৎ এই subgroup-এ সত্যিকারের insulin-resistant participants-দের আরও বড় proportion model identify করতে পেরেছে।

---

Sedentary Participants

Sedentary participants-এর ক্ষেত্রে sensitivity আরও বেশি ছিল।

Sensitivity = 88%

অর্থাৎ এই group-এ model insulin-resistant individuals identify করার ক্ষেত্রে 88% sensitivity দেখিয়েছে।

---

Obese + Sedentary Participants

যারা একই সঙ্গে obese এবং sedentary—এই particularly high-risk group-এ model আরও high sensitivity দেখিয়েছে।

Results:

Sensitivity = 93%

এবং

Adjusted specificity = 95%

এখানে adjusted specificity-এর উদ্দেশ্য ছিল সত্যিকার অর্থে insulin-sensitive মানুষকে ভুলভাবে insulin-resistant হিসেবে classify করার ঘটনা কমানো।

অর্থাৎ এই subgroup-এ model-এর performance researchers-এর কাছে বিশেষভাবে notable ছিল।

এই results থেকে researchers suggest করেছেন যে এই approach এমন মানুষদের identify করতে বিশেষভাবে useful হতে পারে যারা early lifestyle intervention থেকে benefit পেতে পারেন।

---

কিন্তু শুধু এই dataset-এ ভালো হলেই তো হবে না

একটি Machine Learning model কোনো একটি dataset-এর specific characteristics বা quirks শিখে ফেলতে পারে।

তাই researchers আরও গুরুত্বপূর্ণ একটি পরীক্ষা করেন:

Independent validation cohort

অর্থাৎ completely আলাদা group-এর মানুষের data দিয়ে model test করা হয়।

---

Independent Validation Cohort

এই validation cohort-এ ছিল:

N = 72 participants

তারা initial WEAR-ME study-এর participant ছিলেন না।

তাদের recruit করা হয়েছিল একটি separate IRB-approved consented study-এর মাধ্যমে।

এই participants wearable data share করেছিলেন:

Fitbit Charge 6

দিয়ে।

এবং blood biomarker data in-person study center-এ সংগ্রহ করা হয়েছিল।

Study location ছিল San Francisco।

এই cohort-এর:

- Median BMI = 30.6 kg/m²
- Median age = 44.5 years

ছিল।

---

Independent Validation-এর ফল

WEAR-ME data দিয়ে train করা best-performing model-টি যখন এই completely independent cohort-এ test করা হয়:

Sensitivity = 84%

Specificity = 81%

ছিল।

অর্থাৎ original dataset-এর বাইরে গিয়েও model strong predictive performance maintain করেছে।

Researchers-এর মতে, এটি model-এর potential generalizability-এর evidence দেয়।

তবে খুব গুরুত্বপূর্ণ limitation হলো:

এটি এখনও একটি research prototype।

এর safety এবং effectiveness কোনো health-related real-world purpose-এর জন্য এখনও established হয়নি।

---

শুধু Prediction করলেই তো শেষ নয়

Researchers-এর পরবর্তী প্রশ্ন ছিল:

«ধরুন AI একজন মানুষকে বলল যে তার insulin resistance-এর risk আছে। কিন্তু সে যদি জিজ্ঞেস করে—“এর মানে কী?” বা “আমার এখন কী করা উচিত?”—তাহলে information-টা কীভাবে understandable করা যায়?»

এই প্রশ্ন থেকেই তারা একটি LLM-based system explore করেছেন।

---

Insulin Resistance Literacy and Understanding Agent

তারা তৈরি করেছেন:

Insulin Resistance Literacy and Understanding Agent

সংক্ষেপে IR Agent।

এটি একটি prototype agent, যা Gemini family of LLMs-এর ওপর তৈরি।

এর উদ্দেশ্য হলো insulin resistance-এর prediction-কে শুধু একটি number বা risk result হিসেবে না রেখে মানুষকে সেটি বুঝতে সাহায্য করা।

---

IR Agent কী করতে পারে?

যখন user metabolic health নিয়ে কোনো প্রশ্ন করে, IR Agent:

- personalized answer দিতে পারে
- context অনুযায়ী explanation দিতে পারে
- individual's study data ব্যবহার করতে পারে
- predicted IR status-এর context দিতে পারে
- educational information দিতে পারে

User-এর consent থাকলে agent specific user-provided data points access করতে পারে।

এছাড়া এটি:

- up-to-date information search করতে পারে
- calculations করতে পারে

অর্থাৎ conceptually এটি এমন একটি interface তৈরি করার চেষ্টা করছে যেখানে machine-learning prediction এবং LLM-based explanation একসঙ্গে কাজ করে।

---

কিন্তু IR Agent-এর purpose কী?

এখানে একটি গুরুত্বপূর্ণ distinction আছে।

IR Agent-এর উদ্দেশ্য:

education + information

এটি medical diagnosis দেওয়ার জন্য তৈরি নয়।

অর্থাৎ user-এর study data এবং predicted IR status দেখে agent explanation দিতে পারে, কিন্তু সেটিকে doctor-এর diagnosis বা medical treatment-এর replacement হিসেবে ধরা যাবে না।

---

Doctors দিয়ে IR Agent evaluate করা হয়েছিল

Researchers শুধু নিজেরা system-এর response ভালো মনে করেছেন—এমন নয়।

তারা ৫ জন board-certified endocrinologist দিয়ে IR Agent-এর responses evaluate করিয়েছেন।

তারা IR Agent-এর responses-কে একটি base model-এর responses-এর সঙ্গে compare করেন।

Endocrinologists IR Agent-এর responses-কে strongly prefer করেছেন এবং responses-গুলোকে:

- বেশি comprehensive
- বেশি trustworthy
- বেশি personalized

হিসেবে evaluate করেছেন।

Researchers-এর interpretation হলো, predictive health models-এর সঙ্গে LLM combine করলে মানুষের নিজের metabolic health সম্পর্কে understanding improve করার potential থাকতে পারে।

---

পুরো system-টা কীভাবে কাজ করে?

Conceptually pipeline-টা এমন:

Wearables
↓
Resting heart rate, steps, sleep ইত্যাদি

+

Routine Blood Biomarkers
↓
Fasting glucose, insulin, lipid panel ইত্যাদি

+

Demographics / Other information
↓
Age, BMI, health history ইত্যাদি

↓

Machine Learning Model

↓

HOMA-IR prediction / Insulin Resistance risk

↓

IR Agent

↓

User-এর জন্য personalized educational explanation

এইভাবে prediction model এবং LLM একসঙ্গে একটি broader health-understanding tool হিসেবে কাজ করার সম্ভাবনা তৈরি করে।

---

একটি গুরুত্বপূর্ণ finding: Blood sugar normal হলেও IR থাকতে পারে

Research-এর একটি interesting observation হলো—অনেক participant-এর HbA1c normal range-এর মধ্যে থাকা সত্ত্বেও insulin resistance ছিল।

বিশেষভাবে researchers উল্লেখ করেছেন যে study-তে অনেক normoglycemic participants, যাদের:

HbA1c < 5.7%

ছিল, তাদের মধ্যেও insulin resistance পাওয়া গেছে।

এখানে concept-টা গুরুত্বপূর্ণ:

Normal blood sugar ≠ necessarily no insulin resistance

অর্থাৎ একজন মানুষের blood glucose এখনও normal-looking range-এ থাকতে পারে, কিন্তু শরীরকে glucose control করতে বেশি insulin ব্যবহার করতে হতে পারে।

এই ধরনের early metabolic dysfunction traditional glucose-based screening-এর আগে detect করার সম্ভাবনাই এই research-এর একটি বড় motivation।

---

এই approach-এর সম্ভাব্য সুবিধাগুলো কী?

Google Research তাদের findings-এর ভিত্তিতে কয়েকটি potential advantage উল্লেখ করেছে।

১. Accessibility

অনেক মানুষের কাছে wearable data আগে থেকেই থাকতে পারে।

আর routine blood test-ও specialized insulin-resistance test-এর তুলনায় সহজে পাওয়া যেতে পারে।

অর্থাৎ completely new বা highly specialized measurement-এর বদলে existing data ব্যবহার করা যায়।

---

২. Early Detection

এই approach এমন মানুষের মধ্যে insulin resistance detect করার সম্ভাবনা দেখিয়েছে যাদের blood sugar এখনও abnormal হয়নি।

বিশেষ করে study-তে কিছু normoglycemic participant-এর মধ্যেও IR পাওয়া গেছে।

এতে type 2 diabetes develop হওয়ার অনেক আগেই risk শনাক্ত করার সম্ভাবনা তৈরি হয়।

---

৩. Scalability

Euglycemic insulin clamp-এর মতো specialized testing-এর তুলনায় wearable + routine blood data-based approach potentially অনেক বেশি scalable হতে পারে।

অর্থাৎ বড় population-এর মধ্যে screening করার একটি সম্ভাব্য পথ তৈরি হতে পারে।

তবে এটি বাস্তবে clinical screening method হিসেবে ব্যবহার করার আগে আরও validation প্রয়োজন।

---

৪. Personalization

High-risk subgroup-এ strong performance এবং user-specific data ব্যবহার করার capability থাকার কারণে এই ধরনের system ভবিষ্যতে personalized health tools-এর সঙ্গে integrate করা যেতে পারে।

তবে এই potential এখনও research stage-এ।

---

ভবিষ্যতে কী করা দরকার?

Researchers মনে করেন এই research-এর পরবর্তী ধাপে বেশ কিছু গুরুত্বপূর্ণ কাজ করতে হবে।

১. Longitudinal validation

একই মানুষকে দীর্ঘ সময় ধরে track করতে হবে।

অর্থাৎ শুধু একটি নির্দিষ্ট সময়ের data নয়, সময়ের সঙ্গে:

IR কীভাবে develop বা change করে

তা দেখতে হবে।

---

২. Intervention-এর impact

Lifestyle intervention বা অন্য ধরনের intervention-এর পরে model-এর prediction কীভাবে পরিবর্তিত হয়, সেটাও investigate করতে হবে।

অর্থাৎ intervention করলে model কি meaningful metabolic change detect করতে পারে?

---

৩. Genetic data

Future model-এ genetic information যোগ করার সম্ভাবনাও researchers উল্লেখ করেছেন।

কারণ insulin resistance এবং type 2 diabetes-এর risk-এর সঙ্গে genetic factors-ও সম্পর্কিত।

---

৪. Microbiome data

আরেকটি সম্ভাব্য information source হলো microbiome data।

ভবিষ্যতের multimodal model-এ wearable + blood biomarkers-এর সঙ্গে microbiome information combine করা যেতে পারে।

---

৫. Specific populations-এর জন্য model refine করা

সব population-এর metabolic characteristics একই নয়।

তাই বিভিন্ন population-এর জন্য model refine এবং validate করা প্রয়োজন।

বিশেষভাবে researchers চান model যেন diverse population-এর ক্ষেত্রে equitable performance দিতে পারে।

অর্থাৎ কোনো নির্দিষ্ট demographic group-এর ক্ষেত্রে system disproportionately কম accurate না হয়।

---

Researchers-এর overall conclusion

এই research দেখিয়েছে যে wearable data + routine blood biomarkers combine করে Machine Learning model ব্যবহার করে insulin resistance predict করার potential আছে।

বিশেষ করে:

Wearables + Demographics → auROC 0.70

+ Fasting Glucose → auROC 0.78

Wearables + Demographics + Routine Blood Panels →

- R² = 0.50
- auROC = 0.80
- Sensitivity = 76%
- Specificity = 84%

এবং high-risk subgroup-এ sensitivity আরও বেশি ছিল:

- Obese: 86%
- Sedentary: 88%
- Obese + Sedentary: 93%

Independent validation cohort-এ:

- Sensitivity: 84%
- Specificity: 81%

এই findings suggest করে যে existing wearable এবং routine clinical data ব্যবহার করে insulin resistance-এর জন্য একটি potentially scalable screening approach তৈরি করা সম্ভব হতে পারে।

---

সবচেয়ে interesting conceptual point

এই research-এর মূল idea শুধু “AI দিয়ে insulin resistance predict করা” নয়।

বরং এখানে তিনটি layer একসঙ্গে কাজ করছে:

Layer 1 — Passive data

Wearable থেকে পাওয়া:

heart rate + activity + sleep

Layer 2 — Routine clinical data

Blood test থেকে:

glucose + insulin + lipid biomarkers

Layer 3 — AI

Machine Learning:

এই data থেকে hidden metabolic pattern → IR prediction

তারপর আরেকটি AI layer:

Gemini-based IR Agent → prediction-টা মানুষকে বুঝিয়ে বলা

অর্থাৎ long-term vision অনেকটা এমন:

Everyday wearable data
+
Routine healthcare data
↓
AI metabolic risk detection
↓
Personalized explanation
↓
Earlier awareness / potentially earlier intervention

এটাই এই research-এর broader direction।

---

কিন্তু খুব গুরুত্বপূর্ণ: এটি এখনও Medical Device নয়

Google-এর disclaimer এখানে অত্যন্ত গুরুত্বপূর্ণ।

তারা স্পষ্টভাবে বলেছে যে এই proposed approach এবং IR Agent বিভিন্ন health application-এর জন্য promising হলেও:

এই research-এর modelগুলো approved medical device নয়।

এগুলো:

- medical devices নয়
- FDA দ্বারা cleared হয়নি
- FDA দ্বারা approved হয়নি
- কোনো national বা international regulatory agency দ্বারা reviewed/approved হয়নি

এবং এগুলো:

professional medical advice-এর substitute নয়।

এগুলো diagnosis বা treatment-এর replacement হিসেবেও ব্যবহার করা উচিত নয়।

Real-world deployment-এর আগে প্রয়োজন হবে:

- rigorous testing
- additional validation
- safety evaluation
- regulatory approval

অর্থাৎ research result promising হলেও এটি এখনো এমন পর্যায়ে নেই যেখানে কেউ শুধু smartwatch + blood test data দিয়ে এই model-এর output দেখে নিজের medical diagnosis ধরে নেবে।

---

Research Team ও Partnership

এই research Google Research এবং partner teams-এর যৌথ কাজ।

Contributors ছিলেন:

- Ahmed A. Metwally
- A. Ali Heydari
- Daniel McDuff
- Alexandru Solot
- Zeinab Esmaeilpour
- Anthony Z. Faranesh
- Menglian Zhou
- David B. Savage
- Conor Heneghan
- Shwetak Patel
- Cathy Speed
- Javier L. Prieto

Google Quest Diagnostics-এর সঙ্গে partnership করেছিল।

Quest Diagnostics eligible participants-কে তাদের free blood draw-এর মাধ্যমে পাওয়া biomarker data share করার সুযোগ দেয়।

এই blood testing-এর মধ্যে ছিল:

- comprehensive metabolic panel
- cholesterol
- triglycerides
- insulin levels

ইত্যাদি।

---

পুরো research একদম সহজ ভাষায়

ধরুন একজন মানুষের কাছে একটি smartwatch আছে।

Watch জানে:

সে কতটা হাঁটে → কত ঘুমায় → resting heart rate কত → activity pattern কেমন

তারপর তার routine blood test থেকে পাওয়া গেল:

fasting glucose → insulin → cholesterol → triglycerides → অন্যান্য biomarkers

AI এই information একসঙ্গে দেখে।

তারপর AI চেষ্টা করে estimate করতে:

«“এই ব্যক্তির insulin resistance থাকার সম্ভাবনা কতটা?”»

এরপর Gemini-based IR Agent সেই result-টা এমনভাবে explain করার চেষ্টা করে যাতে একজন সাধারণ মানুষ বুঝতে পারেন:

«“Insulin resistance কী?”
“আমার result-এর অর্থ কী?”
“এই metabolic pattern সম্পর্কে কী জানা যায়?”»

কিন্তু শেষ ধাপে একজন doctor-এর diagnosis বা treatment recommendation-এর জায়গা নেওয়া হচ্ছে না।

অর্থাৎ research-এর vision হলো:

Data → Prediction → Understanding

এবং দীর্ঘমেয়াদে:

Early detection → Earlier awareness → Potentially earlier preventive action

তবে এই শেষ অংশটি এখনো future clinical validation-এর বিষয়—এটি বর্তমান research থেকে established medical outcome হিসেবে ধরা যাবে না।Original Google Research article: [Insulin resistance prediction from wearables and routine blood biomarkers](https://research.google/blog/insulin-resistance-prediction-from-wearables-and-routine-blood-biomarkers/?utm_source=chatgpt.com)

একটা গুরুত্বপূর্ণ distinction: এই article-এ HOMA-IR prediction এবং insulin-resistance classification—দুটো related কিন্তু এক জিনিস নয়। HOMA-IR হলো একটি calculated marker, আর classification-এ researchers HOMA-IR ≥ 2.9 threshold ব্যবহার করেছেন। 
