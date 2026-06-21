Generate a tailored resume for a specific job description.

Steps:
1. Read `1-Profile/YOUR_context.md` and `1-Profile/YOUR_resume_data_compact.md`
2. Read `2-Resume/prompts/prompt_compact.md` for generation instructions
3. If $ARGUMENTS contains a job description, use it. Otherwise ask the user to paste it.
4. Follow the prompt instructions exactly — rebuild the resume from scratch for this role, not a generic tweak
5. Output the complete `.tex` file
6. Ask if the user wants it saved to `2-Resume/output/`
