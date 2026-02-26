---
agent: agent
model: Claude Sonnet 4.6 (copilot)
description: Specify the skill directory
---
# Skill Validation

Your task is to validate the skill implementation against the provided skill specification.

## Workflow

1. Ensure user provided full skill implementation by providing the whole folder. If missing, ask for it and continue after receiving it.
2. Validate the skill discovery. Based on the `description` field in `SKILL.md` file:
   1. Generate 3 realistic user prompts you are 100% sure the skill will be triggered by.
   2. Generate 3 realistic user prompts that looks similar but will NOT trigger the skill.
   3. Review the description. Is it too vague? Suggest optimized description.
3. Validate the skill implementation. Act as an autonomous agent that triggered the skill.
   1. Ask for a prompt from the user first
   2. For each step in the skill, write out your thought process:
      * What exactly are you doing?
      * Specify a file or a script you read or execute.
      * Flag any execution blocker or ambiguity you encounter and how you resolve it.
      * **MUST NOT EXECUTE ANY CODE**, just specify what you would execute if you were to execute it.
4. Test edge cases and error handling. Act as a ruthless QA tester trying to break the skill. IMPORTANT: just ask in this step, DO NOT FIX things
   1. Ask the user for which the agent should focus on
   2. Ask the user 3-5 challenging questions about edge cases, failure or missing fallbacks in the skill.
5. Refine the skill. Based on my answers to your edge-case questions, rewrite the SKILL.md file, strictly enforcing the Progressive Disclosure design pattern:
   * Keep the main SKILL.md strictly as a high-level set of steps using third person imperative commands.
   * If there are dense rules, large templates or complex schemas in the file, move them into references/ or assets/ and replace the text with a strict command to read the specific file only when needed.
   * Add a dedicated Error Handling section at the bottom incorporating my answers you have found about failures and missing fallbacks.

Go step by step and move to the next step only after finishing the previous one.



