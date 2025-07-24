# Autogen
This project is a simple (and fun!) multi-agent AI simulation using Microsoft’s AutoGen framework, where:
	•	✍️ A Writer Agent writes an article.
	•	🧐 An Editor Agent reviews and gives feedback.
	•	🙋‍♂️ A User Proxy (that’s you!) oversees the process and ends the chat once the final version is ready.

🚀 What Happens in Chat.py?

Here’s a breakdown of what this script does:

1. 🧪 Model Setup

We load a list of OpenAI models from a JSON file (OAI_CONFIG_LIST). The one we’re using here is:
	•	"gpt-3.5-turbo-1106"

 config_list_from_json(...)

 This lets AutoGen know which models and API keys to use.


 2. 📝 Writer Agent

We create an AssistantAgent called writer whose job is:
	•	To write an article on a given topic.
	•	To revise the article based on feedback.
	•	It stops once it replies with the word TERMINATE.

Config details:
	•	Randomness enabled (temperature=1)
	•	Timeout: 5 minutes
	•	Deterministic seed for reproducibility (seed=50)

⸻

3. 🔍 Editor Agent

Another AssistantAgent named editor is in charge of:
	•	Reviewing the article.
	•	Listing improvements — but not rewriting the article!
	•	Uses a more strict, less creative config (temperature=0) for accuracy.

⸻

4. 🙋‍♂️ User Proxy Agent

This agent simulates you — the human in charge:
	•	Reads the conversation.
	•	Ends the session by typing a message ending with TERMINATE.

⸻

5. 💬 Group Chat Begins!

We bring the agents together in a GroupChat, controlled by a GroupChatManager.

The conversation flow:
	•	You initiate the topic (e.g., “Write an article about Large Language Models”)
	•	The writer writes 🖊️
	•	The editor gives feedback 📋
	•	The writer corrects 🛠️
	•	You observe or end it 👀

⸻

🧾 Example Prompt:

            user_proxy.initiate_chat(
    manager, 
    message="Write an article about Large Language Models"
)


📁 Files
	•	Chat.py: Main script with all the logic.
	•	OAI_CONFIG_LIST: JSON file with OpenAI model and API key info (make sure to add your API key!).


 💡 Why This is Cool
	•	It’s a working demo of multi-agent collaboration.
	•	It shows how roles and prompts guide agent behavior.
	•	You can expand it — maybe add a Fact-Checker Agent, or a Publisher Agent next?

⸻

✨ Future Ideas
	•	Add support for Claude or Mistral via different config.
	•	Let the user give real-time feedback during the chat.
	•	Save chat transcripts to a file.

