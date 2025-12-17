Objective: Create a customer support workflow triggered by a new email received in Gmail, which classifies the email, retrieves relevant information using AI, and sends an automated response.
Background/Context: The task involves setting up an automated customer support workflow using a platform that integrates Gmail, AI text classification, a vector database (Pinecone), and an AI agent to process and respond to customer emails. The workflow is triggered by a new email, classifies it as customer support-related or not, retrieves relevant policy information, and sends a tailored response.
Steps:
1.	Set Up Gmail Trigger: 
o	Add a Gmail node as the first step with the trigger "On Message Received."
o	Authorize access using OAuth 2.0 via Google Cloud Console by enabling the Gmail API.
o	Sign in with the desired Google account, grant permissions, and name the credential.
o	Fetch a test email to verify the trigger pulls email content (e.g., "What is the privacy policy? I'm concerned about my data and passwords.").
o	Turn off the "Simplify" option to retrieve full email content and pin the test data for consistent testing.
2.	Classify Email Content: 
o	Add a Text Classifier node after the Gmail trigger to determine if the email is customer support-related.
o	Connect an AI chat model (e.g., Open Router with GPT-4o Mini or Google Gemini 2.0 Flash).
o	Configure the Text Classifier: 
	Drag the email content (text field from the Gmail node) into the "Text to Classify" field.
	Define two categories: 
	Customer Support: Emails related to helping customers, asking about policies, products, or services.
	Other: Any non-customer support email.
o	Test the classifier to ensure it correctly identifies the email as customer support-related.
3.	Set Up AI Agent for Response: 
o	Add an AI Agent node to the Customer Support branch.
o	Configure the AI Agent: 
	Set the input to the email content from the Gmail trigger.
	Define a system prompt: "You are a customer support agent for TechHaven. Respond to emails with relevant information using your knowledgebase tool. Output should be friendly, use emojis, and sign off as Mr. Helpful from TechHaven Solutions. Output only the body content of the email."
	Connect a chat model (e.g., OpenAI or Google Gemini 2.0 Flash).
	Add a Pinecone Vector Store tool: 
	Name it "knowledgebase."
	Set the operation to "Retrieve Documents as a Tool for an AI Agent."
	Configure the index (e.g., "sample") and namespace (e.g., "FAQ").
	Use an embeddings model (e.g., OpenAI text-embedding-3-small).
o	Test the AI Agent to ensure it retrieves relevant information (e.g., privacy policy details) and generates a friendly response.
4.	Send Automated Reply: 
o	Add a Gmail node to reply to the email.
o	Configure the node: 
	Select "Reply to a Message" operation.
	Set the message type to "Text."
	Drag the message ID from the Gmail trigger node to ensure the reply is in the same thread.
	Drag the AI Agent’s output (response body) into the message field.
	Enable the option to append an attribution (e.g., avoid "sent by n8n").
o	Test the step to verify the email is sent successfully and appears in the same thread.
5.	Optional Enhancements: 
o	Add a Gmail node to label the email (e.g., "Customer Support"): 
	Use the same message ID from the Gmail trigger.
	Select or create a label and test the step.
o	Expand the workflow to handle other email types (e.g., finance) by adding more branches and knowledge bases.
Output Format: Step-by-step guide in bullet points, followed by a summary of the workflow’s functionality.
Style and Tone: Technical, clear, and instructional, suitable for a tutorial audience.
Key Elements/Constraints:
•	Ensure proper authorization for Gmail API and correct credential setup.
•	Handle errors (e.g., chat model key issues) by switching models or resetting keys.
•	Use the exact message ID to maintain email thread continuity.
•	Ensure the AI Agent’s system prompt aligns with the desired output (friendly tone, emojis, specific sign-off).
•	Verify the Pinecone Vector Store is correctly configured with the right index and namespace.
Example:
•	Test Email: "What is the privacy policy? I'm concerned about my data and passwords."
•	AI Agent Output: "Hey there! 😊 Thank you for your concern about our privacy policy. At TechHaven, we take your data protection seriously. [Summary of data collection, protection, cookies]. Best, Mr. Helpful from TechHaven Solutions."
•	Result: The email is classified as customer support, the AI retrieves privacy policy details from Pinecone, and a reply is sent in the same thread with the customer support label applied.
Verification:
•	The Gmail API is enabled via Google Cloud Console (verified as a standard process).
•	The Text Classifier accurately categorizes emails based on provided descriptions.
•	The AI Agent’s response aligns with the system prompt and uses the Pinecone knowledgebase.
•	The reply is sent in the correct thread, and optional labeling works as intended.
Summary: This workflow automates customer support by triggering on new Gmail emails, classifying them as customer support-related or not, using an AI agent to retrieve relevant information from a Pinecone vector database, and sending a friendly, emoji-filled response signed by "Mr. Helpful from TechHaven Solutions." Optional enhancements include labeling emails and expanding for other email types, improving inbox management efficiency.

