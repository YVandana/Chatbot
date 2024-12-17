# Chatbot using GPT 2.0

## Overview
This project implements a chatbot using the Hugging Face Transformers library and LangChain. It allows users to interact with a conversational AI that can generate responses based on user inputs and maintain conversational context.

## Prerequisites
Before running the project, ensure you have the following installed:

- Python 3.10 or higher
- pip

## Installation
To install the required packages, run the following commands:

```bash
!pip install huggingface_hub
!pip install transformers
!pip install langchain
!pip install chainlit
```
All dependencies will be handled automatically.

## Getting Started

1. Clone the repository or download the project files.
2.Open a terminal and navigate to the project directory.
3. Start the Chainlit application by running:
```
!chainlit hello
```
4. Your app will be available at http://localhost:8000.

## Usage
1. Import necessary libraries:
```
import os
import chainlit as cl
from langchain import HuggingFaceHub, PromptTemplate, LLMChain
from getpass import getpass
```
2. Set up your Hugging Face API token:
```
HUGGINGFACEHUB_API_TOKEN = getpass("Enter your Hugging Face API token: ")
os.environ['HUGGINGFACEHUB_API_TOKEN'] = HUGGINGFACEHUB_API_TOKEN
```
3. Choose a model and create a conversational chain:
```
model_id = "gpt2-medium"  # or other models
conv_model = HuggingFaceHub(
    huggingfacehub_api_token=os.environ['HUGGINGFACEHUB_API_TOKEN'],
    repo_id=model_id,
    model_kwargs={"temperature": 0.8, "max_new_tokens": 200}
)
```
4. Define the prompt and run the chatbot:
```
template = """You are a helpful AI assistant that makes stories by completing the query provided by the user: {query}"""
prompt = PromptTemplate(template=template, input_variables=['query'])
conv_chain = LLMChain(llm=conv_model, prompt=prompt, verbose=True)

response = conv_chain.run("Once upon a time in 1947")
print(response)
```
## Features
- Conversational Memory: The chatbot can remember previous interactions, providing a more engaging user experience.
- Customizable Models: Easily switch between different models from Hugging Face.
- User-Friendly Interface: Built with Chainlit for an intuitive chat interface.

## Contributing
Contributions are welcome! Please open an issue or submit a pull request for any improvements or bug fixes.

## License
This project is licensed under the MIT License. See the LICENSE file for more details.

## Acknowledgments
- Hugging Face for providing powerful models.
- LangChain for simplifying the interaction with language models.
- Chainlit for the chat interface.
