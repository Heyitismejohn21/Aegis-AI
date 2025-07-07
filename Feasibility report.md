System Architecture and Deployment
The solution will use a hybrid deployment across servers, web interfaces, and dedicated embedded/edge devices. For the demo, the core application runs as a secure web service (using existing servers or cloud VM) that captures face images via a browser. At the same time, the design supports edge processing on low-power devices to reduce latency and increase robustness
zpesystems.com
. For example, a Raspberry Pi or smartphone can perform local face detection and recognition (see image below). This edge capability allows the system to switch between online/cloud and offline/local modes depending on connectivity and performance needs. Edge computing “deploys compute to the network’s edges to improve performance”
zpesystems.com
, so our architecture will process data on-device when possible and fallback to the server/API pipeline as needed. This ensures the system can function in high-risk or disconnected environments without requiring new hardware (no additional GPUs) – it simply uses existing CPU-friendly models (e.g. optimized FaceNet) and lightweight detection (e.g. Blazeface)
faceonlive.com
twine.net
. Figure: An embedded system (e.g. Raspberry Pi) running on-device face recognition using OpenCV (no new GPU required). This example shows a live camera feed being processed to identify a consenting subject.
Offline/Online Switching
The system is designed to operate in both offline (edge) and online (cloud) modes with seamless switching. In practice, if internet connectivity is available, the application can offload heavy tasks (e.g. querying multiple web APIs) to the server. If connectivity is poor or unavailable, the application will perform all inference locally using on-device models (e.g. running TensorFlow Lite or an on-device face-recognition engine). To minimize user interaction, the switch is automatic: the app detects connectivity and chooses the best pipeline. This dual-mode operation means the demo can be presented as a web app for now, but the same codebase (e.g. using cross-platform frameworks) could later be extended to mobile or wearable AR glasses. All communication will be secured (no unencrypted data transfer), and authentication is not required from end-users since subjects pre-consent to being scanned. No user login or registration is needed – the system processes each new face as it appears, without relying on any pre-existing user database.
Data Privacy and Consent
All participants in the demo will provide explicit, written consent before their images or data are used. We will not store any personal data beyond the scope of the demo, and no private information is retained after processing. Importantly, there is no pre-registered user database: the system does not rely on any stored profiles or login accounts. Instead, each facial recognition event is handled on-the-fly. This minimizes user interaction – the operator simply points the camera at a consenting subject, and the system processes the input automatically. Because the project is for demonstration only, all data handling will follow ethical guidelines: no data harvesting, no unauthorized recording, and immediate deletion of any temporary data after each run. By design, the pipeline captures only new images and queries external sources in real time, ensuring compliance with privacy norms and focusing on automation rather than user-led data entry.
Face Recognition and Data Retrieval Pipeline
Our system follows the I-XRAY-inspired pipeline but with higher accuracy and robustness. First, the camera feed is processed by a face-detection model to locate faces. We will use state-of-the-art open-source models (e.g. Blazeface for speed on devices
faceonlive.com
 or InsightFace for accuracy
faceonlive.com
) and libraries like OpenCV or DLib
twine.net
faceonlive.com
. Once a face is detected, a face-encoding model (e.g. FaceNet) generates a feature vector. For the demo, we can use a free service like Exadel’s CompreFace which provides REST APIs for face recognition using FaceNet/InsightFace under the hood
github.com
. CompreFace can be deployed as a Docker service on CPU, requiring no additional GPU
github.com
. Alternatively, the Python face_recognition library (built on DLib/OpenCV) offers an easy API to detect and compare faces
twine.net
. Once a face is encoded, we retrieve identity information by querying public sources. For example, we can send the face image (or its feature embedding) to a reverse-image search service. Harvard’s I-XRAY used PimEyes (a face-search engine) followed by public-record lookups
harvardtechnologyreview.com
. We will mimic this: the app can call a face-search API (or open-source equivalent) to find matching identities. After obtaining a candidate name, the system automatically queries free or low-cost data services (like FastPeopleSearch or phone/address lookup APIs) to gather details such as address or phone. Large Language Models (LLMs) are then used to parse and cross-check this information (e.g. verifying that the name matches the retrieved address logically)
harvardtechnologyreview.com
. This layered approach – face recognition → identity search → data aggregation – is fully automated once the face enters view. As with I-XRAY, our goal is to surface details (name, home address, etc.) within seconds, but with careful filtering so that only consensually-provided subjects are processed. All APIs and databases used will either be free-tier or publicly accessible. Figure: Harvard’s I-XRAY prototype combined smart glasses, facial search, and data aggregation to reveal personal info from a face
harvardtechnologyreview.com
harvardtechnologyreview.com
. Our system follows a similar design: an embedded camera feeds face data into recognition engines, and retrieved identities are cross-referenced with public records automatically.
Software Tools and APIs
We will rely on open-source models and free APIs wherever possible, since no new hardware purchases are allowed. For face detection/recognition, this includes:
OpenCV/DLib – classical face detectors (Haar cascades or HOG) for quick prototype testing
twine.net
faceonlive.com
. These run on CPU and are lightweight.
FaceNet/InsightFace – deep neural networks for face embeddings; models are available open-source and can be optimized for CPU inference
twine.net
faceonlive.com
.
CompreFace – a free Docker-based face recognition service (no ML expertise needed) that uses FaceNet/InsightFace
github.com
.
face_recognition Python library – simple API on top of DLib for real-time face matching
twine.net
.
For data retrieval, example APIs and services:
Face++ (Megvii) – offers a generous free tier for face analysis (detection, recognition, attributes)
faceonlive.com
. While Face++ can compare faces, for the demo it can verify a name once we query it, or provide confidence scores.
Kairos Face API – provides 1:1 and 1:N matching and has a free starter plan
twine.net
.
Lambda Labs API – has high accuracy (claimed ~99%) and a 1,000-images/month free tier
nordicapis.com
, useful for bulk testing.
Google Vision / Azure Face – both have free quotas (e.g. 1,000 free Google Vision calls, 30,000 free Azure transactions) for face detection and analysis
faceonlive.com
.
Eden AI (optional) – a platform to manage multiple APIs; it allows switching between different face APIs and consolidating billing
faceonlive.com
.
For gathering identity data (once a name is known), we will use free web-search or public-data APIs. FastPeopleSearch (U.S.) can supply names/addresses, and various free phone lookup APIs can verify phone numbers. No paid subscription APIs will be used in the demo; if needed, we rely on free trials or open data. All chosen tools are well-regarded for accuracy, and we aim to cross-validate results across sources to improve reliability in challenging (high-risk) conditions.
Data Sources and Datasets
To develop and test the system, we will use public face image datasets that cover diverse conditions. For example:
CelebA – 200K+ celebrity face images
imerit.net
, with a wide range of poses and lighting.
Labeled Faces in the Wild (LFW) – ~13,000 images of ~6,000 people
imerit.net
, commonly used for benchmarking face recognition.
UTKFace – 20,000 faces with age/gender labels
imerit.net
, useful for testing demographic variation.
UMDFaces – 367,000+ annotations across 8,200 subjects
imerit.net
, great for training under varied poses.
These datasets are freely available (e.g. on Kaggle or university sites) and allow us to simulate the recognition pipeline without using any private data. We will also curate a small set of controlled images from the consenting participants to fine-tune the models as needed.
In summary, we will integrate state-of-the-art algorithms and free data: models like FaceNet/InsightFace (often cited as achieving ~99% accuracy
nordicapis.com
) and robust detectors like Blazeface (designed for fast, on-device detection
faceonlive.com
). The combination of pre-trained models, public datasets, and free API tiers ensures we can achieve high accuracy without additional hardware or paid services.
Team Workflow and Timeline
The project will be executed over 3 months, with clear responsibilities for each team member. Below is a high-level breakdown of each person’s workflow and timeline (Month 1 to Month 3) to ensure completion by demo time:
Project Manager (e.g. Team Lead) – Month 1: Finalize project scope, ethical approvals, and consents; set up development environment on existing servers; coordinate team schedules. Month 2: Oversee integration of components (front-end, back-end, ML); ensure consent forms are collected for test subjects. Month 3: Manage testing and validation; handle documentation and final presentation; ensure security/compliance checks are done.
ML Engineer – Month 1: Research and select face-recognition models; deploy a quick prototype using CompreFace or face_recognition library for baseline face encoding
github.com
twine.net
. Gather sample data from public datasets. Month 2: Integrate the face detection/recognition model into the backend; optimize for CPU use. Begin implementing the data-retrieval logic (e.g. pipelining PimEyes or Face++ queries). Month 3: Tune model parameters (e.g. embedding thresholds) and address edge cases (occlusions, poor lighting); test accuracy with consenting subjects; iterate based on results.
Backend Developer – Month 1: Set up server infrastructure (e.g. Docker container for CompreFace) and implement REST APIs for the face pipeline. Establish database or cache (if any, though no prereg DB of people will be stored). Month 2: Integrate third-party APIs for identity retrieval (e.g. PimEyes, Face++, people-search APIs); handle data parsing and prepare results. Implement LLM or heuristic logic to cross-reference and validate results. Month 3: Ensure reliability and scalability (e.g. add retry logic, rate-limit handling); optimize performance (minimize latency); conduct stress tests.
Frontend Developer – Month 1: Design the web interface; implement camera capture (e.g. using WebRTC) and live video feed. Ensure minimal UI (since we avoid logins) – e.g. “Start Scan” button for consenting subject. Month 2: Connect front-end to backend APIs; display recognition results in an overlay or info panel (e.g. name, address). Handle user feedback (e.g. highlighting processing status). Month 3: Refine UI/UX based on testing (make it user-friendly for demo); implement fail-safes (e.g. on failure, retry or notify user). Prepare the web app for demo deployment, including any hosting setup.
Data/QA Engineer – Month 1: Assemble all required datasets (CelebA, LFW, etc.) and annotate any needed faces from consenting users. Verify data quality and consent documentation. Month 2: Develop test cases and evaluation metrics (e.g. accuracy under different lighting, mask/no-mask). Perform integration testing of each pipeline stage (detection → recognition → retrieval). Month 3: Conduct full-system testing in realistic scenarios (e.g. “high-risk” conditions with glare or multiple faces); log issues and work with others to fix bugs. Ensure the demo runs reliably within time limits. Prepare final reports and confirm that all subjects’ data are handled per consent.
Each member’s work is coordinated to meet milestones at the end of each month, ensuring all components (server, ML model, UI, data integration) come together smoothly. By the end of 3 months, we will have a web-based prototype that automatically identifies consenting individuals from live video and displays personal details (name, address, etc.) using only free tools and existing hardware – with a clear path to extend this system onto embedded or AR platforms in the future. Sources: The design draws on established face-recognition techniques and the I-XRAY project as a blueprint
harvardtechnologyreview.com
harvardtechnologyreview.com
. Open-source libraries like CompreFace and FaceNet are used for cost-free, accurate recognition
github.com
twine.net
. Free API tiers and public datasets (CelebA, LFW, UTKFace, UMDFaces) provide the necessary data and functionality without new hardware or expense
imerit.net
imerit.net
imerit.net
imerit.net
. These choices ensure a feasible implementation within the 3-month timeline and available resources.
