# STEMViz Agent Guidelines

## Build/Test Commands

```bash
# Install dependencies
uv add <package_name>  # Add new packages
uv pip install -r requirements.txt  # Install all dependencies

# Run the main application
uv run app.py

# Test individual pipeline phases (if available)
uv run test_phase1.py   # Concept interpretation
uv run test_phase2.py   # Animation generation  
uv run test_phase3.py   # Script + audio synthesis
uv run test_phase4.py   # Full pipeline

# Test specific concepts (if available)
uv run test_bubble_sort.py
uv run test_gradient_descent.py
uv run test_bayes.py
```

## Code Style Guidelines

### Imports & Structure
- Use absolute imports from project root (e.g., `from config import settings`)
- Group imports: standard library, third-party, local modules
- Use `pathlib.Path` for file operations
- Type hints required for all function signatures

### Formatting & Types
- Use Pydantic models for data validation and configuration
- Follow PEP 8 spacing and naming conventions
- Use `logging` instead of `print()` for debugging
- Class names: PascalCase, functions/variables: snake_case

### Error Handling
- Use custom exceptions (e.g., `ValidationError`) in utils/validators.py
- Implement retry logic with exponential backoff for API calls
- Log errors with context using structured logging
- Validate all external inputs before processing

### Architecture Patterns
- Inherit from `BaseAgent` for all AI agent classes
- Use dependency injection via config/settings
- Separate concerns: agents/, generation/, rendering/, utils/
- Clean up temporary files after successful operations

### API Integration
- Use OpenRouter for LLM calls with proper error handling
- Implement token usage tracking in agents
- Use structured JSON responses with Pydantic validation
- Handle timeouts and rate limiting gracefully