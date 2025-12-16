# ✈️ TravelRAG A Retrieval-Augmented Travel Assistant

### Project Description
TravelRAG Assistant is an interactive assistant that allows users to ask travel-related questions and receive responses grounded in real sources like:
Travel guides from National Geographicr
Destination overviews from professional advisors
Travel tips and recommendations from recognized travel Bloggers
The app used a Retrieval-Augmented Generation (RAG) pipeline built with CrewAI, DuckDB, and Sentence Transformers, ensuring responses are informed by relevant source material rather than generic knowledge.

## Domain Overview and Problem Statement
I have always enjoyed traveling and getting to discover new places. What I don't enjoy as much is the planning. From a personal standpoint, travel planning has always felt fragmented to me. Particularly, it feels hard to know where to start. The information is spread across blogs, PDFs, guides, review sites, and youtube videos which makes it difficult to get clear and reliable answers that truly target my needs and aspirations as a traveler. With the rise of AI and chatbots like ChatGPT and Gemini, it seemed like there finally was a centralized place to start, but instead, I found myself getting generic answers and even fake information (given often hallucinations) leading to surface-level advice without grounding responses in real sources.
Faced with this issue, I decided to build TravelRAG, which serves as a retrieval-augmented travel assistant that provides source-grounded travel recommendations using modern NLP techniques. 
The benefit of opting for this model, is that rather than relying purely on a language model’s internal knowledge (which is exactly the issue I found with traditional chatbots), TravelRAG retrieves relevant information from a curated travel document collection and uses that context to generate accurate responses.

## Document Collection Summary
Curating Travel Database → The first step to construct the Travel RAG was to gather sources that would inform the chatbot. These documents were gathered from trusted and diverse travel resources to have sufficient information that caters to the needs of different travelers. In order to do this, the main focus was on sources that recommended destinations, as the starting point often feels like the hardest decision to make. To do this, I included general recommendations like articles recommending top travel destinations for 2026 as well as destinations ideal for specific seasons, different types of travelers (luxury, backpacking, foodies, group trips), while always seeking to have geographic diversity (including recommendations from every continent). Below is the full list of documents that were used. Each document is then broken into smaller text chunks so that the system can retrieve specific, relevant passages instead of entire articles.
![Documents in Database](backend/images/documents.png)

## Agent Configuration
Once top documents  are selected they are passed to the CrewAI based agent which is responsible for generating the final response. This agent was intentionally configured to serve the purpose of being a travel centered RAG, with a defined role, goal and backstory to guide its behaviours:
- Role → _“Travel Destination Recommendator Assistant”_: The agent is a guide that allows users to explore and compare travel destinations using curated materials without committing to detailed planning or logistics.
- Goal → _“Answer questions about travel destination recommendations using the database to build ideal itineraries”_: The primary goal of the agent is to help users overcome what I consider the hardest part of planning: choosing a destination. By offering evidence-based recommendations, the system looks to identify suitable travel destinations that fit their interests and based on these recommendations, suggest high-level itineraries that illustrate how a trip might be structured. It is important to highlight that this system is not designed to generate fully detailed travel plans with bookings, schedules, or logistics, but rather to serve as an informed starting point in the travel planning process.
- Backstory → _“You are a travel expert who has access to a database with content about travel destinations. You want to provide a variety of options in terms of destinations depending on the user preferences and build ideal high level itineraries to fit traveler needs”_: The backstory defines this agents as a travel expert with access to a curated database of travel content, which reinforce evidences based recommendation and discourage false or overly detailed outputs.

### Architecture Diagram
The TravelRAG built follows the following architecture:
![Architecture](backend/images/IMG_0778.png)

**1. Query Input:** User enters a travel related question (destination ideas, seasonal recommendations, etc)

**2. Retrieval of Relevant Information:** Considering the question, relevant information is looked up in a previously built database (duckdb database) . Identified chucks with similar semantics are selected.  

**3. Selected Knowledge Strips:** The chunks are sorted in descending similarity scores. Only k results per query (as set by the user) are passed to the Large Language model (CrewAI based) along with the questions. 

**4. Large Language Model:** The agent previously configured receives x # results per query (user defined), and questions to generate answers. It uses x # of max tools (user selected) as extra functions in the generation process. 

**5. Generation Output:** The answer to the query is outputted in proper natural language, backed up by sources. Output also includes the sources from the database used and their similarity score in respect to the question. 

### Installation
- To run the app locally, follow the steps below:
- Open terminal inside main portfolio (MEJIA-Language-Processing)
- Run ‘pip install pipreqs’ command
- Navigate to the FINAL-Project folder:
    - ‘cd MEJIA-Language-Processing/MEJIA_LPP_Rag/FINAL-Project’
- Run ‘ls’ command to check you are in the right folder (should be FINAL-Project)
- Run ‘pipreqs’ command to create text file in folder
- Run ‘streamlit run app.py’ to open streamlit browser
- Use your open API key to interact with the TRAVEL RAG

### Link to deployed version
https://silvanamejia1-language-porcessing-in-practice--app-guo92y.streamlit.app/




