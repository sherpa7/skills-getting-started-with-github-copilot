# GenAI Training Exercises

This repository serves as a hands-on training environment for learning how to work with GitHub Copilot and AI-assisted development.

## Training Objectives

By completing these exercises, you will learn to:

1. **Use GitHub Copilot for Code Generation**
   - Generate code from comments
   - Use inline suggestions
   - Leverage Copilot's context awareness

2. **Leverage Copilot Chat for Code Understanding**
   - Ask questions about codebases
   - Get explanations for complex code
   - Understand project structure

3. **Apply Test-Driven Development with AI**
   - Write tests with Copilot assistance
   - Generate test cases
   - Debug failing tests

4. **Refactor Code with AI Assistance**
   - Improve code quality
   - Add error handling
   - Implement new features

## Exercises

### Exercise 1: Understanding the Codebase
**Objective:** Use GitHub Copilot to explore and understand the existing application.

**Tasks:**
1. Open the `src/app.py` file
2. Use Copilot Chat with `@workspace` to ask: "What does this application do?"
3. Ask Copilot to explain the purpose of each endpoint
4. Request a summary of the data model

### Exercise 2: Writing Tests
**Objective:** Use Copilot to write comprehensive test cases.

**Tasks:**
1. Open `tests/test_app.py`
2. Review the existing test structure
3. Use Copilot to generate additional test cases:
   - Test for maximum participant limits
   - Test for invalid email formats
   - Test for edge cases in activity names

**Prompt example:**
```
# Add a test to verify that signup fails when activity is at max capacity
```

### Exercise 3: Fixing the Duplicate Signup Bug
**Objective:** Use Copilot to identify and fix a critical bug.

**Background:** Students can currently sign up for the same activity multiple times.

**Tasks:**
1. Ask Copilot Chat: "Where could a bug allowing duplicate signups exist?"
2. Navigate to the identified location in `src/app.py`
3. Add a comment: `# Validate student is not already signed up`
4. Accept Copilot's suggestion to implement the validation
5. Run tests to verify the fix

### Exercise 4: Adding New Activities
**Objective:** Use Copilot to generate realistic test data.

**Tasks:**
1. Locate the `activities` dictionary in `src/app.py`
2. Use inline chat (Ctrl/Cmd + I) with this prompt:
   ```
   Add 2 more sports activities, 2 artistic activities, and 2 intellectual activities
   ```
3. Review and accept the generated activities
4. Test the application to ensure new activities appear

### Exercise 5: Implementing New Features
**Objective:** Add a feature to check if an activity is full before signup.

**Tasks:**
1. Use Copilot Chat to ask: "How should I prevent signups when an activity is at max capacity?"
2. Implement the suggested validation in the `signup_for_activity` function
3. Write a test case for this scenario
4. Run tests to verify the implementation

### Exercise 6: Code Documentation
**Objective:** Generate comprehensive documentation with Copilot.

**Tasks:**
1. Select the `signup_for_activity` function
2. Use inline chat to request: "Add detailed docstring with parameter descriptions and return values"
3. Generate a markdown file documenting all API endpoints
4. Create example curl commands for each endpoint

## Running the Application

### Prerequisites
- Python 3.8 or higher
- pip package manager

### Installation
```bash
pip install -r requirements.txt
```

### Running the Server
```bash
uvicorn src.app:app --reload
```

Access the application at:
- Web interface: http://localhost:8000
- API documentation: http://localhost:8000/docs
- ReDoc: http://localhost:8000/redoc

### Running Tests
```bash
pytest
```

Run tests with coverage:
```bash
pytest --cov=src tests/
```

Run specific test classes:
```bash
pytest tests/test_app.py::TestSignupEndpoint
```

## Tips for Working with GitHub Copilot

### Context is Key
- Keep relevant files open in tabs
- Use clear, descriptive variable and function names
- Write explicit comments to guide Copilot

### Effective Prompting
- Be specific about what you want
- Provide examples when necessary
- Iterate on prompts if results aren't satisfactory

### Review AI-Generated Code
- Always review suggestions before accepting
- Verify logic and edge cases
- Run tests to validate functionality

### Use Chat Participants
- `@workspace` - For project-wide questions
- `@terminal` - For command-line assistance
- `#file` - To reference specific files

## Advanced Challenges

Once you've completed the basic exercises, try these advanced tasks:

1. **Add Database Persistence**: Replace in-memory storage with SQLite
2. **Implement Authentication**: Add JWT-based authentication for students
3. **Create Admin Endpoints**: Build endpoints for activity management
4. **Add Email Notifications**: Send confirmation emails when students sign up
5. **Implement Waiting Lists**: Queue students when activities are full

## Resources

- [GitHub Copilot Documentation](https://docs.github.com/en/copilot)
- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [Pytest Documentation](https://docs.pytest.org/)
- [VS Code Tips](https://code.visualstudio.com/docs)

## Feedback and Contributions

This is a learning repository. Feel free to experiment, break things, and learn from mistakes!
