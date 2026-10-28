Internship Information Assistant - AI Engineering Project Scope

1. Project Name

Internship Information Assistant

2. Domain

Higher Education / Career Development / AI-Powered Information Retrieval

3. Problem Statement

University students need to understand internship requirements, application procedures, eligibility criteria, required documents, and reporting processes. However, this information may be published across different university and faculty webpages, guidelines, and downloadable documents. Students may need to consult multiple sources to find the information relevant to their faculty.

The Internship Information Assistant proposes a document-grounded AI question-answering system that helps students retrieve internship information from selected official university sources. The system will use Retrieval-Augmented Generation (RAG) to retrieve relevant information before generating an answer. Each answer should include its supporting source so that students can verify the information independently.

The proposed system is intended to support information retrieval, not replace official university staff or make internship placement decisions.

4. Evidence of the Problem

Evidence 1: Internship information is distributed across faculty resources.

The Universiti Teknologi Malaysia (UTM) Faculty of Electrical Engineering publishes industrial training information covering procedures, required forms, training processes, and contact information. This indicates that students need to consult faculty-specific resources for relevant internship guidance.

Source: UTM Faculty of Electrical Engineering - Industrial Training
https://fke.utm.my/li/

Evidence 2: Internship-related documents are published separately.

The UTM Faculty of Management provides an industrial training webpage containing multiple downloadable documents, including student details, reporting, and acceptance forms. The UTM Faculty of Chemical and Energy Engineering also publishes industrial training guidelines and forms through its download page.

Sources:

UTM Faculty of Management - Industrial Training: https://management.utm.my/industrial-training/
UTM Faculty of Chemical and Energy Engineering - Undergraduate Forms: https://fkt.utm.my/download/
Evidence limitation: These sources demonstrate that information is available across multiple webpages and documents. They do not, by themselves, prove that students experience significant difficulty finding it. Student interviews or a short survey could be conducted later to validate the problem.

5. Initial Related Work / Existing Approaches

Approach 1: Human Support from Industrial Training Coordinators

University faculty pages provide procedures, contact details, and guidance for students who need help with industrial training.

Source: UTM Faculty of Electrical Engineering - Industrial Training
https://fke.utm.my/li/

Key limitation: Students may need to identify the correct coordinator or contact the faculty to clarify information. This approach remains important for complex or exceptional cases but is not an automated, document-grounded question-answering service.

Approach 2: Static Webpages and Downloadable Guidelines

Universities publish industrial training information through webpages, PDF guidelines, and forms.

Sources:

https://management.utm.my/industrial-training/
https://fkt.utm.my/li/resources/
Key limitation: Students may need to navigate several pages or documents and manually identify the relevant information. Different faculties may also have different requirements, so information must be interpreted in the correct context.

Approach 3: Retrieval-Augmented Generation (RAG) Chatbots for Education

Swacha and Gracel (2025) reviewed educational RAG chatbot applications and discussed their uses, evaluation methods, and limitations.

Reference: Swacha, J., & Gracel, M. (2025). Retrieval-Augmented Generation (RAG) Chatbots for Education: A Survey of Applications. Applied Sciences, 15(8), 4234.
https://doi.org/10.3390/app15084234

Key limitation: RAG does not guarantee that the system retrieves the most relevant passage or generates an answer that accurately reflects the retrieved information. The proposed assistant must therefore be evaluated for answer correctness, source relevance, and groundedness.

Additional Relevant Study

Yafie et al. (2026), Academic Chatbot for Campus Information Services Using Retrieval-Augmented Generation, discusses document retrieval and answer generation for campus information services.

Source: https://jurnal.polgan.ac.id/index.php/sinkron/article/view/16088

Relevance and limitation: This work supports the feasibility of applying RAG to university information services. However, a campus information chatbot is not necessarily designed specifically for internship procedures, faculty-specific eligibility, or internship document requirements.

6. Engineering Gap / Limitation

Existing approaches provide human support, static documents, or general document-grounded chatbot capabilities. The proposed project will investigate a focused internship assistant that retrieves answers from selected official university sources and displays the supporting source for verification.

The main engineering challenge is to ensure that the system retrieves information from the correct faculty and document, avoids combining conflicting requirements, and does not invent information when the answer cannot be found in the available sources.

The project contribution is the implementation and evaluation of a focused, source-attributed internship information assistant. It does not claim to invent a new RAG algorithm.

