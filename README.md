# Python_error_fixer

**The project is currently under development. The README will be updated as progress is made.**
The project aims to create a system based on Retrieval-Augmented Generation (RAG) to assist users with their Python programming errors/issues (similar to answers on StackOverflow). The target audience includes beginner programmers, schoolchildren, and students learning to program.

## Contents
- [Data Preprocessing](#data-preprocessing)
- [RAG-baseline](#rag_base)
- [Evaluation](#evaluation)
- [FAQ](#faq)
- [Project Team](#project-team)
- [Links](#links)

## Data Preprocessing
The [dataset](https://huggingface.co/datasets/TacoPrime/errored_python) was taken and processed. During processing, the data was divided into 4 categories: `prompt`, `input` (erroneous Python code), `explanation` (description of the error), and `correct_code`. Duplicates were removed, resulting in a final dataset of 7,095 data points. The data was saved in formats that are convenient for working with the RAG system (`csv` and `json`).

## RAG-baseline
- Embeddings: all-MiniLM-L6-v2
- Indexer: FAISS
- Generator: api gemini -> text2text-generation
- Error-validator

## API-Deployment
- fastAPI + gradio

## Evaluation
We came up with somewhat custom metrics of correctness: due to the fact that our intention is to help novices in coding, we decided to test models correctnes in a way that it shouldnt return broken code. Since its tricky to validate the code logic if its any different from basic algorithms or print("hello world"), out best bet is to check if model returned somewhat working without ValueError or IndexError, etc. 
- If model's output returned working code (not necessarily _desired_ output), then we mark data point as "1", else - "0".
- Based on 100 examples picked for testing, we came with impressive result: 92% of corrected outputs are valid to run. (Explanation for such result will be a bit later).
- Example below>
![simple](./rag_base/simple_exmpl.jpg)

## How to build
1. Clone the repo with `git clone https://github.com/Egelvein/Python_error_fixer.git`
2. Go to the folder `cd Python_error_fixer`
3. Install the requirements `pip install -r requirements.txt`
4. Get the free gemini api-key [here](https://ai.google.dev/gemini-api/docs/api-key?hl=en)
5. Write this code in file `api_key_file.py`

## How to use
1. Run the command `uvicorn main:app`
2. Open url `http://127.0.0.1:8000`
3. Open url `http://127.0.0.1:7860`
4. Enjoy it!

## FAQ
This section will include information on common errors when using the tool or attempting to reproduce experiments.

## Project Team
- [Mikhail Ivanov](https://www.linkedin.com/in/mikhail-ivanov-2a2767210/) - ML Engineer
- [Viacheslav Siniaev](https://www.linkedin.com/in/vyacheslavsinyaev/) - ML Engineer

## Links
- [Raw Dataset](https://huggingface.co/datasets/TacoPrime/errored_python)
- [Preprocessed Datasets](https://drive.google.com/drive/folders/1vEvFF5a6vSkaRhjf0WylZPu9a6R5hIS0?usp=sharing)
