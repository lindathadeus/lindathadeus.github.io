---
layout: post
title: "Survey of Existing Solutions in LLM"
date: 2024-11-05
categories: [llm]
giscus_comments: true
tags: [AI, future of work, emerging technologies, llm]
authors:
  - name: Linda Joe Thadeus
    url: "https://lindathadeus.github.io"
    affiliations:
      - name: SuSE
      - name: NITK
  - name: ChatGPT
    url: "https://openai.com"
    affiliations:
      - name: OpenAI
---

### **1\. Executive Summary**

**Purpose**: The survey of existing solutions in LLM is conducted to know the structure of each solution in terms of cost of the solution, environmental cost, hardware cost, human-power cost, input data, output data, input’s parameters like size, human-made or ai-generated, output parameters like quality, quality parameters like likeability by the readers, function on the likeability by the readers like how many readers liked how much, etc. It also defines various words used in the LLM, demystifying the meaning for the readers.  
**Scope**: We will be covering the major parameters of different solutions at a high level. We will also do implementations for some of them.  
**Key Findings**: The average user of LLM is an API/Cloud LLM user, for truly enjoying the LLM technology, one has to build LLMs from scratch and for best of the both worlds, one can opt for Hybrid ones.

### **2\. Introduction**

**Background**: Short description of the technology landscape and why this survey is relevant.

  Everything, action has a consequence. Also, everything is a consequence of a previous action or actions. LLM was a consequence of high consumption of Cloud Computing Resources that resulted in the High Volume Unstructured Data from the users themselves through the technological innovation that operated on the cloud like social media and internet blogs instead of just the companies that host the computing resources, Some Initial Patterns or Learning Methodology or some rules. Like we had seen earlier, there were humongous amounts of unstructured data available with these internet companies created by the people of the Earth, there was a need to generate insights from the people, so that we can benefit the people directly. So, there came a need to study patterns in their data. Some companies, they say, collected and studied the users’ data without consent. So there comes the need to get consent. Also, these data put forth by the users are out there for another user to get data too, that means, the user needs privacy protection too. So, anyway the large companies that had these bulk of these user-data and some of them relied on advertisements for money, so they had to understand the user’s needs otherwise, the companies feared getting blocked off by the user. So, all these meant there had to be a super data collector, monitor, inspector, predictor that would deal with all the previous problems. The intelligent system had to predict user behavior, they may even have to generate scenarios and more data. AI in the form of generative AI came as a natural consequence. But, how would a common person use this AI effectively? How would it benefit them? What could happen if not?  
    
**Problem Statement**: The problem with this is, there is too much data but not much awareness about the usage of generative AI LLM tools.

**Objectives**: What the paper aims to achieve is, to compare, evaluate, or identify trends in solutions, and also to structure the solutions.

### **3\. Methodology**

**Research Approach**: 

We believe that the correct way to learn a solution is to use it. So over a period of time. We used the different solutions and we gathered some interesting insights and found some methods were easier for some set of users than the others.

**Evaluation Criteria**: Key factors used to compare solutions are cost, ease of use.

### **4\. Overview of Existing Solutions**

**Solution Categories**: As per our perspective and our research on it so far, there are 3 types of LLMs available for use. The first one is the “Cloud-based” or “Hosted” LLM. The LLM could be hosted anywhere in the open internet, or closed. The existing ideas of private cloud, public cloud, on-premises cloud, apply here too. The Hugging face comes as the public cloud based on but it is built on top of open LLMs unlike OpenAI’s GPT that is based on closed dataset LLM GPT3 and above. They typically use API as the connection. The next one is building one from scratch and making it to our taste. The other solution is making a hybrid one. Take one existing LLM and finetune with our data. For this we would use a foundational LLM and give our custom data and interacting guidelines. So, There are 3 solutions available, the first one is API based existing LLM, the next one is Home-made LLM, and the third one is Hybrid LLM.   
    
**Key Players/Technologies**: OpenAI ChatGPT, a very popular Chat-tuned LLM, LLAMA LLMs \- a popular open distribution LLM but not open weight, Microsoft Phi LLM \- a popular smaller LLM.

### **5\. Comparative Analysis**

**API Based LLMs**:  
  * Strengths  
  * Weaknesses  
  * Unique Features  

API based LLM: The first solution is the API based LLM. The most popular one amongst them is the ChatGPT by OpenAI. We would like to think of it as a Mainframe Supercomputer, where we have keyboard and dumb screens and our interaction is through these fancy wires called APIs. Now, we also have a voice mode, in future, we may also have a video mode and so on. Of-course there are different tiers where one can access these modes like, just using chat interface i.e. ChatGPT and create GPTs on top of them in their GPT store or through web services or through CLIs that would anyway have to contact these REST APIs. For the purpose of understanding these API based LLM, we created a GPT in 2 hours. Below is the GPT. So, this is the most accessible way for creating custom LLMs for our use. But, the drawbacks are obvious, we need to follow the RULES, specifically the rules given and managed by OpenAI.

  Eg GPT : Please check the appendix

