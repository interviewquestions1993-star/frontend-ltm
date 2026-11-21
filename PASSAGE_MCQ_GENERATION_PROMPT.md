# Grade 8 Hindi passage MCQ generation prompt

Use this prompt once for each passage. Replace `{{PASSAGE_NUMBER}}` with a number from 1 to 50. No uploaded document is required. Save the returned JSON in the MCQ bank with the exact extensionless filename `Passage {{PASSAGE_NUMBER}}-MCQ-v1`.

```text
You are an expert CBSE Grade 8 Hindi teacher, children's content writer, and assessment designer.

Create one completely original, age-appropriate Hindi prose passage for Passage {{PASSAGE_NUMBER}}, and then create exactly 10 multiple-choice comprehension questions based only on that passage. No document will be uploaded. You must write both the passage and the questions yourself.

Passage requirements:
1. Write the passage entirely in natural, grammatically correct Hindi (Devanagari).
2. Make it suitable for a CBSE Grade 8 student and approximately 250-350 words long.
3. Give the passage a clear beginning, development, and conclusion or central idea.
4. Choose an educational, engaging theme appropriate for Grade 8, such as values, environment, science in daily life, health, teamwork, responsibility, culture, creativity, problem-solving, digital awareness, or community life.
5. Make Passage {{PASSAGE_NUMBER}} meaningfully different from other passages. Do not reuse a familiar textbook passage, copyrighted text, famous story, real exam passage, or lightly modified online content.
6. The passage must contain enough explicit and implicit information to support questions about the main idea, facts, vocabulary in context, cause and effect, sequence, inference, title/theme, and the writer's message.
7. Do not depend on outside knowledge to answer any question. If the passage contains factual information, include every fact needed to answer the questions within the passage itself.
8. Do not mention these instructions, artificial intelligence, question generation, or the passage number inside the prose passage.

Question requirements:
1. Use Hindi (Devanagari) for every question, option, answer, and explanation.
2. Generate exactly 10 questions with this exact difficulty distribution:
   - 3 easy
   - 4 medium
   - 3 hard
3. Exactly 2 questions must be Assertion-Reason questions. The other 8 must be standard MCQs.
4. Cover a balanced mix of the main idea, directly stated facts, vocabulary in context, sequence or cause-and-effect, inference, suitable title/theme, and the writer's intended message.
5. Every question must have exactly 4 plausible options and exactly one correct answer.
6. Do not introduce facts, assumptions, names, events, or meanings that are not supported by the generated passage.
7. Do not duplicate or lightly rephrase any question.
8. Give a clear 3-4 sentence Hindi explanation for every correct answer. State which information or idea in the passage supports the answer without referring to an uploaded document or PDF.

Frontend/backend compatibility requirements:
- Repeat the COMPLETE generated passage inside every "question" field using exactly this structure:
  "[PASSAGE]\n<complete generated passage text>\n[/PASSAGE]\nप्रश्न: <question text>"
- The passage text must be identical in all 10 "question" fields.
- Do not create a separate "passage" field.
- Set "subject" to "Hindi Grammar".
- Set "chapter" to "Passage {{PASSAGE_NUMBER}}" exactly.
- Use IDs 1 through 10 with no gaps.
- Use only "easy", "medium", or "hard" in lowercase for "difficulty".
- Use only "standard_mcq" or "assertion_reason" for "question_type".
- The "answer" value must exactly match the complete text of one option.
- Do not prefix standard options with A, B, C, or D.
- Set "page_number" to "1" because the generated passage itself is the single source page.

For the 2 Assertion-Reason questions:
- Store the complete Assertion and Reason after the passage markers in the "question" field using this form:
  "प्रश्न: कथन (A): <कथन>\nकारण (R): <कारण>"
- Use these same four options exactly:
  1. "A और R दोनों सही हैं तथा R, A की सही व्याख्या है।"
  2. "A और R दोनों सही हैं, लेकिन R, A की सही व्याख्या नहीं है।"
  3. "A सही है, लेकिन R गलत है।"
  4. "A गलत है, लेकिन R सही है।"
- Check the truth of A and R and their logical relationship carefully.

Return ONLY a valid JSON array using this schema:
[
  {
    "id": 1,
    "subject": "Hindi Grammar",
    "chapter": "Passage {{PASSAGE_NUMBER}}",
    "difficulty": "easy",
    "question_type": "standard_mcq",
    "question": "[PASSAGE]\n<complete generated passage text>\n[/PASSAGE]\nप्रश्न: <question text>",
    "options": [
      "विकल्प 1",
      "विकल्प 2",
      "विकल्प 3",
      "विकल्प 4"
    ],
    "answer": "विकल्प 1",
    "explanation": "सही उत्तर की 3-4 वाक्यों में स्पष्ट व्याख्या। इसमें बताया जाए कि गद्यांश की कौन-सी जानकारी उत्तर का समर्थन करती है।",
    "page_number": "1"
  }
]

Output rules:
- Return only the JSON array.
- Use double quotes for all JSON keys and string values.
- Escape all newlines inside JSON strings as \n.
- Do not use trailing commas.
- Do not include Markdown, code fences, headings, notes, or comments.
- The response must start with [ and end with ].
- It must parse successfully with Python json.loads().
- Before returning the JSON, silently verify that there are exactly 10 objects, the difficulty count is 3/4/3, exactly 2 objects use "assertion_reason", every object has 4 options, every answer matches one option exactly, and the complete passage is identical in all 10 question fields.
```

## Required MCQ-bank filenames

The backend works without code changes when the files are uploaded to `learnenglishandgrow93-web/cbse-mcq-bank` using these exact extensionless names:

- `Passage 1-MCQ-v1`
- `Passage 2-MCQ-v1`
- ...
- `Passage 50-MCQ-v1`

Do not add `.json` to these filenames unless the backend filename-building logic is changed too.
