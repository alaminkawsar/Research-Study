# GlucoFM: Continuous Glucose Monitoring-এর জন্য Foundation Model

Google Research — ২৬ আগস্ট ২০২৬

Google Research-এর Ahmed A. Metwally এবং Zechen Li-এর তৈরি GlucoFM হলো একটি lightweight, self-supervised CGM (Continuous Glucose Monitoring) foundation model।

সহজভাবে বললে, GlucoFM মানুষের glucose-এর data দেখে এমন কিছু general pattern শিখতে পারে, যেগুলো পরে বিভিন্ন metabolic health-related prediction task-এ ব্যবহার করা যায়।

এর বিশেষত্ব হলো—এটি glucose-এর ধীরে পরিবর্তন হওয়া long-term trend এবং হঠাৎ বা short-term পরিবর্তন—এই দুটিকে আলাদা করে বোঝার চেষ্টা করে।

এর মাধ্যমে modelটি diabetes risk, insulin resistance, beta-cell dysfunction এবং খাবার খাওয়ার পর glucose কীভাবে পরিবর্তিত হবে—এসব prediction task-এ ব্যবহার করা হয়েছে।

---

CGM কেন গুরুত্বপূর্ণ?

আজকের অনেক wearable device movement এবং বিভিন্ন physiological signal ব্যবহার করে activity বা sleep-এর মতো জিনিস estimate করতে পারে।

কিন্তু এগুলো glucose regulation সম্পর্কে সরাসরি তথ্য দেয় না।

CGM (Continuous Glucose Monitor) অন্যদিকে কয়েক মিনিট পরপর শরীরের skin-এর নিচে থাকা sensor-এর মাধ্যমে interstitial glucose measure করে।

ফলে আমরা দেখতে পারি—

- fasting অবস্থায় glucose কেমন থাকে
- রাতে glucose কীভাবে পরিবর্তিত হয়
- খাবার খাওয়ার পর glucose কীভাবে ওঠানামা করে
- দিনের বিভিন্ন সময়ে glucose-এর pattern কেমন

সমস্যা হলো, এই বিশাল glucose data থেকে meaningful information বের করা সহজ নয়। বিশেষ করে ভালো quality-এর clinical label সংগ্রহ করা expensive এবং সময়সাপেক্ষ।

---

GlucoFM আসলে কী করছে?

আগের কিছু CGM foundation model, যেমন CGMformer, GluFormer এবং CGM-JEPA, glucose data-কে মূলত একটি single representation stream হিসেবে process করে।

কিন্তু Google-এর researchers-এর যুক্তি হলো, glucose data আসলে এতটা simple নয়।

একজন মানুষের glucose level-এর মধ্যে সাধারণত দুই ধরনের পরিবর্তন দেখা যায়:

১. Slow baseline trend

এটি হলো glucose-এর relatively ধীরে পরিবর্তন হওয়া overall state।

২. Short-term deviation

এর মধ্যে খাবার, physical activity, শরীরের physiological response অথবা sensor-এর artifact-এর কারণে হঠাৎ হওয়া পরিবর্তন থাকতে পারে।

GlucoFM এই দুই ধরনের information-কে আলাদা stream-এ process করে।

অর্থাৎ modelটি glucose data-কে মোটামুটি এভাবে দেখে:

Slow glucose state + Short-term events → Overall metabolic representation

এই dual-stream approach-টাই GlucoFM-এর একটি মূল idea।

---

Modelটি কীভাবে train করা হয়েছে?

GlucoFM train করার জন্য researchers 109,066 hours of unlabeled CGM data ব্যবহার করেছেন।

এই data এসেছে Wear-CGM এবং আরও চারটি published dataset থেকে।

মোট ছিল 477 participant/session records।

এখানে গুরুত্বপূর্ণ বিষয় হলো—সব data-র সঙ্গে clinical label ছিল না।

অর্থাৎ modelকে প্রতিটি glucose recording-এর পাশে "এই ব্যক্তি diabetic", "এই ব্যক্তির insulin resistance আছে"—এমন label দিয়ে train করা হয়নি।

বরং model প্রথমে unlabeled glucose data থেকে glucose-এর structure এবং pattern নিজে নিজে শেখে।

