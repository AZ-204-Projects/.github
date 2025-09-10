# 🗂️ Project Guidelines & Prompts Naming Plan

This document defines how to name and organize guideline and prompt files for both enterprise-ready and learning/lab projects.

---

## 📑 Prefixes & Categories

| Prefix              | Description                                         | Example Subject(s)                |
|---------------------|-----------------------------------------------------|-----------------------------------|
| `guide-`            | Enterprise/project standards                        | dotnet, python, powershell        |
| `prompt-`           | Enterprise/project code-generation prompts           | dotnet, python, powershell        |
| `lab-guide-`        | Learning/lab standards and style guides             | dotnet, python, react             |
| `lab-prompt-`       | Learning/lab code-generation prompts                | dotnet, python, react             |
| `learning-guide-`   | General learning/demo standards                     | dotnet, flask, terraform          |
| `learning-prompt-`  | General learning/demo code-generation prompts       | dotnet, flask, terraform          |

---

## 🏢 Enterprise vs. 🧪 Learning/Lab

### **Enterprise Guides & Prompts**
- Strict best practices (e.g., robust error handling, retry logic, scalability, logging, security).
- Intended for production-quality projects.

**Example:**
- `guide-dotnet-enterprise.md`
- `prompt-dotnet-enterprise.md`

### **Learning/Lab Guides & Prompts**
- Focus on clarity, simplicity, and core concepts.
- Some enterprise features (e.g., retry logic, advanced error handling) may be omitted to avoid distraction.
- Still recommend centralized configuration (e.g., a config.ps1 for .NET projects).

**Example:**
- `lab-guide-dotnet.md`
- `lab-prompt-dotnet.md`
- or
- `learning-guide-dotnet.md`
- `learning-prompt-dotnet.md`

Use whichever prefix (`lab-` or `learning-`) best fits your organization’s terminology.

---

## 📝 Usage Guidelines

- Store each guideline or prompt as a standalone markdown file in the `.github` repository or a dedicated `guides/` directory.
- Use clear, consistent naming: `prefix-guide-subject.md` or `prefix-prompt-subject.md`
- Link key guides or prompts from the main README or category indexes.
- Document differences between enterprise and learning standards in the guides themselves.

---

## 🔗 Example File Listing

- `guide-dotnet-enterprise.md`
- `prompt-dotnet-enterprise.md`
- `lab-guide-dotnet.md`
- `lab-prompt-dotnet.md`
- `guide-powershell-enterprise.md`
- `lab-guide-powershell.md`

---

_Last updated: 2025-09-10_
