# Set Up Your AI Agent

Currently Epsilla supports two types of agents: Chatbot Agents and Smart Search Agents. Chatbot Agents provide an interactive experience similar to ChatGPT, generating context-aware responses for use cases such as customer support or domain-specific conversations, often tailored to specific knowledge bases. Smart Search Agents focus on efficient information retrieval, inspired by platforms like Perplexity. They excel in providing precise answers to user queries, making them ideal for use cases such as research, content discovery, and data-driven decision-making.

### **Navigate to the Application Tab**

In your Epsilla Cloud dashboard, click on the **Create Application** button located on the navigation bar.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 10.20.05 PM (1).png" alt="" width="256"><figcaption></figcaption></figure>

Or click on the **Applications** tab. This will lead you to the page where you can create and manage all your Applications.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 10.20.17 PM.png" alt="" width="563"><figcaption></figcaption></figure>

Select **Chatbot** as the application type from the available options.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 10.22.43 PM.png" alt=""><figcaption></figcaption></figure>

### **Add Application Details**

**Name Your Chatbot**: Enter a name for your chatbot that reflects its purpose.

**Provide a Description**: Add a description for your chatbot to indicate what kind of tasks or questions it is intended to handle.

**Upload a Logo** (Optional): For a personalized touch, upload a logo to represent your chatbot visually in the interface.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 10.23.30 PM.png" alt="" width="563"><figcaption></figcaption></figure>

The chatbot will be created in 15 - 30 seconds. Now you can preview the Chatbot and modify its configurations side by side:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 10.31.07 PM.png" alt=""><figcaption></figcaption></figure>

### **Define the Chatbot Role**

Technically this is the system prompt to instruct the LLM to behave with desired personality. For instance, if you're creating a tax assistant, you could use a system prompt like:

* "You are a professional CPA specializing in individual taxation. Utilize your expert knowledge of tax laws and regulations to ensure clients benefit from all applicable deductions and credits. Provide clear explanations to clients about their tax situations and the implications of their financial decisions."

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 10.32.01 PM.png" alt=""><figcaption></figcaption></figure>

This role setup is crucial as it helps ensure that the chatbot’s responses are aligned with your intended use case.

### **Add Knowledge to the Chatbot**

**Link the Knowledge Base**: Select the knowledge base you created and attach it to your chatbot. This ensures that the chatbot can ground its responses in the specific data you provided, making answers more relevant and accurate. You can add multiple knowledge bases to an AI agent.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 10.33.49 PM.png" alt="" width="563"><figcaption></figcaption></figure>

### **Config Appearance**

**Change Icon:** Select a new icon for your agent by uploading a custom image. Ensure the icon reflects your agent's purpose and aligns with your brand identity.

**Change Primary Color:** Customize the primary color to match your branding.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 10.41.35 PM.png" alt="" width="563"><figcaption></figcaption></figure>

### **Configure Chat Experience**

**Introduction Message**: Set an introductory message that the chatbot will use to greet new users. This helps set the context of the conversation.

**Chatbox Placeholder:** Set the placeholder text in the chatbox.

**Sample Questions**: Add sample questions for users to quickly get started. For example, for a tax assistant, questions could be like "What are the standard deductions?" or "How do I report freelance income?"

**Enable Follow-up Questions**: Allow users to ask follow-up questions during a conversation, providing a more interactive and engaging experience. If enabled, you can futther customize the LLM model and prompt for generating the follow up questions.

**How to Label a Chat:** Config how to label a chat. By default Epsilla will use LLM to summarize the a chat.

**Hide Epsilla Logo:** For a paid tier, you can choose to hide Epsilla logo from the Chatbot for white labeling.

**Collect User Feedback:** Whether allow users to provide feedback to the Chatbot response.

**Allow Message Sharing:** Whether allow other users to share the chat with others.

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 10.37.50 PM.png" alt="" width="563"><figcaption></figcaption></figure>

### **Test Your Chatbot**

You can test the chatbot in the right hand  side **Preview.** Test the chatbot in the interface to ensure it responds appropriately. Verify that it can answer questions using the knowledge base and that the defined role aligns with its response:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 10.45.48 PM.png" alt=""><figcaption></figcaption></figure>

Click the resize button <img src="../.gitbook/assets/Screenshot 2024-09-28 at 10.46.33 PM.png" alt="" data-size="line"> to make the preview full screen:

<figure><img src="../.gitbook/assets/Screenshot 2024-09-28 at 10.47.47 PM.png" alt=""><figcaption></figcaption></figure>