এটাই self-supervised learning-এর মূল ধারণা।

---

CGM data-তে একটা সমস্যা আছে

বাস্তব CGM data সবসময় perfectly clean হয় না।

কখনও—

- data missing থাকে
- sampling interval আলাদা হয়
- sensor কিছু সময় কাজ করে না
- sensor artifact তৈরি করে
- glucose measurement-এ অস্বাভাবিক fluctuation দেখা যায়

GlucoFM প্রতিটি recording-কে একটি 24-hour, 5-minute grid-এর সঙ্গে align করে।

আর কোন জায়গায় সত্যিই measurement আছে এবং কোন জায়গায় data missing—সেটাও modelকে জানানো হয়।

অর্থাৎ model missing data-কে actual glucose measurement হিসেবে ধরে নেয় না।

---

Dual-stream encoder

GlucoFM-এর encoder glucose signal-কে দুই ভাগে দেখার চেষ্টা করে।

১. State component

এটি relatively slow glucose trend capture করে।

যেমন, একজন মানুষের দিনের overall glucose level বা baseline কীভাবে পরিবর্তিত হচ্ছে।

২. Residual / event component

এটি short-term পরিবর্তন capture করে।

যেমন—

- খাবার খাওয়ার পর glucose spike
- exercise-এর পরে glucose change
- physiological response
- sensor artifact

তারপর এই দুই ধরনের information combine করে model একটি useful representation তৈরি করে।

---

Model কীভাবে শেখে?

GlucoFM-এর training-এর জন্য মূলত দুটি complementary task ব্যবহার করা হয়েছে।

১. Contextual prediction

ধরুন একটি দিনের glucose sequence-এর কিছু অংশ আমরা hide করে দিলাম।

তারপর modelকে বলা হলো:

"চারপাশের information দেখে এই hidden অংশের representation কেমন ছিল সেটা predict করো।"

এখানে model সরাসরি exact glucose number reconstruct করার চেষ্টা করছে না।

বরং সে latent representation predict করছে।

এর ফলে modelকে প্রতিটি sensor reading হুবহু copy করার বদলে broader glucose pattern বুঝতে হয়।

---

২. Temporal dynamics

Glucose static নয়—সময় অনুযায়ী পরিবর্তিত হয়।

তাই modelকে আরেকটি কাজ দেওয়া হয়:

একজন মানুষের baseline এবং short-term glucose deviation এক ঘণ্টা পরে কীভাবে পরিবর্তিত হবে, সেটা predict করা।

এর ফলে model glucose readings-কে আলাদা আলাদা isolated number হিসেবে না দেখে একটি continuous temporal process হিসেবে বুঝতে শেখে।

---

Real-world CGM-এর মতো data বানানো

Training-এর সময় researchers ইচ্ছাকৃতভাবে বিভিন্ন ধরনের সমস্যা data-তে introduce করেছেন।

যেমন—

- baseline drift
- sudden compression-like drops
- sparse sampling
- short disconnections

এর উদ্দেশ্য হলো modelকে বাস্তব CGM data-তে যেসব imperfection এবং missingness দেখা যায়, সেগুলোর সঙ্গে পরিচিত করা।

---

GlucoFM কী কী করতে পারে?

Researchers GlucoFM-কে চারটি cohort এবং সাতটি clinical prediction task-এ evaluate করেছেন।

Taskগুলোর মধ্যে ছিল:

- diabetes risk
- insulin resistance
- beta-cell dysfunction
- hyperlipidemia
- hypoglycemia
- obesity
- glucotype

এছাড়াও postprandial glycemic response (PPGR)—অর্থাৎ খাবার খাওয়ার পর glucose কীভাবে পরিবর্তিত হবে—সেটাও predict করা হয়েছে।

---

Diabetes এবং metabolic health prediction

Researchers একটি 24-hour glucose window নিয়ে model-এর representation ব্যবহার করে prediction করার পরীক্ষা করেন।

১৪টি cohort–task evaluation-এ GlucoFM-এর average PR-AUC 58.8 ছিল।

একই data-তে retrain করা strongest CGM-specific baseline-এর average PR-AUC ছিল 54.7।

