# Aegis-AI
Aegis AI: A live AI security demo. Using DeepFace, it verifies identity and analyzes emotion for duress detection. Selenium enables real-time web profile matching. A GenAI instantly creates security protocols for audience-suggested threats, fusing computer vision, web automation, and generative AI.
I UNDERSTAND THAT THE DESCRIPTION IS PRETTY LONG BUT I SUGGEST THAT YOU READ IT.


Of course. A clear and detailed workload division is crucial for a team project's success. Here is a more granular breakdown of the roles and responsibilities for each of the four students working on the **"Aegis AI: Real-Time Threat Assessment and Anomaly Detection"** project.

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
