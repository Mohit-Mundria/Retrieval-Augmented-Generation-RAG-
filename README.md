# Agentic-RAG_system
📚 Legal RAG System for Indian Labour & IT Laws

Retrieval-Augmented Generation (RAG) system powered by Indian legal documents.

This project combines vector-based semantic search and a generative LLM to answer questions about Indian Labour Laws, IT Act 2000, Intermediary Rules 2021, and other legal acts—without hallucination or generic output. Just real legal insight, sourced directly from the law.

⚙️ What This Project Is

A small but complete RAG pipeline built for learning (and also useful enough that you can demo it with confidence). It answers legal queries using:

A FAISS vector store for efficient similarity search

Gemini 2.5 Flash for summarization and response synthesis

Gemini text embedding model for vectorization

Indian Government legal PDFs as data sources

🎯 Key Features

Semantic search over real legal documents (not mock text).

Full RAG architecture using FAISS + Gemini models.

Implementation suitable for production scaling: modular, stateless generative calls, explicit chunking strategies.

Support for multiple legal sources including:

The Information Technology Act, 2000

IT Intermediary Guidelines Rules, 2021

Labour Laws in India (Compilation)

Social Security Code, 2020

Code on Wages, 2019

Companies Act summaries

Clean abstraction between indexing and querying.

🧠 Architecture Overview

Document Loading – Parse PDFs and handle metadata extraction.

Chunking & Preprocessing – Split text into meaningful chunks.

Vector Embeddings – Generate embeddings using Gemini’s embedding model.

FAISS Vector Indexing – Approximate nearest neighbor search for scalability.

Query Pipeline – Encode user query, retrieve relevant chunks, and feed into LLM for generation.

Response Generation – Use Gemini 2.5 Flash for grounded outputs based on retrieval context.

🚀 Getting Started
1. Clone and Install
git clone <your_repo_url>
cd <repo>
pip install -r requirements.txt

2. Add Your Gemini API Key

Set environment variable:

export GOOGLE_API_KEY="your_key_here"

3. Run Indexing

Use RAG_system.ipynb notebook or a Python script if included:

# In notebook or script
from src.loader import load_pdfs
from src.embedder import embed_docs
from src.vector_store import build_faiss_index

docs = load_pdfs("data/")
embeddings = embed_docs(docs)
build_faiss_index(embeddings)

4. Query the System
from src.retrieval import retrieve
from src.generator import generate_answer

query = "What are the penalties under the IT Act 2000 for tampering with computer source code?"
results = retrieve(query)
response = generate_answer(query, results)
print(response)

📊 Performance Tips

Use chunk sizes based on semantic structure (e.g., sections of laws) instead of fixed tokens.

Track retrieval overlap to detect redundancy.

Consider adding reranking with cross-encoders if hallucinations sneak in.

If FAISS performance drops on large datasets, switch to HNSW index or run on GPU.

🧾 Data Sources

All documents are official gazetted acts and legal summaries from:

Ministry of Law & Justice (India)

Government PDFs included under /data/

References:
https://www.cert-in.org.in/

https://ncib.in/pdf/ncib_pdf/Labour%20Act.pdf

https://www.wisemonk.io/blogs/hr-policies-in-india

https://www.skyflow.com/whitepapers/indias-dpdp-passed-ease-compliance-with-skyflow?qgad=777557598363&qgterm=dpdp%20compliance&kw=dpdp%20compliance&cpn=23082497031&utm_agid=186994677536&creative=777557598363&extension_id=&device=c&utm_term=dpdp%20compliance&utm_campaign=APAC:Search:HI:DPDP:MaxConv&utm_source=google&utm_medium=ppc&utm_content=DPDP+Compliance&utm_content=DPDP+Compliance&hsa_acc=6575335991&hsa_cam=23082497031&hsa_grp=186994677536&hsa_ad=777557598363&hsa_src=g&hsa_tgt=kwd-2261862527001&hsa_kw=dpdp%20compliance&hsa_mt=p&hsa_net=adwords&hsa_ver=3&gad_source=1&gad_campaignid=23082497031&gbraid=0AAAAABzDxWpHLEg1_PqW-12rpRWIFZAQt&gclid=CjwKCAiAw9vIBhBBEiwAraSATqrYPOeCWgP9t-YlhaHfPbsbWkvQASoF3MDkMrGsxUFUUpFY2IHFCxoC_8MQAvD_BwE

https://www.cert-in.org.in/PDF/Guidelines_for_Smart_City_Infrastructure.pdf

https://iclg.com/practice-areas/data-protection-laws-and-regulations/india

https://www.greythr.com/wiki/acts/shops-and-establishments-act-india/

https://www.meity.gov.in/static/uploads/2024/06/2bf1f0e9f04e6fb4f8fef35e82c42aa5.pdf

https://www.lawrbit.com/article/shops-establishment-act/

https://www.indiacode.nic.in/bitstream/123456789/2187/2/A187209.pdf

https://www.indiacode.nic.in/bitstream/123456789/2013/3/A2006-27.pdf

https://www.mkgeducation.com/uploads/1/8/0/4/18040539/list_of_important_sections__based__on_companies_act_with_complete_summary_of_companies_act_part_2.pdf

https://icmai.in/TaxationPortal/upload/IDT/Article_GST/113_1803_21.pdf

https://www.cert-in.org.in/PDF/CERT-In_Directions_70B_28.04.2022.pdf

https://www.meity.gov.in/static/uploads/2024/02/IT-Intermediary-Rules-2021-updated-on-28.10.2022-2.pdf

https://www.meity.gov.in/static/uploads/2024/06/2bf1f0e9f04e6fb4f8fef35e82c42aa5.pdf

⚠️ Disclaimer

This project does not provide legal advice. It provides legal information extracted from official acts using automated retrieval. Always consult a qualified legal professional for real legal matters.