# ChatPDF

ChatPDF is a Python project that allows users to upload a PDF document and chat with its contents using natural language queries. The application utilizes various libraries and APIs for text processing, document splitting, embeddings, and question-answering.

## Prerequisites

Before running the project, make sure you have the following dependencies installed:

- Python 3.7 or higher
- `dotenv` library
- `streamlit` library
- `PyPDF2` library
- `langchain` library
- `openai` library

You can install these dependencies using `pip` with the following command:

```
pip install -r requirements.txt
```

Additionally, you need an OpenAI API key to access the OpenAI models. Make sure to set up your OpenAI API key and create a `.env` file in the project directory with the following content:

```
OPENAI_API_KEY=your_api_key
```

Replace `your_api_key` with your actual OpenAI API key.

## Running the Project

To run the ChatPDF project, follow these steps:

1. Clone the project repository to your local machine.
2. Navigate to the project directory.
3. Install the dependencies mentioned above.
4. Create a `.env` file and set up your OpenAI API key as described in the prerequisites.
5. Run the following command to start the application:

```
streamlit run app.py
```

6. The application will start and display a web interface.
7. Use the "Upload your PDF" button to upload a PDF document.
8. Once the PDF is uploaded, you can enter your questions in the "Ask a question to your PDF" text input field.
9. The application will process your question, search for relevant information in the PDF, and display the answer.

Note: If there are any errors or exceptions during the execution, they will be printed to the console.

## Additional Notes

- The `pdf` file uploaded by the user is read and processed using the `PyPDF2` library to extract the text contents.
- The extracted text is split into smaller chunks using the `langchain.text_splitter.CharacterTextSplitter` class. This step is necessary for efficient processing and searching.
- The text chunks are converted into embeddings using the `langchain.embeddings.openai.OpenAIEmbeddings` class. These embeddings represent the semantic meaning of the text.
- The `langchain.vectorstores.FAISS` class is used to create a knowledge base from the text chunks' embeddings. This knowledge base enables similarity search for user queries.
- User questions are inputted through the "Ask a question to your PDF" text input field. The application performs a similarity search in the knowledge base to find relevant documents.
- The `langchain.llms.OpenAI` class is used to initialize the language model for question-answering.
- The `langchain.chains.question_answering.load_qa_chain` function is used to load the question-answering chain, which combines the language model with the knowledge base.
- The retrieved answer to the user's question is displayed in the web interface.

## Conclusion

ChatPDF provides a convenient way to interact with the contents of a PDF document using natural language queries. It leverages powerful language models, embeddings, and similarity search techniques to deliver accurate and relevant answers. Feel free to explore and enhance the project to suit your specific requirements. If you have any questions or encounter any issues, please don't hesitate to reach out.



## Dockerfile

To containerize the ChatPDF project and run it using Docker, you can use the following Dockerfile:

```Dockerfile
FROM python:3.9-slim-buster

WORKDIR /app

ADD . /app

RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 5000

ENV NAME World

CMD ["streamlit", "run", "app.py"]
```

Save the above content in a file named `Dockerfile` in the project directory.

The Dockerfile starts with the base image `python:3.9-slim-buster`, which provides a minimal Python environment.

The working directory is set to `/app`, and the entire project directory is copied into the Docker image.

The `requirements.txt` file, containing the project dependencies, is installed using `pip` with the `--no-cache-dir` flag to avoid caching the downloaded packages.

The `EXPOSE` instruction exposes port 5000, which is the default port used by Streamlit.

The `ENV` instruction sets the `NAME` environment variable to "World". You can modify or remove this line as per your needs.

Finally, the `CMD` instruction specifies the command to run when the Docker container starts. It executes the `streamlit run app.py` command to start the Streamlit application.

To build and run the Docker image, follow these steps:

1. Make sure Docker is installed on your machine.
2. Open a terminal and navigate to the project directory containing the Dockerfile.
3. Run the following command to build the Docker image:

```bash
docker build -t chatpdf .
```

4. After the image is built, run the following command to start a Docker container:

```bash
docker run -p 5000:5000 chatpdf
```

5. The Streamlit application will be accessible at http://localhost:5000 in your web browser.

Note: Make sure to replace `chatpdf` with the desired image name in the above commands if needed.

Using Docker allows you to easily package and deploy the ChatPDF project, ensuring consistent execution across different environments.
