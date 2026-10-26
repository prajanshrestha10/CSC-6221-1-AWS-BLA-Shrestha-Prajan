# CSC-6221-1 BLA - AWS Managed AI Services

## 📌 BLA Number and Title
* **BLA Number:** BLA-14
* **Title:** AWS Certified Machine Learning Associate - Part 14: AWS Managed AI Services (Comprehend, Polly, Transcribe, Rekognition & Lex)

---

## 🎯 Purpose of the Activity
The main purpose of this activity is to explore AWS Managed AI services ("Intelligence as an API") and understand how pre-trained cloud models can be leveraged via simple API calls without requiring machine learning expertise or manual model training. The lab focuses on deconstructing five core managed services (Comprehend, Polly, Transcribe, Rekognition, and Lex), chaining them together for complex workflows, and determining when to choose managed AI services versus custom training in Amazon SageMaker.

---

## 🛠️ AWS Services, Tools, Languages, Databases, or Technologies Used
* **AWS Managed AI Services:** Amazon Comprehend, Amazon Polly, Amazon Transcribe, Amazon Rekognition, Amazon Lex
* **Integration & Compute Tools:** AWS Lambda, REST APIs, SDKs
* **Data Types Handled:** Text, Audio (Speech/Voice), Images, Video

---

## 💡 Concepts Learned
* **What Are Managed AI Services?** Pre-trained intelligence models managed entirely by AWS and accessed via simple API calls. They require zero machine learning expertise or infrastructure maintenance, scale automatically, and follow a pay-as-you-go pricing model.
* **Amazon Comprehend (Text $\rightarrow$ Insights):** Analyzes text to provide sentiment analysis (positive, negative, neutral, mixed), entity recognition (people, places, organizations), key phrase extraction, language detection, PII detection for redaction, and custom classification.
* **Amazon Polly (Text $\rightarrow$ Speech):** Converts text into lifelike spoken audio using advanced neural voices across multiple languages, featuring SSML (Speech Synthesis Markup Language) control for pauses and speed, alongside custom lexicons.
* **Amazon Transcribe (Speech $\rightarrow$ Text):** Transcribes recorded audio files or live streaming audio into text, incorporating speaker identification, custom vocabularies for domain-specific terms, language identification, and automatic redaction.
* **Amazon Rekognition (Image/Video $\rightarrow$ Labels):** Analyzes visual media to detect objects, scenes, and text inside images, perform facial analysis and comparisons, execute content moderation to flag unsafe content, and train custom labels.
* **Amazon Lex (Conversation $\rightarrow$ Bot):** Builds conversational chatbots and voice bots powered by Alexa technology, mapping user **utterances** to **intents**, collecting required **slots**, and executing **fulfillment** actions (often via AWS Lambda).
* **Combining Services for Multi-Modal Workflows:** Chaining individual APIs together (e.g., Transcribe call audio $\rightarrow$ Comprehend sentiment analysis $\rightarrow$ Lex query handling $\rightarrow$ Polly spoken response).
* **Managed AI vs. Amazon SageMaker:** Managed AI services are ideal for standard tasks (sentiment, speech, image labels) when fast results without ML expertise are required. In contrast, Amazon SageMaker should be used when building custom models requiring full control.

---

## 🏗️ Architecture or Design Description

```
+-----------------------------------------------------------------------------------+
|                           AUDIO INPUT (Call Recordings)                           |
+-----------------------------------------------------------------------------------+
|
v
+-----------------------------------------------------------------------------------+
|                        1. AMAZON TRANSCRIBE (Speech to Text)                      |
|                           (Turns call recordings into text)                       |
+-----------------------------------------------------------------------------------+
|
v
+-----------------------------------------------------------------------------------+
|                        2. AMAZON COMPREHEND (Text Analysis)                       |
|                          (Finds sentiment and key issues)                         |
+-----------------------------------------------------------------------------------+
|
v
+-----------------------------------------------------------------------------------+
|                        3. AMAZON LEX (Conversational Bot)                         |
|                         (Runs a chatbot for common questions)                     |
+-----------------------------------------------------------------------------------+
|
v
+-----------------------------------------------------------------------------------+
|                          4. AMAZON POLLY (Text to Speech)                         |
|                            (Speaks the answers aloud)                             |
+-----------------------------------------------------------------------------------+
```

---

## 📋 Major Steps Completed
1. Evaluated the operational model of AWS Managed AI services ("Intelligence as an API") and reviewed pricing and scaling advantages.
2. Configured Amazon Comprehend API calls to process customer reviews for sentiment analysis, PII redaction, and entity extraction.
3. Implemented Amazon Polly text-to-speech workflows utilizing neural voices and SSML control tags for e-learning narration.
4. Set up Amazon Transcribe batch and streaming jobs with custom vocabularies to process audio files.
5. Analyzed image and video assets using Amazon Rekognition for object detection and content moderation.
6. Designed an Amazon Lex conversational bot defining intents, utterances, slots, and Lambda fulfillment functions.
7. Chained Transcribe, Comprehend, Lex, and Polly into an integrated multi-modal customer support pipeline.

---

## ⚠️ Problems or Errors Encountered
* **Domain-Specific Vocabulary Misinterpretations:** Amazon Transcribe initially failed to correctly spell specialized medical or technical terms during audio-to-text conversion.
* **Rigid Conversational Flow in Chatbots:** Initial Amazon Lex bot configurations failed to capture user requests when utterances drifted outside predefined phrasing templates.

---

## 🔧 How Those Problems Were Resolved
* **Custom Vocabulary Integration:** Uploaded domain-specific terminology lists into Amazon Transcribe's **Custom Vocabulary** feature, which successfully boosted recognition accuracy for industry jargon.
* **Utterance Expansion & Slot Training:** Added diverse alternative phrases, synonyms, and conversational variations to Lex **utterances** and configured mandatory **slots** to ensure smooth intent fulfillment.

---

## 📊 Results or Output
* Fully functional, serverless AI integration pipeline capable of transcribing speech, analyzing text sentiment, managing conversational intents, and synthesizing speech responses.
* Clear architectural decision framework distinguishing when to apply pre-trained managed AI APIs versus building custom models in SageMaker.

---

## 🤔 Lessons Learned / Reflection
AWS Managed AI services remove the heavy lifting of building, training, and maintaining machine learning models for standard operational tasks. By treating intelligence as simple API endpoints, developers can rapidly integrate text understanding, speech synthesis, transcription, computer vision, and conversational bots into applications without deep data science expertise. When custom tailoring or specialized model control is required, practitioners can seamlessly transition to Amazon SageMaker.

---

## 🔗 YouTube Link(s)
* *[Insert your YouTube presentation/lab video link here]*

---

## 💼 LinkedIn Post Link(s)
* *[Insert your LinkedIn project/reflection post link here]*

---

## 📚 References or Resources Used
* AWS Certified Machine Learning Associate Part 14 Presentation Deck
* AWS Documentation: [What are AWS AI Services?](https://docs.aws.amazon.com/machine-learning/latest/dg/what-is-ml.html)
The multi-modal customer support pipeline illustrates how multiple managed AI services can be chained together using simple API calls:
