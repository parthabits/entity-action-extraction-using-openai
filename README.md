
# OpenAI Metadata Extraction

This project demonstrates how to use OpenAI's API to extract actions and metadata entities such as place, email ID, and things from a given text. The application uses the `gpt-35-turbo` model to process the input text and generate structured metadata.

## Prerequisites

Ensure you have Python installed and set up in your environment.

### Required Installations

Install the necessary library using pip:

```bash
pip install openai==0.28
```

## OpenAI API Setup

Before running the script, set up your OpenAI credentials:

- Replace `openai.api_key` with your OpenAI API key.
- Update `openai.api_base`, `openai.api_type`, and `openai.api_version` as per your OpenAI Azure configuration.

```python
import openai

openai.api_key = "your-api-key"
openai.api_base = "your-api-endpoint"
openai.api_type = "azure"
openai.api_version = "2023-03-15-preview"
model_name = "gpt-35-turbo"
```

## Model Settings

The following settings are used for the LLM:

- **Temperature**: `0` (for deterministic responses)
- **Max Tokens**: `500` (maximum tokens in the response)

```python
temperature = 0
max_tokens = 500
```

## Method Description

The `get_entity_action` function processes an input text and an action list. It:

1. Splits the input text into sentences.
2. Matches actions from the provided action list for each sentence.
3. Extracts metadata entities like place, email ID, and things from each sentence.
4. Returns the result in a structured format.

### Function Signature

```python
def get_entity_action(input_text, input_action_list):
    ...
```

### Sample Execution

```python
input_text = (
    "Alice booked a hotel in Paris and shared the details via alice@example.com. "
    "She also mentioned bringing a camera for the trip."
)
input_action_list = ["book", "share", "mention", "bring"]

print(get_entity_action(input_text, input_action_list))
```

### Expected Output

```json
[
    {
        "sentence": "Alice booked a hotel in Paris and shared the details via alice@example.com.",
        "action": "book",
        "entity": {
            "place": "Paris",
            "email_id": "alice@example.com",
            "things": "hotel"
        }
    },
    {
        "sentence": "She also mentioned bringing a camera for the trip.",
        "action": "mention",
        "entity": {
            "place": null,
            "email_id": null,
            "things": "camera"
        }
    }
]
```

## Notes

- Ensure valid input text is provided; otherwise, the function will return: `'Valid text need to be passed'`.
- Customize `action_list` and `entity_list` in the prompt to suit your use case.

## License

This project is licensed under the MIT License.
