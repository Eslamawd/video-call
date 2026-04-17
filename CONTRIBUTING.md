# Contributing to Social App

Thank you for your interest in contributing! We welcome all kinds of contributions.

## Ways to Contribute

### 🐛 Report Bugs

Found a bug? Please open an issue on [GitHub Issues](https://github.com/Eslamawd/video-call/issues) with:

- Clear description of the bug
- Steps to reproduce
- Expected vs actual behavior
- Your environment (OS, Docker version, etc.)

### 💡 Suggest Features

Have an idea? Open a GitHub Discussion or Issue with:

- Use case / problem it solves
- Proposed solution
- Alternative approaches (if any)
- Relevant context

### 📝 Improve Documentation

Documentation is crucial! You can:

- Fix typos or unclear explanations
- Add examples
- Create deployment guides for different platforms
- Translate documentation to other languages

### 🔧 Code Contributions

**Before coding:**

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature-name`
3. Make sure you have a linked GitHub issue

**While coding:**

- Follow the existing code style
- Add comments for complex logic
- Test your changes locally with Docker
- Keep commits atomic and well-messaged

**Before submitting:**

1. Run tests: `npm test` (if available)
2. Build locally: `docker compose build`
3. Test with: `docker compose up -d`
4. Create a Pull Request with a clear description

### 🎨 Design & UX Improvements

We'd love to improve the UI/UX! You can:

- Submit design mockups
- Create responsive improvements
- Enhance accessibility (a11y)
- Improve dark mode support

### ⚙️ DevOps & Infrastructure

Help with:

- Kubernetes deployment examples
- CI/CD pipeline improvements
- Docker optimization
- Database scaling strategies

## Development Setup

```bash
# 1. Clone your fork
git clone https://github.com/YOUR_USERNAME/video-call.git
cd video-call

# 2. Create a feature branch
git checkout -b feature/awesome-feature

# 3. Set environment variables
echo 'HOST_IP=192.168.8.42' > .env

# 4. Start development
docker compose up -d --build

# 5. Make your changes
# 6. Test thoroughly

# 7. Commit and push
git add .
git commit -m "feat: add awesome feature"
git push origin feature/awesome-feature
```

## Pull Request Guidelines

- **Title**: Clear and descriptive (e.g., "feat: add screen sharing")
- **Description**: Link to issue, explain changes, mention testing
- **Size**: Prefer smaller PRs (easier to review)
- **Tests**: Add tests if applicable
- **Documentation**: Update README if needed

## Code Style

- **Frontend**: Follow Prettier + ESLint rules
- **Backend**: Follow NestJS conventions
- **Comments**: Explain "why", not "what"
- **Naming**: Clear, descriptive variable/function names

## Commit Message Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Code style changes
- `refactor`: Code refactoring
- `test`: Tests
- `chore`: Build, dependencies, etc.

**Example:**

```
feat(rooms): add room persistence to database

Store room metadata in database for history/analytics.
Fixes #123

BREAKING CHANGE: room ID format changed from UUID to ULID
```

## Reporting Security Issues

⚠️ **Don't open public issues for security vulnerabilities!**

Email: security@example.com (or DM on GitHub)

## Code of Conduct

- Be respectful and inclusive
- No harassment or discriminatory language
- Focus on the code, not the person
- Assume good intent

## Need Help?

- 📖 Check the [README](README.md)
- 💬 Ask in GitHub Discussions
- 📧 Email: contact@example.com

---

**Thank you for contributing! 🎉**
