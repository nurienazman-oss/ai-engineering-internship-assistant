**Internship Information Assistant**

An AI Engineering semester project that helps university students find internship and industrial training information from selected official university documents.

**Problem Statement**

Internship information may be published across different university webpages, guidelines, and forms. Students may need to consult multiple sources to find information relevant to their faculty.

The Internship Information Assistant aims to answer common internship-related questions using Retrieval-Augmented Generation (RAG) and provide source references so users can verify the answers.

**Objectives**

1. Organise selected public internship documents from official university sources.  
2. Develop a document-grounded question-answering prototype with source references.  
3. Evaluate answer correctness, source relevance, groundedness, response time, and handling of unanswerable questions.

**Target Users**

University undergraduate students seeking information about internship or industrial training requirements.

Initial Data Sources

* Faculty of Artificial Intelligence (FAI)  
* Razak Faculty of Technology and Informatics 
* Malaysia-Japan International Institute of Technology 

The source collection is preliminary. Documents will be checked for relevance, version, and permitted use before implementation.

**Planned Methodology**

1. Collect and inspect selected public documents.  
2. Extract and organise document text with source metadata.  
3. Retrieve relevant passages for user questions.  
4. Generate answers grounded in the retrieved passages.  
5. Display source references and handle unsupported questions safely.  
6. Evaluate the prototype using a predefined question set.

**Evaluation**

The initial evaluation will consider answer correctness, source relevance, groundedness, response time, and appropriate abstention when the available documents do not contain the answer.

**Responsible AI Considerations**

* Prevent unsupported or fabricated answers.  
* Identify outdated information.  
* Avoid mixing requirements across faculties.  
* Minimise the collection of personal information.  
* Direct students to official sources for confirmation.

**Project Structure**

* docs/ \- project scope, requirements, and documentation  
* data/ \- data documentation and permitted project data  
* src/ \- application and retrieval code  
* notebooks/ \- experiments and exploratory analysis  
* evaluation/ \- test questions, reference answers, and evaluation results  
* prompts/ \- prompt versions and instructions

**Project Status**

Week 1: Initial project scoping and repository setup.

This project is an academic prototype and is not an official university service.