অর্থাৎ absolute difference ছিল 4.1 percentage points।

Google Research-এর evaluation-এ GlucoFM diabetes-risk এবং beta-cell-dysfunction-এর সব evaluation-এ এবং insulin-resistance-এর চারটির মধ্যে তিনটিতে highest PR-AUC পেয়েছে।

---

খাবারের পর glucose কতটা বাড়বে?

এটি GlucoFM-এর একটি interesting application।

Researchers জানতে চেয়েছিলেন:

খাবার খাওয়ার আগে পর্যন্ত যে information পাওয়া গেছে, সেটা ব্যবহার করে পরবর্তী দুই ঘণ্টায় glucose কীভাবে পরিবর্তিত হবে তা predict করা যায় কি না।

তারা 34 জন participant-এর 874 paired meal events ব্যবহার করেছেন।

Model-কে ধীরে ধীরে আরও information দেওয়া হয়েছে:

1. খাবারের আগের এক ঘণ্টার CGM data
2. খাবারের calories
3. carbohydrate
4. fat
5. protein
6. dietary fiber
7. fasting glucose
8. BMI
9. diabetes status

সব information একসঙ্গে দেওয়ার পর GlucoFM-এর average MAE ছিল 21.88 mg/dL।

তুলনায় best baseline-এর MAE ছিল 22.90 mg/dL, আর train-fold mean baseline-এর ছিল 27.69 mg/dL।

MAE বা Mean Absolute Error যত কম, prediction তত কাছাকাছি।

অর্থাৎ GlucoFM historical glucose context ব্যবহার করে খাবারের পর glucose response predict করতে সাহায্য করতে পারে—এমন evidence researchers পেয়েছেন।

---

শুধু এক দিনের data কি যথেষ্ট?

সবসময় নয়।

একজন মানুষের একদিনের glucose pattern তার পুরো metabolic pattern-এর representation নাও হতে পারে।

তাই researchers দেখেছেন, একাধিক দিনের data combine করলে কী হয়।

GlucoFM প্রতিটি দিনকে আলাদাভাবে encode করে এবং সর্বোচ্চ সাত দিনের representation average করে।

অনেক dataset-এ অতিরিক্ত দিন যোগ করলে prediction performance improve করেছে।

উদাহরণ হিসেবে:

- Stanford beta-cell dysfunction task-এ 9.6 points gain দেখা গেছে
- Hall diabetes prediction task-এ 14.0 points gain দেখা গেছে

তবে সব জায়গায় improvement একই ছিল না। ShanghaiT2DM insulin-resistance task-এ simple averaging ব্যতিক্রম হিসেবে ভালো improvement দেয়নি।

অর্থাৎ কত দিনের data এবং কীভাবে সেই data combine করা উচিত—তা task অনুযায়ী আলাদা হতে পারে।

---

অন্য dataset-এর মানুষের ক্ষেত্রে কাজ করে কি?

এটাও গুরুত্বপূর্ণ।

ধরুন model একটি clinical study-এর মানুষের data থেকে diabetes risk সম্পর্কে কিছু শিখল।

এখন সেই model-কে অন্য একটি completely different study-এর মানুষের data দিলে কী হবে?

Researchers এটাও test করেছেন।

Diabetes risk এবং insulin resistance-এর cross-dataset transfer evaluation-এ GlucoFM 12টির মধ্যে 11টি evaluation-এ strongest competing method-এর চেয়ে এগিয়ে ছিল, যেখানে difference ছিল 0.5 থেকে 8.6 PR-AUC points।

একটি evaluation-এ এটি 0.6 points পিছিয়ে ছিল।

এর অর্থ হলো, modelটি শুধু একটি নির্দিষ্ট dataset-এর quirks মুখস্থ না করে কিছু more general metabolic pattern শিখতে পেরেছে—এমনটাই এই evaluation থেকে researchers মনে করছেন।

---

কম labeled data দিয়েও কি কাজ করে?

Clinical data label করা expensive।

তাই researchers few-shot learning-ও test করেছেন।

অর্থাৎ modelকে খুব অল্প সংখ্যক labeled example দিয়ে downstream task শেখানোর চেষ্টা করা হয়েছে।

