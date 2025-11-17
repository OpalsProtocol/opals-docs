---
name: rewrite
description: Rewrite documentation pages in Jack Pinfire's voice - authoritative, accessible, and conviction-building
examples:
  - rewrite components/patron-power.md
  - rewrite for-founders/tokenomics.md
  - rewrite overview/litepaper.md
---

You are being asked to rewrite documentation pages using the Jack Pinfire agent.

## Your Task

1. **Identify the file(s) to rewrite**
   - The user will specify which file(s) need rewriting
   - If not specified, ask which file they want to rewrite
   - Common targets: components/*, for-founders/*, for-investors/*, mechanisms/*, technical/*

2. **Launch the Jack Pinfire agent**
   - Use the Task tool with subagent_type "jack-pinfire"
   - Pass the current content of the file to be rewritten
   - Provide clear instructions on what aspects to improve

3. **Agent Instructions Template**

   Use this template when launching the agent:

   ```
   You are rewriting [FILE_PATH] in Jack Pinfire's voice.

   **Original Content:**
   [Paste original content here]

   **Your Task:**
   - Rewrite this documentation maintaining all technical accuracy
   - Use Jack Pinfire's authoritative yet accessible voice
   - Make complex concepts clear without oversimplifying
   - Connect features to real benefits and problems they solve
   - Reference real examples where relevant (Infinex, True Markets, etc.)
   - Use the problem ’ solution ’ vision arc where appropriate
   - Remove jargon or explain it clearly
   - Keep the cypherpunk ethos and focus on sustainability

   **Target Audience:** [founders/investors/developers/general]

   **Output:** The complete rewritten content, ready to replace the original file.
   ```

4. **After the agent completes**
   - Review the rewritten content for technical accuracy
   - Save the rewritten content to the original file using the Write tool
   - Confirm with the user that the rewrite is complete

## Example Usage

**User command:**
```
/rewrite components/patron-power.md
```

**Your response:**
1. Read the current content of components/patron-power.md
2. Launch Jack Pinfire agent with the content and rewrite instructions
3. Save the rewritten content back to components/patron-power.md
4. Confirm completion: "Rewrote [components/patron-power.md](components/patron-power.md) in Jack Pinfire's voice"

## Quality Standards

Ensure the rewritten content:
-  Maintains all technical accuracy
-  Uses Jack's authoritative yet accessible voice
-  Explains jargon or removes it
-  Includes real examples where relevant
-  Connects features to benefits
-  No emojis (unless user requests)
-  No price predictions or hype
-  Consistent with Opals v2 messaging
-  Builds conviction in fair launches and sustainability

---

Begin by reading the file to rewrite and launching the Jack Pinfire agent.
