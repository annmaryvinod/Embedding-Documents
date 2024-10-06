
# PDF Text Embedding and Storage using Hugging Face and PostgreSQL

This project extracts text from a PDF document, generates embeddings for the text chunks using Hugging Face models, and stores both the text chunks and their corresponding embeddings in a PostgreSQL database. The stored data can then be retrieved and displayed.

## Table of Contents
1. [Prerequisites](#prerequisites)
2. [Installation](#installation)
3. [Usage](#usage)
    - [Extracting text from PDF](#extracting-text-from-pdf)
    - [Generating text embeddings](#generating-text-embeddings)
    - [Storing embeddings in PostgreSQL](#storing-embeddings-in-postgresql)
    - [Retrieving and displaying stored data](#retrieving-and-displaying-stored-data)
4. [Project Structure](#project-structure)
5. [License](#license)

---

## Prerequisites

Before running the project, ensure you have the following installed:

- Python 3.x
- PostgreSQL
- Hugging Face API Token (for Hugging Face embeddings)
- Required Python libraries:
    - \`psycopg2\`
    - \`PyPDF2\`
    - \`langchain_huggingface\`

---

## Installation

1. Clone the repository or copy the script to your local environment.
2. Install the necessary Python packages by running the following command:
   \`\`\`bash
   pip install psycopg2 PyPDF2 langchain_huggingface
   \`\`\`

3. Set up a PostgreSQL database:
   - Create a database called \`embeddings\`.
   - Inside this database, create a table named \`documents\` using the following SQL query:
     \`\`\`sql
     CREATE TABLE documents (
         id SERIAL PRIMARY KEY,
         text TEXT NOT NULL,
         embedding FLOAT8[] NOT NULL
     );
     \`\`\`
4. Set your Hugging Face API token in the environment variables:
   \`\`\`bash
   export HUGGINGFACEHUB_API_TOKEN="your_huggingface_api_token"
   \`\`\`

---

## Usage

### Extracting Text from PDF
The script starts by extracting text from a PDF file using the \`PyPDF2\` package.

- **Function**: \`extract_text_from_pdf(pdf_path)\`
- **Parameters**: 
  - \`pdf_path\`: The path to the PDF file.
- **Description**: Reads the PDF file and extracts the text from all pages.
- **Returns**: The extracted text as a string.

### Generating Text Embeddings
Once the text is extracted, it is split into smaller chunks, and embeddings are generated for each chunk using the Hugging Face model.

- **Function**: \`split_text_into_chunks(text, chunk_size=1000)\`
- **Parameters**:
  - \`text\`: The extracted text.
  - \`chunk_size\`: The size of each text chunk (default is 1000 characters).
- **Description**: Splits the text into manageable chunks for embedding generation.
- **Returns**: A list of text chunks.

- **Function**: \`generate_embeddings(text_chunks)\`
- **Parameters**:
  - \`text_chunks\`: A list of text chunks for which embeddings will be generated.
- **Description**: Uses the Hugging Face API to generate embeddings for the provided text chunks.
- **Returns**: A list of embeddings corresponding to the text chunks.

### Storing Embeddings in PostgreSQL
The generated embeddings, along with the text chunks, are stored in a PostgreSQL database.

- **Function**: \`store_embeddings_in_postgresql(text_chunks, embeddings)\`
- **Parameters**:
  - \`text_chunks\`: The list of text chunks.
  - \`embeddings\`: The corresponding embeddings for the text chunks.
- **Description**: Stores the text chunks and their embeddings into the PostgreSQL \`documents\` table.
- **Returns**: None. It directly inserts the data into the database.

### Retrieving and Displaying Stored Data
You can retrieve the stored text chunks and embeddings from PostgreSQL and display them.

- **Function**: \`retrieve_and_display_data()\`
- **Parameters**: None.
- **Description**: Fetches the text and embeddings from the database and displays them. It prints the first 100 characters of each text chunk and the first 5 values of the embedding.
- **Returns**: None. It directly prints the data.

### Example Usage:

To run the script:
\`\`\`bash
python script.py
\`\`\`

Make sure to replace \`"doc1.pdf"\` with the actual path to your PDF document. The script will:

1. Extract text from the provided PDF.
2. Split the text into chunks.
3. Generate embeddings using Hugging Face's model.
4. Store the text chunks and embeddings in the PostgreSQL database.
5. Retrieve and display the stored data.

---

## Project Structure

\`\`\`
📁 project-directory
 ├── script.py               # Main script file
 ├── README.md               # Documentation file
 └── requirements.txt        # List of Python dependencies
\`\`\`

---

## License

This project is licensed under the MIT License.
