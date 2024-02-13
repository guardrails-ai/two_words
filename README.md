## Overview

| Developed by | Guardrails AI |
| --- | --- |
| Date of development | Feb 15, 2024 |
| Validator type | Format |
| Blog |  |
| License | Apache 2 |
| Input/Output | Output |

## Description

The validator ensures that a generated LLM output is two words only.

## Installation

```bash
$ guardrails hub install hub://guardrails/two_words
```

## Usage Examples

### Validating string output via Python

```python
# Import Guard and Validator
from guardrails.hub import TwoWords
from guardrails import Guard

# Initialize Validator
val = ValidChoices(on_fail="fix")

# Setup Guard
guard = Guard.from_string(
    validators=[val, ...],
)

guard.parse("two dogs")  # Validator passes
guard.parse("horse")  # Validator fails
```

### Validating JSON output via Python

```python
# Import Guard and Validator
from pydantic import BaseModel
from guardrails.hub import TwoWords
from guardrails import Guard

val = ValidChoices(on_fail="fix")

# Create Pydantic BaseModel
class PetInfo(BaseModel):
    pet_name: str = Field("Name of pet", validators=[val, ...])
    pet_type: str = Field(description="Type of pet")

# Create a Guard to check for valid Pydantic output
guard = Guard.from_pydantic(output_class=PetInfo)

# Run LLM output generating JSON through guard
guard.parse("""
{
    "pet_name": "Caesar Rajpal",
    "pet_type": "dog"
}
""")
```

## API Reference

`__init__`
- `on_fail`: The policy to enact when a validator fails.
