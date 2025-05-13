# 🍽️ Roorkee Food Assistant

**Roorkee Food Assistant** is an advanced, retrieval-augmented Streamlit app that answers any question about food, dishes, restaurants, or menus in Roorkee-using only real, up-to-date menu data.

---

## **Features**

- **Natural language Q&A:** Ask about any dish, price, restaurant, cuisine, or food type in Roorkee.
- **Strict domain focus:** Only answers questions about food/restaurants in Roorkee (refuses all other topics).
- **No hallucinations:** Answers are always grounded in the real menu/context data loaded from local CSV/JSON.
- **Price & type filtering:** Supports queries like “cheap pizza places,” “expensive non-veg dishes,” or “moderate paneer options.”
- **Streamlit UI:** Clean, interactive web interface for users and admins.

---

## **How It Works**

1. **Data Preprocessing:**  
   - `New_Feature_And_data_preprocessing.py`  
     Cleans and enriches the raw menu CSV (`Nugget_final_dataset.csv`), adds features like `dish type` (cheap/moderate/expensive) and a combined `tag` column, and outputs `Nugget_New_feature_dataset.csv`.

2. **Data Conversion:**  
   - `data_converter.py`  
     Converts the preprocessed CSV into a list of menu item documents (`Nugget_restaurant_menu.json`) for vector search.

3. **Vector Store Ingestion:**  
   - `ingest.py`  
     Loads the JSON, creates embeddings (HuggingFace), and uploads all menu documents to Pinecone vector DB.

4. **Retrieval + LLM Pipeline:**  
   - `rag_pipeline.py`  
     Sets up the retriever (Pinecone + HuggingFace embeddings) and loads the LLM (MistralAI) with a strict prompt:
     - Only answer food/restaurant/menu questions about Roorkee.
     - Refuse all others.
     - Never use external knowledge.
     - If answer not in context, say “I don’t know based on provided information.”

5. **Streamlit App:**  
   - `app2.py`  
     User interface for asking questions and viewing answers. Shows current date, random food facts, and maintains chat history.

---

## **Installation**

1. **Clone this repo and enter the folder:**
     git clone https://github.com/yourusername/roorkee-food-assistant.git

2. **Install dependencies:**
     pip install -r requirement.txt

3. **Set up your environment variables:**  
Create a `.env` file with your Pinecone and MistralAI API keys:
     PINECONE_API_KEY=your-pinecone-key
     MISTRAL_API_KEY=your-mistral-key
     PINECONE_INDEX_NAME=your-pinecone-index

---

## **Usage**

1. **Preprocess and convert data:**
      python New_Feature_And_data_preprocessing.py
      python data_converter.py      

2. **Ingest menu data into Pinecone:**
      python ingest.py

3. **Launch the Streamlit app:**
      streamlit run app2.py
Open the provided local URL in your browser.

---

## **File Descriptions**

- **New_Feature_And_data_preprocessing.py** - Cleans and enriches the raw menu data.
- **Nugget_final_dataset.csv** - Raw menu data (input).
- **Nugget_New_feature_dataset.csv** - Cleaned/enriched menu data (output).
- **data_converter.py** - Converts CSV to JSON format for vector DB.
- **Nugget_restaurant_menu.json** - JSON menu data for vector DB.
- **ingest.py** - Uploads menu data to Pinecone vector DB.
- **rag_pipeline.py** - Sets up the retrieval-augmented generation pipeline.
- **app2.py** - Streamlit web app for user interaction.
- **requirement.txt** - Python dependencies.

---

## **Example Queries**

- “What are the cheapest non-veg pizzas in Roorkee?”
- “Which restaurants serve spicy paneer dishes?”
- “Show me moderate price desserts from Domino’s Pizza.”
- “List all veg dishes available after 10pm.”
- “What are the contact details for Pizza Hut in Roorkee?”

---

## **Notes**

- **Domain restriction:** The assistant will only answer food/restaurant/menu questions about Roorkee. All other queries are politely refused.
- **No external knowledge:** All answers are based strictly on your menu/context data.
- **API keys:** You must provide your own Pinecone and MistralAI API keys in the `.env` file.

---

## **License**

MIT License

---

## **Contact**

Created by **Affan Faridi**  
For issues or suggestions, open a GitHub Issue or contact via your profile.

---
         
