# AIVO: Advanced Intelligent Virtual Orator 🤖🎙️

**Authors:**
* MOHAMMED HISHAM (CHN21CS085)
* DIANA LIZ KURIAKOSE (CHN21CS046)
* MARIA JOSHY (CHN21CS080)
* NANDANA VINOD (CHN21CS094)

**Institution:** College of Engineering Chengannur (Affiliated to APJ Abdul Kalam Technological University - KTU)

## 🎯 Overview

AIVO (Advanced Intelligent Virtual Orator) is an innovative "digital professor" designed to streamline and enhance the learning process for 3rd-year B.Tech students at Kerala Technological University (KTU). In the demanding academic environment of KTU, students often struggle with limited time, scattered resources, and the need for concise, syllabus-aligned content for effective exam preparation.

AIVO addresses these challenges by integrating curated notes, past question papers, and verified solutions into a comprehensive, interactive platform. It aligns rigorously with the official KTU syllabus, ensuring students receive relevant, exam-focused content, presented with the clarity and structure of a dedicated professor.

## ❗ Problem Statement

Third-year B.Tech students at KTU face significant difficulties in:
* Accessing and organizing study materials relevant to their specific syllabus.
* Finding concise, exam-focused content amidst an overwhelming amount of unstructured resources.
* Preparing effectively for exams within short semester timeframes.
* Lacking a centralized, reliable system for syllabus-specific queries.

This leads to inefficient use of study time and increased academic stress.

##💡 Proposed Solution: AIVO

AIVO acts as a digital professor offering personalized, curriculum-specific assistance. Key aspects of the solution include:

* **Curriculum-Specific Focus:** Delivers precise, curated information aligned strictly with the KTU syllabus, unlike general-purpose AI tools.
* **Voice Interaction:** Integrates advanced voice-to-text (Whisper AI) and text-to-voice (Kokoro) capabilities, allowing natural spoken dialogues for enhanced accessibility and engagement.
* **Retrieval-Augmented Generation (RAG):** Utilizes vector embeddings and semantic search to retrieve the most relevant context from KTU-specific documents before generating answers with a powerful language model.

## ✨ Key Features

* **KTU-Specific Content:** Access curated lecture notes, past question papers, and verified solutions aligned with the KTU 3rd-year syllabus.
* **Syllabus-Aligned & Exam-Focused:** Content is structured for effective exam preparation.
* **Interactive Chatbot:** Ask questions via text or voice and receive immediate, relevant answers.
* **Voice-to-Text Input:** Use your voice to ask questions (powered by Whisper AI).
* **Text-to-Voice Output:** Listen to answers and study materials (powered by Kokoro).
* **Organized Resources:** Browse materials easily, filtered by academic year, branch, and subject. (See Screenshots below)
* **Semantic Search:** Understands the meaning behind queries to retrieve the most relevant information using vector embeddings.
* **Offline Voice Capabilities:** Core voice features (Whisper, Kokoro) run offline for reliability.

## 🏗️ System Architecture

AIVO employs a Retrieval-Augmented Generation (RAG) pipeline:

1.  **Data Collection:** Gathering KTU syllabus documents, notes, past papers.
2.  **Preprocessing:** Converting data (e.g., PDFs) to Markdown format and cleaning it.
3.  **Vector Embedding:** Using `BAAI/bge-large-en-v1.5` to create semantic vector representations (1024 dimensions) of the data chunks.
4.  **Vector Storage:** Storing embeddings efficiently in `Milvus DB` for fast retrieval.
5.  **Query Processing:**
    * User query (text/voice) is converted to a vector embedding.
    * `Milvus DB` performs a similarity search to find the top relevant document chunks.
6.  **Answer Generation:** The retrieved chunks provide context to the `Qwen 2.5 32b` Large Language Model (via Hugging Face Inference API) to generate a comprehensive, accurate answer.
7.  **Output:** The answer is presented as text and optionally converted to speech using `Kokoro`.
8.  **Interface:** A web-based frontend (HTML, CSS, JS) interacts with the Python backend (Flask) via APIs.

*(Refer to Figure 4.1 in the project report for a visual diagram)*

## 🛠️ Tech Stack

* **AI Models:**
    * **Language Model:** Qwen 2.5 32b (Alibaba Cloud via Hugging Face)
    * **Embedding Model:** BAAI/bge-large-en-v1.5
    * **Speech-to-Text:** Whisper Large (OpenAI via Hugging Face)
    * **Text-to-Speech:** Kokoro
* **Vector Database:** Milvus
* **Backend:** Python (3.10+), Flask, PyTorch
* **Frontend:** HTML5, CSS3, JavaScript, Fetch API
* **Libraries:** Hugging Face Transformers
* **Tools:** Docker (for Milvus deployment, potentially application), FFmpeg (audio processing dependency for Whisper)

## 🖼️ Screenshots

*(Screenshots from the project report showing the Home Page, Ask AIVO interface, and Resource navigation by Branch, Semester, and Subject)*

* Figure 5.3: Home page
* Figure 5.4: Ask AIVO interface
* Figure 5.5: Branch Selection
* Figure 5.6: Semester Selection
* Figure 5.7: Subject Resources

## ⚙️ Installation & Setup

**(Note:** These are inferred steps based on the tech stack. Update with specific instructions for your repository.)