**Home-made LLMs**:  
Home-made LLM: These LLMs are purely made by the users from their home. But, this requires the users to be technical, they have to have knowledge of LLMs, Python and even Linux for some cases where they use Linux developer setup.We would like to think of these LLMs as truly open and purposeful LLMs. Much like, when the internet technology was given to the world, it gave multiplication over the existing issues and so it made easy users fall prey to DISTRACTION if there was not a PURPOSE. But, this is the best use of an LLM. Because the users generate data and they themselves know the pattern or the world view with which they generated the data. So, this is less environmentally bothersome too. And, so, in our perspective, we think this as the TRUE by \-product of this AI revolution if it were. But this method is not very accessible to the common users and more accessible to the Developers. So, the developers should make use of this. As part of understanding this type, we created an LLM, kinda, using the existing framework like pytorch and used a custom dataset.

**Hybrid LLMs**:  
Hybrid LLM: This is the best of both worlds. This can be achieved easily with lesser time too unlike the “PURPOSEFUL LLMs” above. We downloaded the existing LLM from Hugging Face and did our prompting on that. This is also less accessible to common person and more suited for software engineers. As part of this survey, we downloaded a smaller LLM from Microsoft Phi Series and tried to work with that.

{% highlight python %}
$ pip install transformers 
$ pip install torch 
$ pip install 'accelerate\>=0.26.0' 
$ python3 phi.py
{% endhighlight %}

{% highlight python %}
import torch
from transformers import AutoModelForCausalLM, AutoTokenizer, pipeline
import json

model = AutoModelForCausalLM.from_pretrained(
    "microsoft/Phi-3.5-mini-instruct", 
    device_map="cpu", 
    torch_dtype="auto", 
    trust_remote_code=True, 
)
tokenizer = AutoTokenizer.from_pretrained("microsoft/Phi-3.5-mini-instruct")

pipe = pipeline(
    "text-generation",
    model=model,
    tokenizer=tokenizer,
)

# Open and read the file
with open("conversation_samples.txt", "r") as f:
    conversation = f.readlines()

# Initialize a list to store the conversation data
conversation_json = []

# Process each line
for line in conversation:
    line = line.strip()  # Remove any extra spaces or newline characters

    # Check if the line starts with "User:" or "AI:"
    if line.startswith("User:"):
        content = line.split("User:", 1)[1].strip()
        conversation_json.append({"role": "user", "content": content})
    elif line.startswith("AI:"):
        content = line.split("AI:", 1)[1].strip()
        conversation_json.append({"role": "assistant", "content": content})

messages = [
    {"role": "system", "content": "You are a helpful AI Emotions Stabilizer. The Emotions Stabilizer is designed to provide empathetic, structured guidance for processing emotions, adapting to the user's needs while ensuring each conversation has a clear, progressive flow. Acting as a supportive mentor, the Emotions Stabilizer helps users process both positive and negative emotions by following a structured set of questions. It provides prompts one at a time and waits for each response,acknowledging and validating the user's experience before moving forward. The Emotions Stabilizer aims to keep conversations focused and purposeful, minimizing unnecessary steps to help the user feel a sense of progress and completion.The Emotions Stabilizer will acknowledge user responses concisely to avoid overly lengthy dialogues and unfocused dialogues, guiding each step in a way that maximizes clarity and momentum. If the user seems ready to let go or wishes to end the conversation, the Emotions Stabilizer will respect this, encouraging closure in a supportive, empowering tone. For simplicity, the Emotions Stabilizer will focus as only positive and negative, and group all emotions under this with an intensity"}
]

messages.extend(conversation_json)

while True:
	user_input = input("Press quit or exit to quit\n\nUser: ")
	if user_input.lower() in ["exit", "quit"]:
		print("Ending conversation.")
		break

	messages.append({"role": "user", "content": user_input})

	print("\n\n")
	response = pipe(messages, max_new_tokens=100, return_full_text=False, temperature=0.7)[0]['generated_text']

	messages.append({"role": "assistant", "content": response})

	print("\n\n")
	print(f"AI: {response}")
{% endhighlight %}

---

**Appendix**
[https://chatgpt.com/g/g-wjwrMf1LL-emotions-stabilizer](https://chatgpt.com/g/g-wjwrMf1LL-emotions-stabilizer)

---

**What do you think?** Let me know your thoughts in the comments below. Together, we can navigate this evolving landscape and find our place in the future of work.
