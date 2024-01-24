# LangChain Demo
## An automated test generator using genAI and langChain


This is a completely automated service that creates open ended questions for students and grades the student's answer. The inputs required are the topic of interest and the core standard that we want to use to evaluate the student’s response on (following the [core standard initiative](https://www.thecorestandards.org/)).

## Test creation
The prototype looks for the relevant page in Wikipedia that describes the topic given as an input. Then it splits the page in sections. One section gets randomly chosen to be used as the context to create the question.
We then build the prompt to feed to the AI to create the question. It contains the context to use, the core standard, and a common prompt. Once this prompt is fed to the AI we retrieve the question produced, which contains also an introduction, the context and the question.

## Grading
Once the student answers the question we create another prompt to feed to the AI to grade the student’s response. It contains the context used, the rubric for grading, the question generated previously by the AI, the student’s answer and a common prompt. We use chain of thought prompting to make sure the AI gives a detailed feedback explaining the logic for the grading. We also ask the AI to provide a follow-up question.

## Quality control
For testing we rely on one feature of the Wikipedia API in LangChain which returns for every Wikipedia page its summary. We run the same workflow as described before, but we change the core standard used to one that tests the student’s ability to summarize a given text. We use as context the whole wikipedia page on the given subject.
The first test is to check that the question produced by the AI asks the student to summarize the context (we do this by looking in the AI response of keywords like summary, summarize, etc). 
As a second test we use the wikipedia summary mentioned above as a simulated student’s answer, and we ask the AI to grade it. In this case we test that the AI grades the summary at a “meet” or “exceeds” level, as the summary provided by wikipedia is deemed to be of good quality.
We use GPT4 as it has shown after some testing to be the most reliable model for the task.

## Usage
You need an openAI API key to use the notebook. Other than that, just select your topic of interest in the *subject* variable and enjoy!
