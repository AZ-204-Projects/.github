# Context & Best Practices for README Generation: AZ-204 Learning Labs

This document encapsulates the core requirements and preferred practices for generating README.md files for small, repeatable labs such as those typical in AZ-204 (Azure Developer) learning scenarios. It is designed to guide an AI or contributor to produce README files that are consistent, actionable, and comfortable for enterprise and classroom settings, particularly when using PowerShell scripting for automation.

---

## 1. Git-Oriented Structure

- **Implied or Explicit Git Structure:**  
  README must assume or describe a standard git repository layout, where scripts, application code, and documentation are organized in separate, discoverable folders.  
    - Example:
      - `/scripts` for provisioning and automation scripts.
      - `/src` for application code.
      - `/docs` for additional documentation.

---

## 2. Scripts & Automation: PowerShell First

- **All Commands Provided as PowerShell Scripts:**  
  - Avoid one-off manual commands in the README; instead, provide and reference `.ps1` scripts for each major task (resource provisioning, app setup, deployment, cleanup, etc.).
  - Reference scripts directly in the workflow sections ("run `./scripts/setup.ps1`", etc).

- **Centralized Environment Variables:**  
  - All variables (resource names, locations, configuration values) should be set in a single `source.ps1` file.
  - Each script must dot-source this file (e.g., `. .\source.ps1`) for variable access, ensuring consistency and easy modification.

---

## 3. Script Authoring Conventions

- **Use `.ps1` Scripts Exclusively:**  
  - All automation instructions should be PowerShell scripts (`.ps1`), not Bash or CMD.  
  - Scripts should be cross-platform where possible, but Windows-first is acceptable for labs.

- **Folder Change Safety:**  
  - If a script requires changing directories (e.g., to scaffold a .NET project), it must:
    - Save the original directory at the beginning:  
      ```powershell
      $originalDir = Get-Location
      ```
    - Use `try/catch/finally` to ensure the script always returns to the original directory:
      ```powershell
      try {
          Set-Location "<target-folder>"
          # ... perform actions ...
      } catch {
          Write-Error "Script failed: $_"
      } finally {
          Set-Location $originalDir
      }
      ```
    - This ensures users can run scripts from any directory without manual navigation or cleanup.

---

## 4. README Content & Structure

- **Section Requirements:**  
  - The README must be structured for clarity and guidance, with a Table of Contents and the following sections (where appropriate):
    - Product Description or Lab Overview
    - Testing Method / Verification Steps
    - Project Overview
    - Technology Stack
    - Pre-requisites
    - Azure CLI Setup
    - Resource Provisioning (reference scripts, not inline commands)
    - Application Setup (reference scripts, not inline commands)
    - Exercise/Workflow (how to test, verify, use)
    - Enterprise Practices
    - Local Development (IDE recommendations, extensions)
    - Cleanup
    - References

- **Script Usage Instructions:**  
  - Where user action is needed, direct the user to run provided scripts, not to copy/paste blocks of CLI commands.
  - If manual steps are unavoidable, explain why.

- **Configuration & Variables:**  
  - Always highlight where variables are set and how to modify them (`source.ps1`).
  - Use environment variables for secrets; never hard-code credentials.

---

## 5. Enterprise & Comfort Practices

- **Automation Focus:**  
  - All steps should be automatable/repeatable via scripts (no hidden manual steps).
- **Separation of Concerns:**  
  - Provisioning, application code, and testing should be clearly separated both in structure and in the README.
- **Consistency:**  
  - Use consistent naming, resource naming conventions, and script patterns throughout.
- **Error Handling:**  
  - Scripts must include basic error handling with clear messages.
- **Security:**  
  - Recommend or require Service Principal (Azure AD) for automation where possible.
  - Reference official docs for authentication and permissions.

---

## 6. Additional Guidance

- **References:**  
  - Always provide links to relevant Microsoft/Azure documentation for further reading.
- **Extensibility:**  
  - For labs intended as templates or starting points, include a "Next Steps" section with suggestions for extension or real-world adaptation.
- **Cleanup:**  
  - Provide a script or clearly documented command to remove all provisioned resources.

---

## 7. AI/Author Prompt

When generating a README.md for a new lab, **always follow these practices**:

- Assume PowerShell-first scripting, with all commands provided as `.ps1` files that dot-source a shared variables file.
- Ensure all scripts (especially those that change directories) use `$originalDir = Get-Location` and a `try/catch/finally` block to protect the user's shell context.
- Organize the README in a way that maps directly to the repo folder structure and scripts.
- Do not include manual, stepwise CLI command blocks except for rapid test or verification steps that cannot be scripted.
- Highlight any enterprise-grade or "real-world" best practices, even in minimal labs.

---

**This context is intended for use by humans or AI systems creating README documentation for Azure-focused learning labs, ensuring a high standard of clarity, safety, and maintainability.**
