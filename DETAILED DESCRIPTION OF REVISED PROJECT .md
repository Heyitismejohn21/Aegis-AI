# Aegis-AI
Aegis AI: A live AI security demo. Using DeepFace, it verifies identity and analyzes emotion for duress detection. Selenium enables real-time web profile matching. A GenAI instantly creates security protocols for audience-suggested threats, fusing computer vision, web automation, and generative AI.
I UNDERSTAND THAT THE DESCRIPTION IS PRETTY LONG BUT I SUGGEST THAT YOU READ IT.
**"WHAT IS THE AIM OF THIS PROJECT"**
An excellent and ambitious project idea! The intersection of facial recognition, generative AI, and web automation holds immense potential for a "wow factor" project in the security domain. Let's assess your "Point Cloud ID" concept and then explore a powerful, innovative alternative that builds upon your initial thoughts while enhancing feasibility and impact for an exhibition setting.

### Assessment of "Point Cloud ID"

**Concept:** Retrieve facial data from publicly available sources to build a database for security purposes.

| **Metric** | **Assessment** | **Comments** |
| :--- | :--- | :--- |
| **Innovation** | Moderate | The concept of creating facial databases is not new to the security industry. The innovation would lie in the scale and automation of data collection using Selenium. |
| **"Wow" Factor** | Moderate to High | The visual of rapidly populating a database with faces from the web could be impressive. However, it might also raise immediate privacy concerns from the audience, potentially overshadowing the technological achievement. |
| **Usefulness in Security** | High (in principle) | Threat actor identification and intelligence gathering are core security tasks. However, the legality and ethics of creating such a database from public, non-consensual sources are highly problematic and a significant hurdle for a student project. |
| **Live Environment Success Rate** | Low to Moderate | The success of this project hinges on the reliability of web scraping. Websites frequently change their structure, and many employ anti-scraping technologies. A live demo could easily fail if a target website has implemented such measures. Furthermore, the quality of facial data retrieved (low resolution, poor lighting, obstructions) would likely lead to a high error rate for facial recognition. |

**Conclusion:** While the core idea is relevant to the security industry, "Point Cloud ID" faces significant ethical and technical challenges that could detract from its impressiveness and success in a live exhibition.

---

### Modified and Enhanced Project Idea: "Aegis AI: Real-Time Threat Assessment and Anomaly Detection"

This project shifts the focus from mass data collection to intelligent, real-time analysis, offering a more innovative and ethically sound demonstration with a higher "wow" factor.

**Core Concept:** An advanced security checkpoint system that uses a multi-layered AI approach to identify not just an individual, but also their intent and potential threats in real-time.

#### How It Works:

An individual (a volunteer from the audience) stands before a camera connected to the system. The "Aegis AI" platform performs the following steps in real-time, displayed on a large screen for the audience:

**1. Identity Verification and Digital Footprint Analysis (DeepFace & Selenium):**

* **Facial Recognition (DeepFace):** The system captures the person's face. Instead of matching it against a dubiously sourced database, it could:
    * **Option A (Exhibition Mode):** Match the face against a small, pre-registered, and consented database of "authorized personnel" (your student team, for example).
    * **Option B (The "Wow" Demo):** Ask the volunteer for their name and a public social media profile (e.g., LinkedIn). Selenium would then navigate to that profile, and DeepFace would verify if the person in front of the camera matches the profile picture. This is a powerful demonstration of consent-based, real-time verification.
* **Digital Threat Assessment (Selenium & GenAI):** Upon successful verification, Selenium can scan the provided public profile for publicly visible information. This data is then fed to a GenAI model to perform a rapid, simulated "threat assessment." For instance, the GenAI could be prompted to identify any publicly shared information that might pose a security risk (e.g., "This individual has publicly shared their location 15 times in the last month," or "No suspicious public activity detected"). *Disclaimer: This should be clearly presented as a simulation of a security analysis.*

**2. Behavioral and Emotional Analysis (DeepFace):**

* While the identity is being checked, DeepFace's attribute analysis capabilities will be on full display. The system will analyze the person's real-time emotional state (e.g., neutral, happy, anxious, angry) and other facial attributes.
* **Anomaly Detection:** The system can be programmed to flag unusual emotional states. For example, if an authorized person appears highly stressed or fearful, it could indicate they are under duress.