তাদের evaluation-এ GlucoFM limited-data settings-এও strong performance দেখিয়েছে—এমনকি কিছু সবচেয়ে limited setting-এ যেখানে প্রতি class-এ মাত্র একজন labeled participant বা participant-এর মাত্র 1% observation ব্যবহার করা হয়েছিল।

এখানে মূল সুবিধাটা হলো:

প্রথমে বড় পরিমাণ unlabeled CGM data থেকে general representation শেখানো → পরে অল্প labeled data দিয়ে specific clinical task শেখানো।

এটি healthcare AI-এর জন্য potentially useful approach হতে পারে।

---

দুই ধরনের glucose signal আলাদা করা কেন দরকার?

Researchers এটাও পরীক্ষা করেছেন যে dual-stream architecture সত্যিই useful কি না।

তারা কয়েকটি alternative model-এর সঙ্গে compare করেছেন:

- raw glucose সরাসরি process করা
- শুধু slow trend-এর দিকে focus করা
- শুধু short-term event-এর দিকে focus করা
- full dual-stream model

শুধু short-term event নিয়ে কাজ করা model সবচেয়ে দুর্বল ছিল।

Raw-input এবং state-only model মোটামুটি competitive হলেও full dual-stream design consistently ভালো performance দেখিয়েছে।

এতে researchers-এর hypothesis কিছুটা support পেয়েছে যে glucose-এর slow dynamics এবং fast dynamics—দুটোকেই complementary information হিসেবে দেখা উচিত।

---

তাহলে GlucoFM-এর মূল idea কী?

একদম সহজ করে বললে:

একজন মানুষের CGM data-কে শুধু কয়েক হাজার glucose number হিসেবে দেখার বদলে GlucoFM চেষ্টা করে সেই data-এর মধ্যে থাকা different timescale-এর patterns বুঝতে।

অর্থাৎ:

Long-term / slow trend
↓
Short-term glucose events
↓
Time-of-day + missingness
↓
একটি reusable representation
↓
Diabetes / insulin resistance / beta-cell dysfunction / post-meal glucose prediction ইত্যাদি

এই representation একবার শেখানো হয়ে গেলে, প্রতিটি নতুন clinical task-এর জন্য বিশাল পরিমাণ labeled data প্রয়োজন নাও হতে পারে।

---

Google-এর conclusion

Google Research-এর মতে, CGM modelগুলো glucose dynamics-এর multiscale structure explicitly account করলে benefit পেতে পারে।

অর্থাৎ শুধু glucose-এর current value নয়, বরং—

- slow trend
- short-term deviation
- দিনের সময়
- missing data
- sensor-related variation

এসব একসঙ্গে বিবেচনা করা গুরুত্বপূর্ণ।

GlucoFM unlabeled CGM data থেকে reusable representation শিখে বিভিন্ন prediction, cross-dataset transfer এবং few-shot setting-এ strong results দেখিয়েছে।

তবে researchers নিজেরাই কিছু limitation উল্লেখ করেছেন।

মানুষভেদে metabolic response আলাদা হতে পারে, cohort এবং sensor device-এর মধ্যেও পার্থক্য আছে, এবং বর্তমান pre-training population এখনও relatively small।

তাদের পরবর্তী লক্ষ্য হলো:

- আরও বড় এবং diverse population-এর data দিয়ে model train করা
- শুধু আলাদা আলাদা 24-hour window না দেখে native multi-day modeling করা
- সপ্তাহ বা মাস ধরে তৈরি হওয়া glucose trend capture করা
- এবং real-time glucose changes-এর ক্ষেত্রে modelটি কীভাবে কাজ করে তা দেখা।

এক লাইনে GlucoFM

GlucoFM হলো এমন একটি AI foundation model, যেটি raw CGM data থেকে মানুষের glucose-এর slow baseline pattern এবং fast/short-term changes আলাদাভাবে শিখে, তারপর সেই learned representation ব্যবহার করে বিভিন্ন metabolic health-related prediction করার চেষ্টা করে।মূল Google Research article: [GlucoFM: Foundation model for continuous glucose monitoring](https://research.google/blog/glucofm-foundation-model-for-continuous-glucose-monitoring/?utm_source=chatgpt.com) 
