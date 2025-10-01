# Contributing to Insurance Claims Pipeline

Thank you for your interest in contributing to the Insurance Claims Pipeline project! 🎉

## 🤝 How to Contribute

### 1. Fork the Repository
- Click the "Fork" button on the top right of this repository
- Clone your fork locally:
  ```bash
  git clone https://github.com/yourusername/insurance-claims-pipeline.git
  cd insurance-claims-pipeline
  ```

### 2. Set Up Development Environment
```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
pip install -r requirements-dev.txt

# Set up pre-commit hooks
pre-commit install
```

### 3. Create a Feature Branch
```bash
git checkout -b feature/your-feature-name
# or
git checkout -b fix/issue-number
```

### 4. Make Your Changes
- Write clean, well-documented code
- Follow the existing code style
- Add tests for new functionality
- Update documentation as needed

### 5. Test Your Changes
```bash
# Run Python tests
pytest tests/

# Run dbt tests
cd data-generator/ins_dbt
dbt test

# Run linting
flake8 data-generator/
black data-generator/
```

### 6. Commit Your Changes
```bash
git add .
git commit -m "feat: add new fraud detection algorithm"
```

### 7. Push and Create Pull Request
```bash
git push origin feature/your-feature-name
```

Then create a Pull Request on GitHub.

## 📝 Commit Message Convention

We follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

- `feat:` - New features
- `fix:` - Bug fixes
- `docs:` - Documentation changes
- `style:` - Code style changes (formatting, etc.)
- `refactor:` - Code refactoring
- `test:` - Adding or updating tests
- `chore:` - Maintenance tasks

Examples:
- `feat: add machine learning fraud detection`
- `fix: resolve data type conversion error`
- `docs: update Power BI setup instructions`

## 🧪 Testing Guidelines

### Python Code
- Write unit tests for all new functions
- Aim for >90% code coverage
- Use descriptive test names

### dbt Models
- Add generic tests for data quality
- Test for null values, uniqueness, referential integrity
- Add singular tests for business logic

### Power BI
- Test dashboard functionality
- Verify data refresh works correctly
- Check mobile responsiveness

## 📋 Pull Request Checklist

Before submitting your PR, ensure:

- [ ] Code follows the project's style guidelines
- [ ] All tests pass
- [ ] Documentation is updated
- [ ] Commit messages follow conventional format
- [ ] PR description clearly explains the changes
- [ ] Screenshots included for UI changes
- [ ] Breaking changes are documented

## 🐛 Reporting Issues

When reporting bugs, please include:

1. **Clear description** of the issue
2. **Steps to reproduce** the problem
3. **Expected vs actual behavior**
4. **Environment details** (OS, Python version, etc.)
5. **Screenshots** if applicable
6. **Error logs** if available

## 💡 Feature Requests

For new features, please:

1. Check if the feature already exists
2. Describe the use case and benefits
3. Provide mockups or examples if possible
4. Consider implementation complexity

## 🏷️ Labels

We use these labels to categorize issues and PRs:

- `bug` - Something isn't working
- `enhancement` - New feature or request
- `documentation` - Improvements to documentation
- `good first issue` - Good for newcomers
- `help wanted` - Extra attention is needed
- `question` - Further information is requested

## 📞 Getting Help

- 💬 **Discord**: [Join our community](https://discord.gg/insurance-pipeline)
- 📧 **Email**: support@insurance-pipeline.com
- 🐛 **Issues**: [GitHub Issues](https://github.com/yourusername/insurance-claims-pipeline/issues)

## 🎉 Recognition

Contributors will be:
- Listed in the README.md
- Mentioned in release notes
- Invited to the core contributors team (for significant contributions)

Thank you for contributing! 🚀
