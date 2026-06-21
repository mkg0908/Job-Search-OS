Generate a complete 8-phase interview prep document for a specific role.

Steps:
1. Read `1-Profile/YOUR_context.md`
2. Read `5-Interview-Prep/stories/YOUR_behavioral_stories.yaml` for the story bank
3. Read `5-Interview-Prep/prompts/interview_prep_prompt.md` for generation instructions
4. If $ARGUMENTS contains a job description, use it. Otherwise ask the user to paste the JD and company name.
5. Follow the prep prompt to generate the full 8-phase doc:
   - Phase 1: Role decode
   - Phase 2: Company research
   - Phase 3: Narrative
   - Phase 4: Behavioral prep
   - Phase 5: Questions to ask
   - Phase 6: Objection handling
   - Phase 7: Logistics
   - Phase 8: Thank-you email
6. Ask if the user wants it saved to `5-Interview-Prep/prep/`