**3. Generative AI-Powered Threat Simulation and Response (GenAI):**

* **The "What If" Scenario (The Ultimate "Wow" Factor):** This is where the generative AI truly shines. The audience can suggest a hypothetical threat scenario. For example:
    * "What if this person was trying to tailgate someone into a secure area?"
    * "What if this person's access card was stolen?"
* The GenAI, acting as the "Aegis AI" brain, would then generate a step-by-step security protocol in real-time. For instance:
    * **Scenario:** Stolen Access Card
    * **Aegis AI Response (Generated Text):** "Protocol Activated: Stolen Credential Alert. 1. Facial recognition mismatch detected with access card data. 2. Access immediately denied. 3. Security personnel notified with live camera feed and individual's last known location. 4. All access points temporarily locked for this credential."

#### Why "Aegis AI" is a Superior Project:

* **Highly Innovative:** It moves beyond simple facial recognition to a more holistic, AI-driven security assessment, which is at the forefront of the industry.
* **Greater "Wow" Factor:** The combination of real-time facial analysis, live digital footprint assessment, and interactive, AI-generated threat scenarios is far more engaging and impressive than a static database.
* **Ethically Sound:** By using consented data (pre-registered users or a volunteer's public profile with their permission), you avoid the ethical pitfalls of mass data scraping.
* **Higher Success Rate in a Live Demo:** The project is less dependent on the whims of external website structures. The core functionalities are self-contained, ensuring a smoother and more reliable demonstration.

 The roles and responsibilities for each of the four students working on the **"Aegis AI: Real-Time Threat Assessment and Anomaly Detection"** project.

Each role is designed to be distinct but interconnected, ensuring every member has a core domain of expertise while contributing to a unified, impressive final product.

---

### **Student 1: The DeepFace Lead & Project Manager(computer vision)**

This student is responsible for everything related to computer vision. They will build the system's "eyes" and its ability to understand faces and their expressions.

**Primary Goal:** To create a robust Python module that can analyze a live video stream and output structured data about the person in front of the camera.

**Specific Tasks:**

1.  **Environment Setup:** Install and configure all necessary computer vision libraries, including `OpenCV`, `DeepFace`, and its backends like `TensorFlow`. This is a critical first step.
2.  **Live Video Capture:** Write the Python script using `OpenCV` to access the webcam and display the live video feed.
3.  **Face Detection and Tracking:** Implement logic to reliably detect a face in the video stream frame-by-frame. The output should be a clean, cropped image of the face.
4.  **Identity Verification (`DeepFace.verify`):**
    * Build the function that takes the live facial crop and compares it against a target image.
    * This function will be used for two scenarios:
        * Matching against the pre-registered "authorized personnel" database.
        * Matching against the profile picture retrieved by the Selenium Lead.
    * The function must return a clear result: `Match` or `No Match`, and a confidence score.
5.  **Attribute Analysis (`DeepFace.analyze`):**
    * Build the function that takes the live facial crop and analyzes it to determine key attributes.
    * **Crucially, this must include real-time `emotion` analysis (e.g., "Happy", "Sad", "Anxious").** This is key for the anomaly detection feature.
    * It can also extract secondary attributes like apparent `age` and `gender` for a richer display.
6.  **Module Creation and Optimization:** Package all the above functionalities into a single, clean Python module (e.g., `vision_core.py`). This module will have functions that the Integration Lead can easily call (e.g., `getUserData()`) to get all the vision-based information in a simple format like a JSON object.
7.  **Specific Tasks (Project Manager):**

1.  **Project Planning:** Set up a shared project plan (using tools like Trello, Asana, or a simple spreadsheet) with clear deadlines for each task and deliverable.
2.  **Version Control:** Set up a team repository on **GitHub**. Enforce good practices so that everyone's code can be merged without conflicts.
3.  **Communication & Coordination:** Lead weekly meetings to sync up. You are the chief communicator, ensuring the GenAI lead knows what data to expect from the Selenium lead, and the UI lead knows the format of the data coming from the Integration lead. You resolve any "traffic jams" in the data flow.

**Key Deliverable:** A fully functional and visually impressive graphical user interface that serves as the face of the project, and a well-managed project plan that keeps the team on track.

**Key Deliverable:** A Python module that, when run, activates the camera and provides real-time data on facial identity and emotional state.

---

### **Student 2: The GenAI Lead (The AI)**

This student is the creative and linguistic core of the project. They will give "Aegis AI" its intelligence and its voice, making it seem like a truly thinking machine.

**Primary Goal:** To master a generative AI API and build a module that can generate intelligent security analyses and dynamic response protocols.

**Specific Tasks:**

1.  **API Setup:** Choose a generative AI model (like Google's Gemini or OpenAI's GPT series). Obtain an API key and write the basic Python script to send a prompt and receive a response.
2.  **Prompt Engineering for Threat Assessment:**
    * Design, test, and refine prompts that take unstructured text (e.g., the public information scraped by the Selenium Lead) as input.
    * The prompt should instruct the AI to act as a "Security Analyst" and identify any potential security risks in the provided text in a simulated manner.
3.  **Prompt Engineering for Scenario Response:**
    * This is the core of the "wow" factor. Create a set of prompts corresponding to the interactive threat scenarios (e.g., "Stolen Access Card," "Duress Situation," "Tailgating Alert").
    * These prompts will instruct the AI to generate a clear, step-by-step security protocol that is both realistic and impressive to a non-technical audience.
4.  **Module Creation:** Create a Python module (e.g., `genai_module.py`) that contains functions like `generateThreatAnalysis(text)` and `generateScenarioProtocol(scenario_name)`.
5.  **Collaboration:** Work closely with the UI/UX Lead to ensure the format of the generated text is clean and displays well in the final user interface.

**Key Deliverable:** A Python module that can be fed simple inputs (a block of text or a scenario name) and returns sophisticated, well-formatted security-related text.

---

### **Student 3: The Selenium & Integration Lead (The connetor)**

This student is the glue that holds the entire project together. They handle the interaction with the outside world (the web) and orchestrate the flow of data between all the other modules.

**Primary Goal:** To build the web automation scripts and the main application logic that connects the Vision, Brain, and UI components.

**Specific Tasks:**

1.  **Selenium Setup:** Install Selenium and the correct `WebDriver` for the browser you choose (e.g., ChromeDriver for Google Chrome).
2.  **Web Scraping for Verification:**
    * Write a Python script using Selenium that accepts a URL of a public profile (e.g., LinkedIn).
    * The script must automatically navigate to the page, robustly find the main profile picture's image element, and download it to a known location for the DeepFace Lead's module to use.
3.  **Web Scraping for Analysis:**
    * Expand the Selenium script to extract relevant public text from the profile. This text will be passed to the GenAI Lead's module.
4.  **The Main Application (`app.py`):** This is the most critical task. This student will write the central script that runs the entire application. The logic will be:
    * Initialize and start the Vision Core module.
    * Receive commands from the UI (e.g., "Start Verification for this URL" or "Simulate Scenario X").
    * Call the Selenium module when a URL is provided.
    * Send the scraped image path to the Vision Core for verification.
    * Send the scraped text to the GenAI module for analysis.
    * Send the final, consolidated data from all modules to the UI for display.
5.  **Error Handling:** Implement robust error handling. What happens if a website doesn't load or a profile picture can't be found? The application should fail gracefully, not crash.

**Key Deliverable:** A central `app.py` file that runs the entire project, and a `selenium_module.py` that handles all web interactions.

---

### **Student 4: The UI/UX (The overall integration guy )**

This student is responsible for the audience's experience and the project's overall success. They design how the project looks and feels, and ensure the team works together effectively.

**Primary Goal:** To design and build an impressive, clear, and interactive user interface, while managing the project's timeline and integration points.

**Specific Tasks (UI/UX):**

1.  **Interface Design:** Before writing any code, design mockups of the exhibition screen. Use a tool like Figma or even just paper sketches. Plan where the live video feed, the verification status, the emotion analysis, and the AI-generated text will go.
2.  **GUI Framework Selection & Development:**
    * Choose and learn a Python GUI framework. **Dash** or **Flask** are highly recommended as they create a web-based dashboard that looks modern and professional.
    * Develop the front-end code to create the visual layout.
    * Write the backend GUI code to display all the data coming from the Integration Lead's main app. The interface must update dynamically in real-time.
3.  **Interactivity:** Create the buttons and controls that allow the audience (or the presenter) to trigger the different threat scenarios for the GenAI to respond to.
