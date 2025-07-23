# Transforming Teacher Workflow and Student Feedback with Applied AI

## The Business Context & The Strategic Challenge
Jangmoon is a fast-growing ed-tech startup in South Korea with over 8,000 students, focused on preparing high schoolers for the competitive national college entrance exam. As a backend engineer, I proactively analyzed our existing workflows to identify areas for improvement.

A significant bottleneck was our homework review process. Students submitted video explanations of their solutions to complex problems (e.g., "applications of trigonometric functions"), and assistant teachers had to manually watch and evaluate each video. This process was not only time-consuming and difficult to scale but also lacked consistent, detailed feedback for every student. I saw a clear opportunity to leverage AI to automate this process, enhancing both teacher efficiency and the student learning experience.

## My Role: From Engineer to End-to-End Project Owner
This project was entirely self-initiated. I identified the problem, defined the project scope, and took complete ownership from conception to deployment. Acting as the sole engineer and de facto project manager, I was responsible for everything: initial proof-of-concept (PoC), technology selection, system architecture, development, and collaborating directly with teachers to define the AI's evaluation standards.

## The Action: A Pragmatic Approach to Building a Production-Ready AI
Building a reliable AI evaluation system required a series of pragmatic decisions and iterative development:

* __Cost-Effective Transcription__: I initially explored OpenAI's Whisper for video transcription due to its powerful prompting features. However, I determined it was too costly for production scale. I pivoted to a more economical solution: extracting YouTube's auto-generated captions via their API and then using the more affordable gpt-4o-mini model to refine and correct the text.

* __Iterative Prompt Engineering__: My first attempt involved feeding the LLM the raw textbook content alongside the student's transcript for evaluation. This proved ineffective, as the AI lacked specific guidance.

* __Co-creating Evaluation Criteria__: The breakthrough came from collaborating closely with experienced teachers. Together, we distilled the evaluation logic for each topic into 5-6 precise, true/false criteria (e.g., "Did the student correctly explain concept A as B?"). This structured approach gave the AI a clear, consistent framework for assessment.

## Technical Implementation Details
The final system was a two-stage AI pipeline designed for accuracy and depth of feedback:

* Stage 1: Criteria-Based Assessment: The student's refined transcript was fed to the powerful gpt-4o model. Its primary task was to assess the explanation against the pre-defined, teacher-developed true/false criteria. This ensured the core concepts were covered correctly.

* Stage 2: Personalized Feedback Generation: Based on the outcome of the initial true/false assessment, the system would then generate detailed, constructive feedback. It highlighted areas of misunderstanding and suggested specific improvements to the student's explanation and problem-solving approach.

As a solo developer and not a formal AI expert, I navigated the project's challenges by continuously researching best practices from tech blogs and applying them through rapid trial-and-error cycles.

## Technology Stack
Languages: Python
AI/ML: OpenAI API, Gemini API
Databases & Tools: MongoDB, Github Actions

## The Results: Enhancing Education and Unlocking New Opportunities
The AI evaluation system delivered significant value across the board:

* Teacher Empowerment: Teachers were thrilled with the reduction in tedious review work, allowing them to focus on more impactful student interactions.

* Improved Academic Integrity: The system effectively filtered out irrelevant or low-effort submissions, ensuring students engaged meaningfully with the material to pass.

* Enhanced Student Experience: Students appreciated the immediate, detailed feedback and were excited to be using cutting-edge AI technology in their studies.

Crucially, this project became a new marketing tool for Jangmoon to attract prospective students. Its success also directly led to the planning of a new strategic project focused on tracking student test scores to suggest personalized learning paths.

## Key Takeaways
This was my first startup experience, and it was incredibly impactful. Unlike in larger organizations where tasks are often delegated, I had the unique opportunity to identify a real-world problem, define it, and build a solution from the ground up. Actually building and shipping a production-ready LLM application in 2024, a landmark year for the technology, was a significant personal and technical achievement that has sparked a deeper interest in pursuing AI. This end-to-end problem-solving experience was invaluable.