7. Initial Project Objectives

O1: To collect and organise publicly accessible internship guidelines, procedures, and forms from selected official UTM webpages.

O2: To develop a prototype AI question-answering assistant that retrieves relevant information from the selected documents and provides answers with source references.

O3: To evaluate the prototype using a predefined set of internship-related questions based on answer correctness, source relevance, groundedness, response time, and appropriate handling of questions that cannot be answered from the available documents.

8. Target Users

The primary target users are UTM undergraduate students who need information about industrial training or internship requirements.

The initial prototype will focus on a selected set of publicly accessible UTM sources. Where requirements differ between faculties, the assistant must identify the applicable faculty or source instead of presenting one faculty's requirements as universal UTM policy.

9. Data Sources

The initial document collection will use the following public sources:

Source 1: UTM Faculty of Electrical Engineering - Industrial Training
URL: https://fke.utm.my/li/
Planned use: Procedures, training requirements, forms, and relevant contact information.

Source 2: UTM Faculty of Management - Industrial Training
URL: https://management.utm.my/industrial-training/
Planned use: Publicly available industrial training forms and supporting documents.

Source 3: UTM Faculty of Chemical and Energy Engineering - Undergraduate Forms
URL: https://fkt.utm.my/download/
Planned use: Publicly available industrial training guidelines and forms.

Data preparation plan:

Identify relevant documents and their publication dates, where available.
Download or extract only documents that are publicly accessible and permitted for project use.
Record the source URL, faculty, document title, and date or version where available.
Separate documents by faculty to reduce the risk of mixing requirements.
Use the source collection to create a test set of questions with answers verified against the original documents.
These are initial sources. Their current relevance, accessibility, and suitability for the final prototype must be checked before implementation. Public accessibility does not automatically grant permission to redistribute copyrighted documents.

10. Similar to EduAdvisor

Both projects use AI to answer student questions based on official university information. Both aim to improve access to information, retrieve relevant passages from documents, and evaluate answer quality, source grounding, and response time.

11. Different from EduAdvisor

EduAdvisor focuses on academic advising, including course information, prerequisites, and graduation requirements. The Internship Information Assistant focuses on industrial training and internship information, including application procedures, eligibility, required forms, reporting procedures, and faculty-specific requirements.

Its initial knowledge base will be limited to selected public internship-related documents rather than general university academic information.

12. Responsible AI Risks

Risk 1: Hallucination or Unsupported Answers

The assistant may generate incorrect eligibility criteria, deadlines, procedures, or required documents.

Mitigation: Require answers to be supported by retrieved source passages. If relevant information cannot be found, the system should clearly state that it cannot verify the answer and direct the student to the relevant official source or coordinator.

Risk 2: Outdated Information

A guideline or form may be superseded by a newer version.

Mitigation: Record document dates and source URLs, prioritise the most recent verified version where possible, and display the source information so students can check the original document.

Risk 3: Conflicting Faculty Requirements

Different faculties may have different internship requirements. The system may incorrectly apply one faculty's rules to another.

Mitigation: Store faculty metadata, identify the relevant faculty when answering, cite the specific source, and ask a clarification question when the faculty is unknown and materially affects the answer.

Risk 4: Privacy and Data Protection

Students may enter personal information such as identification numbers, contact details, or application information into the chatbot.

Mitigation: Inform users not to submit sensitive personal information, avoid collecting unnecessary user data, and do not store chat logs containing personal information unless there is a justified and approved need.

13. Initial Evaluation Plan

The prototype will be evaluated using a manually prepared test set of internship-related questions whose expected answers are verified against the original documents.

Proposed evaluation measures:

Answer correctness: Whether the answer matches the information in the verified source.
Source relevance: Whether the cited document or passage supports the answer.
Groundedness: Whether the generated answer stays within the retrieved evidence.
Response time: The time taken to produce an answer.
Abstention behaviour: Whether the system correctly acknowledges missing or unverifiable information rather than inventing an answer.
A baseline comparison may be conducted against manual searching of the same official documents, using task completion time and answer correctness where feasible.

14. Initial Scope and Constraints

The project will begin with a small collection of public internship documents and a limited set of common questions. It will not automatically apply for internships, rank employers, guarantee placements, or make official eligibility decisions.

The scope, data sources, architecture, and evaluation criteria will be refined in Topic 2.
