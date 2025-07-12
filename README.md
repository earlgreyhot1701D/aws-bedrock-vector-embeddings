# Cal Poly AI Summer Camp: Text Embedding Similarity Analyzer

Welcome to our AI Summer Camp! This project will teach you how to use Large Language Models (LLMs) to generate text embeddings and calculate semantic similarity between different texts. You'll learn how to transform text into numerical vectors and measure how similar different pieces of text are to each other using Python and Amazon Web Services (AWS) Bedrock.

## Contact Information

**Instructor**: Ryan Gertz - rgertz@calpoly.edu

Feel free to reach out if you have questions about:
- Setting up AWS credentials
- Understanding embedding concepts
- Troubleshooting errors
- Ideas for extending this project
- General questions about AI and text similarity analysis

## What You'll Learn

- **Text Embeddings**: Converting text into numerical vectors that capture semantic meaning
- **Cosine Similarity**: Mathematical method to measure how similar two texts are
- **AWS Bedrock Titan**: Amazon's embedding model for generating high-quality text representations
- **Python Programming**: Writing code to process text and perform similarity calculations
- **JSON Data Format**: Working with structured data for embeddings and similarity results

## What This Code Does

This project demonstrates how to use AI to analyze text similarity through embeddings. The code:

1. **Connects to AWS Bedrock**: Uses Amazon Titan embedding model to convert text to vectors
2. **Generates Text Embeddings**: Creates numerical representations of text that capture meaning
3. **Calculates Cosine Similarity**: Measures how similar different texts are to each other
4. **Handles File Input**: Optionally reads additional text from a file for analysis
5. **Saves Results**: Outputs embeddings and similarity scores to JSON files

## Prerequisites

Before you start, you'll need:

