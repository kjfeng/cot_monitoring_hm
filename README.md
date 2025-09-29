# Chain-of-Thought Monitoring for Harmful Manipulation

This repository contains experimental code for investigating the extent to which CoT monitoring can serve as a technique for making more informed decisions about whether AI-generated text contains harmful manipulation. You can read a brief research summary [here](https://drive.google.com/file/d/1i4N8LpYSUc3hEgH4GawpWKv1TLro9pTW/view?usp=sharing) and see an accompanying policy demo [in this repo](https://github.com/kjfeng/cot_hm_policy_demo).


## Setup

1. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

2. **Set up environment variables:**
   Create a `.env` file with your API keys:
   ```
   TOGETHER_API_KEY=your_together_api_key
   OPENAI_API_KEY=your_openai_api_key
   ```

3. **Using the dataset:**
   The `main.ipynb` notebook automatically loads the [Anthropic persuasion dataset from HuggingFace](https://huggingface.co/datasets/Anthropic/persuasion).

## Usage

### Reasoning Chain Generation (`main.ipynb`)

Generates potentially persuasive messages using different system prompt conditions:

```python
# Generate data with different system prompt conditions
get_results("openai/gpt-4o", df_filtered, True, 'full')  # Full system prompt (Claude 4)
get_results("openai/gpt-4o", df_filtered, True, 'min')   # Minimal system prompt (Claude 4)
```

### Grading (`grader.ipynb`)

Evaluates generated content for harmful manipulation and faithfulness (modify filenames as needed and the model at your discretion):

```python
# Grade for harmful manipulation
grade_reasoning("gpt-5-mini", "file.csv")

# Grade for faithfulness between reasoning and output
grade_faithfulness("gpt-5-mini", "graded_file.csv")
```

## Experimental Design
This experimental design largely mirrors Anthropic's [2024 persuasiveness study](https://www.anthropic.com/research/measuring-model-persuasiveness) but with some modifications to focus on CoT monitoring.

