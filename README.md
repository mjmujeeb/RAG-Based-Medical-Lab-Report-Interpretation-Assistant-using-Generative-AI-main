RAG-Based Medical Lab Report Interpretation Assistant

A notebook-based project that combines rule-based analysis with Retrieval-Augmented Generation (RAG) to explain medical laboratory results in a more structured and understandable way.

The system evaluates selected laboratory parameters, identifies possible abnormal patterns, retrieves relevant medical context, and uses a language model to produce a structured explanation.

«Important: This project is an educational and experimental system. Its output is not a medical diagnosis and should not replace evaluation by a qualified healthcare professional.»

Overview

Laboratory reports often contain several measurements that need to be interpreted together rather than individually. This project explores a hybrid approach in which predefined clinical rules identify potential abnormalities, while a retrieval and language-generation pipeline provides additional context.

The system is designed to keep the initial findings separate from the generated explanation. This helps make the reasoning process easier to inspect.

How It Works

The project follows a hybrid analysis pipeline:

1. Input laboratory values – laboratory measurements are supplied as structured data.
2. Rule-based evaluation – dedicated analysis modules examine selected groups of parameters.
3. Medical document retrieval – relevant text is retrieved from a medical knowledge collection.
4. Context preparation – verified rule-based findings and retrieved information are combined.
5. Language model processing – the model generates a structured explanation.
6. Structured output – the response is organized into findings, interpretation, risk level, and recommendations.

Analysis Modules

The notebook contains rule-based modules covering:

- Diabetes-related parameters
- Complete blood count (CBC)
- Thyroid function
- Lipid profile
- Vitamins and micronutrients
- PCOS/PCOD-related parameters
- Liver function
- Kidney and renal function

The modules use parameter-specific checks and predefined thresholds. The results should be treated as preliminary indicators, not confirmed diagnoses.

RAG Pipeline

The retrieval component uses the following workflow:

"Medical text → Text splitting → Embeddings → FAISS vector store → Retrieval → LLM"

The notebook uses:

- RecursiveCharacterTextSplitter for document chunking
- Hugging Face "BAAI/bge-base-en-v1.5" embeddings
- FAISS for vector similarity search
- A retriever configured to return relevant context
- Mistral 7B Instruct for response generation

The language model receives the retrieved context together with the rule-based findings. The prompt instructs it not to change verified findings or introduce unsupported laboratory values.

Technology Stack

Component| Technology
Language| Python
Notebook environment| Google Colab
Retrieval framework| LangChain
Embeddings| Hugging Face
Vector database| FAISS
Language model| Mistral 7B Instruct
Model execution| Transformers, PyTorch
Data processing| Python dictionaries and JSON

Getting Started

1. Clone the repository

git clone https://github.com/mjmujeeb/RAG-Based-Medical-Lab-Report-Interpretation-Assistant-using-Generative-AI-main.git
cd RAG-Based-Medical-Lab-Report-Interpretation-Assistant-using-Generative-AI-main

2. Open the notebook

Open "Copy_of_gen_ai_2.ipynb" in Google Colab.

You can also open it directly from the repository using the Colab interface.

3. Install dependencies

Run the installation cell:

!pip install -q langchain langchain-community faiss-cpu sentence-transformers transformers accelerate bitsandbytes

4. Upload the required medical text

The notebook uses Google Colab's file upload interface to load the medical text used by the retrieval pipeline.

5. Run the notebook

Execute the cells in order:

- Prepare and process the medical text.
- Create document chunks.
- Generate embeddings.
- Build the FAISS vector store.
- Load the language model.
- Run the rule-based analysis modules.
- Retrieve relevant context and generate the final structured response.

A compatible runtime with sufficient memory is recommended for loading the language model.

Example Input

The notebook demonstrates structured laboratory input using values such as:

labs = {
    "fbs": 165,
    "creatinine": 1.6,
    "egfr": 52,
    "urine_acr": 120,
    "vitamin_d": 18,
    "b12": 240,
    "ldl": 170,
    "hdl": 35,
    "triglycerides": 210
}

The analysis pipeline processes the supplied values and prepares a structured response.

These are demonstration values, not a real patient's report.

Example Output Structure

The generated response is designed around four sections:

- Findings: relevant observations from the rule-based analysis.
- Clinical interpretation: contextual explanation of the findings.
- Risk level: an indicative assessment based on the system's rules.
- Recommendations: suggested next steps for discussion with a healthcare professional.

Limitations

- The accuracy of the output depends on the quality and completeness of the supplied laboratory values and retrieved documents.
- Rule-based thresholds may not account for every patient-specific factor or laboratory reference range.
- Language models can generate incorrect or incomplete explanations.
- The retrieval collection may not cover every medical topic.
- The project has not been established as a clinically validated diagnostic system.

Future Improvements

- Add support for direct PDF laboratory report extraction.
- Expand and validate the medical reference collection.
- Improve source attribution for retrieved medical information.
- Add patient-specific reference ranges where appropriate.
- Evaluate the system against expert-reviewed examples.
- Improve error handling and structured output validation.

License

See the "LICENSE" file in this repository.