### 1. Python Installation
- Python 3.7 or higher installed on your computer
- You can download it from [python.org](https://www.python.org/downloads/)

### 2. AWS Account Setup
- An AWS account
- AWS credentials configured on your computer
- Access to AWS Bedrock service and Amazon Titan embedding model

### 3. Required Python Packages
Install the necessary packages by running this command in your terminal:
```bash
pip install boto3
```

## Understanding the Code

### Key Components

**boto3**: Amazon's Python library that lets us connect to AWS services. Think of it as a bridge between your Python code and Amazon's AI models.

**Text Embeddings**: High-dimensional numerical vectors that represent the meaning of text. Similar texts will have similar embeddings.

**Cosine Similarity**: A mathematical measure that calculates how similar two vectors are, ranging from 0 (completely different) to 1 (identical).

**AWS Bedrock Titan**: Amazon's embedding model that converts text into high-quality vector representations.

### The Functions Explained

#### Function 1: `cosine_similarity(a, b)`
This function calculates how similar two embedding vectors are:
- Takes two lists of numbers (embeddings) as input
- Computes the dot product and norms of both vectors
- Returns a similarity score between 0 and 1
- Handles edge cases where vectors might be empty

#### Function 2: `get_embedding(text)`
This function converts text into embedding vectors:
- Connects to AWS Bedrock Titan embedding model
- Sends text to the model for processing
- Returns a list of numbers representing the text's meaning
- Each embedding is a vector of 1,024 dimensions

#### Function 3: `output_similarities(pipeline_results)`
This function compares all texts with each other:
- Takes a list of text-embedding pairs
- Calculates cosine similarity for every pair combination
- Saves all similarity scores to a JSON file
- Avoids duplicate comparisons (A vs B is same as B vs A)

#### Function 4: `main()`
This is the main function that orchestrates the entire process:
- Defines default texts to analyze
- Optionally reads additional text from a file
- Generates embeddings for all texts
- Saves embeddings and calculates similarities

## How to Run the Code

1. **Save the code**: Copy the code into a file called `text_similarity.py`

2. **Optional: Create a test file**: Create a file called `test_embed.txt` with any text you want to analyze

3. **Open your terminal/command prompt**

4. **Navigate to your project folder**:
   ```bash
   cd path/to/your/project
   ```

5. **Run the code**:
   ```bash
   python text_similarity.py
   ```

6. **Check the output**: Look for these files in your project folder:
   - `embeddings_output.json` - Contains all text embeddings
   - `cosine_similarities.json` - Contains similarity scores between all text pairs

## Customizing The Code

### Add Your Own Text
Create a file called `test_embed.txt` and add any text you want to analyze:
```
This is my custom text that I want to compare with the other examples.
```

### Change the Default Texts
Modify the texts list in the `main()` function:
```python
texts = [
    "Your custom text here",
    "Another piece of text",
    "Machine learning is fascinating",
    "AI will change the world"
]
```

### Use Different AWS Region
Change the region in the `get_embedding()` function:
```python
client = boto3.client('bedrock-runtime', region_name="us-east-1")  # Instead of us-west-2
```

## Understanding the Generated Data

### Embeddings Output (`embeddings_output.json`)
Contains arrays of text-embedding pairs:
```json
[
  {
    "text": "Hello, world!",
    "embedding": [0.123, -0.456, 0.789, ...]
  }
]
```

### Similarities Output (`cosine_similarities.json`)
Contains similarity scores for all text pairs:
```json
[
  {
    "text_a": "Hello, world!",
    "text_b": "Hello Everyone!",
    "similarity": 0.85
  }
]
```

## Interpreting Similarity Scores

- **0.9 - 1.0**: Very similar texts (near duplicates)
- **0.7 - 0.9**: Similar meaning or topic
- **0.5 - 0.7**: Somewhat related
- **0.3 - 0.5**: Loosely related
- **0.0 - 0.3**: Very different topics

## Common Issues and Solutions

### "No credentials found"
This means your AWS credentials aren't set up. You need:
- AWS Access Keys
- AWS CLI configuration
- IAM permissions for Bedrock

### "Access denied to model"
Your AWS account might not have permission to use Titan embeddings:
- Check your AWS Bedrock model access
- Ensure you have the correct model ID
- Verify your IAM permissions

### "Module not found: boto3"
Install the required package:
```bash
pip install boto3
```

### "ValidationException"
This usually means the input text is empty or invalid:
- Check that your text inputs are not empty
- Ensure text is properly formatted
- Try with shorter text if you're hitting length limits

### "test_embed.txt not found"
This is normal - the file is optional:
- Create the file if you want to add custom text
- The code will work fine without it using default texts

## Important Notes

- **Cost Awareness**: Each embedding generation costs money (usually fractions of a cent per request)
- **Rate Limits**: AWS has limits on how many requests you can make per minute
- **Vector Dimensions**: Titan embeddings are 1,024-dimensional vectors
- **Text Length**: There are limits on how long your input text can be

## Use Cases for Text Similarity Analysis

This type of similarity analysis is useful for:
- **Content Recommendation**: Find similar articles or documents
- **Duplicate Detection**: Identify duplicate or near-duplicate content
- **Search Applications**: Improve search by finding semantically similar content
- **Content Clustering**: Group similar content together
- **Plagiarism Detection**: Identify potentially copied content

## Getting Help

If you run into issues:
1. Check the error message carefully
2. Ask our camp staff for assistance
3. Look up the specific error message online
4. Try running the code with shorter texts first
5. Verify your AWS credentials are working

## Example Results

After running the code, you might see similarity scores like:
- "Hello, world!" vs "Hello Everyone!" = 0.85 (very similar greetings)
- "AWS Bedrock Titan embeddings are cool." vs "This is a simple example." = 0.12 (different topics)

## Resources for Further Learning

- [AWS Bedrock Documentation](https://docs.aws.amazon.com/bedrock/)
- [Understanding Text Embeddings](https://platform.openai.com/docs/guides/embeddings)
- [Cosine Similarity Explained](https://en.wikipedia.org/wiki/Cosine_similarity)
- [boto3 Documentation](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html)
- [Vector Similarity Search](https://aws.amazon.com/what-is/vector-databases/)

---

Happy coding! 🚀