1.  **Prerequisites:**
    * Git
    * Python 3.10+ and Pip
    * Docker and Docker Compose
    * FFmpeg (required by Whisper) - Install via your system's package manager (e.g., `sudo apt update && sudo apt install ffmpeg` on Debian/Ubuntu, `brew install ffmpeg` on macOS).

2.  **Clone the repository:**
    ```bash
    git clone [https://github.com/Hisham1404/AIVO.git](https://github.com/Hisham1404/AIVO.git)
    cd AIVO
    ```

3.  **Set up Vector Database (Milvus):**
    * Use the official Milvus Docker Compose file or adapt one for this project.
    * Start Milvus: `docker-compose up -d` (Refer to Milvus documentation)

4.  **Create Python Virtual Environment:**
    ```bash
    python -m venv venv
    # On Windows
    venv\Scripts\activate
    # On macOS/Linux
    source venv/bin/activate
    ```

5.  **Install Python Dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
    

6.  **Configuration:**
    * Create a `.env` file (copy from a `.env.example` if provided).
    * Add necessary configurations:
        * Milvus connection details (Host, Port)
        * Hugging Face API Token (if using Inference API for Qwen/Whisper)
        * Paths to local models if not using APIs
        * Flask specific settings (e.g., `FLASK_APP`, `FLASK_ENV`)
        * Other settings

7.  **Data Loading & Embedding (Run necessary scripts):**
    * You'll likely need a script to:
        * Load your preprocessed Markdown data.
        * Chunk the data (respecting model token limits).
        * Generate embeddings using `BAAI/bge-large-en-v1.5`.
        * Insert the embeddings into your Milvus collection.
    * Example : `python load_data.py --data_dir path/to/markdown/files`

8.  **Run the Backend Server:**
    
        ```bash
        # On Windows
        set FLASK_APP=server.py
        # On macOS/Linux
        export FLASK_APP=your_main_script.py
        ```
        
    * Run the Flask development server:
        ```bash
        flask run --host=0.0.0.0 --port=8000
        ```
        

9.  **Access the Frontend:**
    * Open your web browser and navigate to `http://localhost:8000`.

## ▶️ Usage

1.  Open the AIVO web application in your browser.
2.  Navigate through the **Resources** section to find study materials organized by Branch, Semester, and Subject.
3.  Use the **Ask AIVO** interface:
    * Type your question related to the KTU syllabus into the chatbox.
    * Alternatively, click the microphone icon (if implemented) to ask your question using voice (requires microphone permission).
4.  Receive the answer in text format.
5.  Click the speaker icon (if implemented) to hear the answer read aloud.

## 💡 Development Insights

The project overcame several technical hurdles:
* Initial attempts using fine-tuned Llama 3.2 3b yielded low accuracy for the specific KTU context.
* Using ChromaDB with Nomic Embed text (768 dimensions) also resulted in low retrieval accuracy.
* **Successful Approach:** Switched to Milvus DB for robust vector storage and BAAI/bge-large-en-v1.5 (1024 dimensions) for higher-quality embeddings, significantly improving retrieval. Adopted the powerful Qwen 2.5 32b model for generation without needing fine-tuning for this task.

## 🚀 Future Scope

Planned enhancements include:
* **Image-to-Text (OCR):** Analyze diagrams, equations, and handwritten notes from images.
* **Handwritten Content Support:** Interpret complex handwritten equations.
* **Expanded Knowledge Base:** Integrate more research papers, textbooks, and tutorials.
* **Multimodal Input:** Allow uploading documents alongside text/voice queries.
* **Adaptive Learning:** Personalize responses and suggest resources based on user interaction.
* **LMS Integration:** Embed AIVO directly into KTU's learning management system.
* **Offline Features:** Provide access to core features without internet connectivity.
* **Performance Optimization:** Improve response time and scalability.
* **AI-Assisted Forum:** Facilitate doubt resolution and peer discussion.

## 🤝 Contributing

Contributions are welcome! Please follow standard GitHub practices:

1.  Fork the repository.
2.  Create a new branch (`git checkout -b feature/YourFeatureName` or `bugfix/IssueDescription`).
3.  Make your changes (write clear code, add comments).
4.  Commit your changes (`git commit -m 'Add some amazing feature'`).
5.  Push to the branch (`git push origin feature/YourFeatureName`).
6.  Open a Pull Request with a clear description of your changes.

## 🙏 Acknowledgements

* Guidance from Project Coordinator Smt. Syama S, Assistant Professor, College of Engineering Chengannur.
* College of Engineering Chengannur for providing facilities and support.
* Authors of referenced papers and creators of the open-source models and tools used.
* A survey paper based on the initial research for this project was published:
    * *Mohammed Hisham, Nandana Vinod, Diana Liz Kuriakose, Maria Joshy, Syama S. "Survey on Generative AI in Education." International Journal of Advances in Engineering and Management (IJAEM), Volume 6, Issue 11, pp: 615-620, Nov. 2024.* ([Link](https://www.ijaem.net/issue_dcp/Survey%20on%20Generative%20AI%20in%20Education.pdf))

## 📞 Contact

Project Link: [https://github.com/Hisham1404/AIVO](https://github.com/Hisham1404/AIVO)

*(Optional: Add contact details for the authors/maintainers)*
