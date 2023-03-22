# Rasa

## RASA NLU (Natural Language Understanding) and NLP (Natural language Processing)

- Understand user's input which is usually unsructered text.
- **Output :** Structure Data for furtther processing
  - Intent
  - Entities

- ### Intent

  - An intent is the intention of the user, or the users, interacting with the chatbot
  - We use a supervised learning approach of training an sentence classifier.
  - Intent classification is nothing but Training a Classifier.
  - Intent is the pridicted class of the user's input.
    Example                       | Class
    ------------------------------|------------
    What's the price of Iphone X? | ask_price
    Can you please tell me the price of Iphone X? | ask_price
    How much does Iphone X cost?  | ask_price
    How much can I buy an Iphone X for | ask_price

- ### Entities

  - Entities are objects /topic useful in further knowing the purpose of User's inputs.
  - What's the price of **Iphone X**?
    - We figures user wants to know the price through intent classfication. But Price of what?</br>
        Iphone X <- Entity (Smartphone)

## Installation options

- Rasa will run on python < python3.9
- Installed packages
  - rasa
  - spacy
  - rasa-x --extra-index-url <https://pypi.rasa.com/simple>
- Installed packages dependencies
  - spacy download en_core_web_md

## Rasa NLU Pipeline

- A sequece of processing steps used to extract specific text features & train certain components which allow the model to learn the underlying patterns from the provided examples.
- So in RASA, we can define the steps for classifying an intent and extracting entities.
- Rasa has inbuilt models for doing this.
- This is done in a config.yml file.

## Process Pipeline Notes

- Define the processing stages the incoming user messages will have to go through untill the model output is produces.
- Sequence Matters!
- Rasa NLU, by default, comes with a bunch of prebuilt components (& even pipelines) for us to use.
- Once the pipeline is defined: Each component is called once after another & produced the output which is either directly added to Rasa NLU model output, or used an input or other components.

### **Training Notes**

- Class Imbalance:
  - Some Intents might have significantly more training examples than others. It's likely to affect your model and make them perform poorly.
    - Make sure we have more or less similar amount of examples for each intent.
    - Rasa inbuilt users balanced branching strategy, it tries to make sure.
- Punctuation like ,;"' { smiley } are ignored by Rasa while training.
- Named Entity Recognition is Case Sensitive (but customizable).
- Intent classifier is Case Insensitive by default.

## Custom Components

- Rasa provides good in-built NLU models for intent classification and entity extraction.
- It comes with an option of making our using and using our own components.
  - Use Case: If we want to use a pretrained embedding model trained on user reviews, then we can use it while training our embeddings.
  - Use Case: If we want to censor the language of the user while he is talking! , we can use a language censor or a profanity filter...

## Types of custom components

- Components which are already trained models.
  - For example, trained on different datasets & packaged as python libraries, .pkl files, .models files.
- Components which train on rasa NLU training data and improve example's or add more of them.

## Adding Custom Components

- Adding Custom components to the NLU pipelines is a process of
  - Implementing the custom component class with the necessary methods.
  - Referencing it inside the Rasa NLU pipeline configuration file.</br>
  or
  - For some pretrained models, just mention them in the configuration File.

## Transfer Learning

- Tranfer learning is a machine learning method where a model developed for a task is reused as the starting point for a model on a second task.
- We first train a base network on a base dataset and task, and then we repurpose the learning features, or transfer them, (i.e, use the pretrained models as the starting point) to a second target network to be trained on a target dataset and task.

- ### **Pre-trained Word Embeddings**

  - It is common to perform transfer learning with natural language processing problems.
  - In NLP transfer learning is generally done through pretrained word embeddings.
  - Word embeddings are a type of word representation that look **context of words** which allow words with similar meaning to have similar vector represnetation.
  - Words like smart phone and mobile are considered similar if there's enough evidence in the data they appear in similar context.Thus, giving us options to augment our current model with new information which otherwise wouldn't be present in the existing model, which in turn increase the model classification accuracy as well as the coverage of the vocabulary.

- ### **Q. When to use Pre-trained model as a starting point ?**

  - Pre-trained model is used on similar language & domain dataset.
  - This process will tend to work of the features are general, meaning suitable to both base and target tasks, instead of specific to the base task.

- ### **Advantages**

  - Better model performance with less training data required.
  - Faster training with less iteration times.
  - Lower training data required for the task at hand.
  - When the pre-trainined model is from the same domain, it will pick up domain specific vocabulary.

## Rasa Core

- Rasa core predict what bot should say for a given user input.
- We cannot write rules for every path.
- Instead of using rules & enforcing them on the user, Rasa uses machine learning to learn the conversational patterns from the **example conversational data** we provide & predict how an assistant should respond in a specific situaton based on the context history of the converaton and other details like the **Policies** defined by us.
- Generally this process of handling conversation flow and responding in a chatbot is called **Dialogue Management**.

- ### **Responses**

  - Similar to how field defined user inputs, we have to define are bored responses.
  - These are set for word/replies and are picked based on prediction by the policies.
  - Actions & Utterances
    - Response is either defined as **Utterances** or **Actions**.
    - Utterances: Hard coded Messages.
      - Can have multiple messages per utterance.
      - Examples: utter_greet:
        - "Welcome. How can I help you?"
        - "Hey, how are you doing?"
      - Various Formats:
        - Text
        - Images
        - Buttons
    - Actions: Allow to use Python code
      - Call the DB
      - Calling an API
      - Writting to the DB
      - Do some calculations

- ### **Stories**

  - Example coonversations between the user & assistant
  - We can have multiple stores
  - Each story is a sample conversation the bot can have with the user.
  - Provides training data for the Dialogue Management System of Rasa.
  - You do not have to deal with the specific contents of the messages that the users send.
    - Use just the combination messages the users can send to mean the same thing.
    - Policies learn to predict the next action based on a **combination** of both the intent and entities.
    - Can change this behaviour using the **use_entities** attribute.

- ### **Domain**

  - Domain is the universe in which the bot operates. It defines all the things your bot should know about.
  - Has Intents: What the user means
  - Responses: What the bot should say
  - What Info: to remember
  - What entities to extract

- ## **Rules**

  - Rules are a type of training data used to train your assistant's dialogue management model. Rules describe short pieces of conversation that should always follow the same path.
  - Rules are better to handle small specific conversation patterns, but unlike stories, rules do not have the power to generalize unseen conversation path.
  - Combine rules and stories to make your assistant robust and able to handle real user behavior.
  - We can have conditions with the rules or have rules for conversation start.

- ## **Dialogue Policies**

  - A policy is responsible for making a decision of how an Assistant should respond next.
  - Not always we use Machine Learning to predict the next action/response.
  - Apart from Machine Learning we have certain other policies defined which help us with other policies which help us with selecting the next response.
  - **Max History**
    - One important hyperparameter for Rasa Core policies is the max_history. This controls how much dialog history the model looks at to decide which action to take next.
    - So if we keep it 1, it will just go one step back to decide what to do. Won't use the previous dialogues as context.
    - This number we set depends on the length of our training stories& the patterns we would like to remember.
    - Don't keep it too long. If we want our assistant to take far back in history we should set those details as slots.
  - **Data Augmentatio**
    - An amount of new stories to create from the existing stories
    - Rasa creates longer longer stories by putting together some shorter stories.
    - Improves theperformance of our models.
    - Allow dialogue management to ignore history of the conversation.
    - Can increase training time.
  - **Memoization Policy**
    - Mimics the stories it was trained on.
    - Depending on what max. history parameter was set, it tries to match the fragement of the current story with the stories provided in the training data.
      - If it finds one, it predicts the next action from the map story with confidence one else it predicts confidence zero.
    - This is usually combines with other policies.
    - Optimized for its precision & not for recall.
  - **Mapping Policy**
    - Allows to add business logic
    - Specific intent cn be followed by a specific action, regardless of what happened in the conversation.
      - Intents:
      - Ask_whats_time:
        - Triggers: action_check_time
    - An intent can only be mapped to at most one action.
    - Once the mapped action is executed the prediction of next responses are handed over to the other policies in the config.
    - Predictions of mapping policy are taken into consideration by default by other policies for meeting predictions.
  - **Keras Policy**
    - Uses Deep Learning to predict Next Action.
    - Features used:
      - what the last action was.
      - What intents & entities were predicted for the current user input.
      - What slots are set
      - Takes Previous states of dialogue based on max_hostory.
    - Default Architecture
      - LSTM
      - Can again change this architecture
    - Learns from training stories we provide.
    - Hyperparameters:
      - max_history
      - Eposhs
      - Validation_split
      - random_seed
      - batch_size
  - **Sklearn Policy**
    - Uses machine learning models to predict the next action.
    - Default model
      - Logistic Regression
  - **Embedding (TEDP) Policy**
    - Uses transformers instead of RNN's
    - Outperforms other policies
    - Simple architecture & Faster
    - Handles chitchat
  - **Fallback Policy**
    - Sometimes users may say something the bot isn't designed to do.
    - Users may provide inputs which makes NLU models confused. Maybe because of not having enough information.
    - Important for assistant to acknowledge this situation
    - Using the Fallback policy we can fallback to a message whenever the bot isn't confident sbout what the user saying.
    - For that we need to define thresholds
    - Fallback Policy
      - nlu_threshold: 0.3
      - Ambiguity_threshold: 0.1
      - Core_threshold: 0.3
      - Fallback_action_name: 'action_default_fallback'
      - **Ambiguity threshold**: Define the difference between the predicted and next action
  - **Policy Priority**
    - Our policy configurations usually contains multiple policies.
    - So, policy with highest confidence score of prediction wins
    - If multiple policies predict the next action with same confidence score. what to do?
    - We rank the policies:
      - **Rank 1**: Form Policy
      - **Rank 2**: Fallback Policy and TwoStageFallbackPolicy
      - **Rank 3**: Memoization Policy and Augmented Memoization Policy
      - **Rank 4**: Mapping Policy
      - **Rank 5**: Embedding Policy, Keras Policy & Sklearn Policy
    - Can be changed but recommended to use Dafault

## Slots

- Slots are basically bots memory.
- Using them we can keep important things the bot has to remember for a later part of the conversation
- Defining slots
  - Through Entities:
    - Can remember important values providedby users through Entities
  - Custom Actions
    - Info from the outside for examples results extracted from the external database

- ### **Types of slots**

  - **Text**
    - Basically a string
    - What matters here is if the slot is set or not.. The value of the slot doesn't matter.
    - Useful in modeling situations when the dialog should take a different turn based on whether or not users provided specific details.
    - For example. We just want to know if an entity is given or not. If yes the bot can move forward.
  - **Bool**
    - Value matters, Check if its True or False
      - Slots: is_authenticated -> type:bool
    - Dialogue Management looks at value and presence while making a prediction for next step.
  - **Categorical**
    - Slots which can take one of **N** values.
      - Slots: Color -> type: categorical
      - Value:
        - Low
        - Medium
        - High
    - Dialogue Management looks at value and presence while making prediction for next step.
  - **Float**
    - Presence & value matters.
      - Slot: Price -> type: float
        - Min_value : 0.0
        - Max_value : 1000,000
  - **List**
    - If you want to store multiplt values in a given slot, (coz by default one slot can store one value at a time..) we can use lists.
    - A list/array for multiple values.
    - Length doesn't matter but if the value is set or not matters.
    - To only store some info. For your assistant to use in specific actions or in later stages.
    - Presence & value of the slot will have no influence on how a dialog management model makes the predictions.

- ### **Slot Types & their influnce on Dialogue Predictions**

  - Slot Type     | Value Presence    | Actual Value
      ------------|-------------------|---------------
      Text        | Yes (Tick)        | No (X)
      Bool        | Yes (Tick)        | Yes (Tick)
      Categorical slot | Yes (Tick)   | Yes (Tick)
      Float       | Yes (Tick)        | Yes (Tick)
      List        | Yes (Tick)        | No (X)
      Unfeaturized | No (X)           | No (X)

- Slots can be used in utterance templates
  - { phone_name }
- Can be used in Custom Actions
  - tracker.get_slot('phone_name')
- Can se set using Custom Actions
  - return [SlotSet('phone_name','iphone X')]
- Slots which are set using custom actions have to be reflected in training stories.
  - action_set_phone
  - slot["phone_naem":"iphone X"]
- In this case we do have to include the - slot{} part in the stories. Rasa Core will learn to use this information to decide on the correct action to take.
- All slot have to be listed in the domain.
- Slot values are kept in memory untill they are reset.

## Rasa - Forms

- One of the most common conversation pattern is to collect a few pieces of information from a user in order to do something. This is also called **slot filling**.
- If you need to collect multiple pieces of information in a row, we should use a Form Action.
- This is a single action which contains the logic to loop over required slots and ask the user for this information.

- Forms in v2 are defined in domain.
- Define slot mapping for each slot which your form should fill.
- Can specify one or more slot mapping for each to be filled.
- For validation and custom slot mappings we can define a Form Action Class in actions.
- Rasa tries to decouple smple forms and advanced functionality or the need to use Python.

- ### **Form Action in Stories**

  - With form{"name": "product_search_form"} the form is activated.
  - With form{"name": "null"} the form is deactivated again.
  - form_1
    </br>buy_phone_laptop
    - product_search_form
    - form{"name": "product_search_form"}
    - form{"name": "null"}

- ### **Featurized vs Unfeaturised Slots & Stories**

  - Note that for story to work, your slots should be <u>unfeaturized</u>.
  - If any of these slot are featurized, your story needs to include slot{} events to show these slot being set.
  - In that case, the easiest way to create valid stories is to use <u>Interactive Learning</u>.

- ### **Form Policy**

  - Once the form action gets called for the first time, the form gets activated and the Form Policy jumps in.
  - The Form Policy is extremely simple and just always predicts the form action.

- ### **Submit**

  - We can define a rule which can run an action. Once all the slots are filled.
  - Once all the slots are filled, the submit() method is called.
  - Here we can use the information collected to do something for the user.
  - For example querying the database and making the product search.

- ### **Custom slot Mappings**

  - By default slots will be only filled by entities with the same name as the slot that are picked from the user input.
  - The **slot_mappings** method defines how to extract slot values from user responses.
  - The predifined functions work as follows:
    - **from_entity :**
      - self.from_entity(entity=entity_name, intent=None) // Rasa 2.0
      - \- type: from_entity //Rasa 3.0
        - will look for an entity called entity_name to fill a slot slot_name regarless of user intent.
      - slef.from_entity(entity=rntity_name, intent=intent_name) //Rasa 2.0
      - \- type: from_entity</br>
          entity: entity_name //Rasa 3.0
        - will look for an entity called entity_name to fill a slot slot_name only if the users intent is intent_name.
    - **from_intent :**
      - self.from_intent(intent=intent_name, value=value) //Rasa 2.0
      - \- type: from_intent</br>
          value: my_value
          intent: intent_name // Rasa 3.0
        - will fill slot slot_name with value if user intent in intent_name.
    - **from_text :**
      - self.from_text(intent=None) // Rasa 2.0
      - \- type: from_text</br>
          intent: None // Rasa 3.0
        - will use the next user utterance to fill the text slot slot_name regardless of user intent.
      - slef.from_text(intent=intent_name) // Rasa 2.0
      - \- type: from_text</br>
          intent: intent_name // Rasa 3.0
        - will use the next utterance to fill the text slot slot_name only if user intent is intent_name.
    - If we want to allow a combination of these, provide them as a list.

- ### **Handling conditional slots logic**

  - Many forms required more logic just requesting a list of fields.
  - For example, if someone requests laptop as their category, we may want to ask questions on slighly different features than phones, we may be asking for Camera specification.
  - We can achieve this by writing some logic into the required_slots() method. // in the action.py file

- ### **Validation**
  
  - By default, validation only checks if the requested slot was successfully extracted from the slot mappings
  - If we want to add custom validation, for examlpe to check against a database, we can do this by writing a helper validaiton function with name validate_{slot_name}.

## Small Talk

- Small talk includes the back-and-forth that makes conversations natural but doesn't directly relate to the user's goal.
- This includes greetings, acknowledgements, reactions and off-topic chithcat.

- ### **Chitchat**

  - Assistant will often receive unexpected or unprompted input.
  - For example: Users might ask
    - *"Whats your occupation?"*
    - *"Where do you stay?"*
  - While it's not possible to coherently respond to everything a user might say, we can make sure we answer some of the frequently asked off-topic questions.
  - For this, we should collect training data and define intents and responses for some of the more common topics.
  - Since we don't care about the context while answering these questions, we can map this intention using mapping policy.
  - **intents:**
    - **ask_occupation:**
      - **trigger :** action_occupation
  - We wouldn't want these questions to affect our normal conversation and would want the bot to continue with the flow once questions like these are answered.
  - For example, if a user asks "Where do you live?" off topic in the middle of the flow, we probably want to answer without that interaction affecting the next action prediction.
  - For this, apart from using Mapping Policy.
      1. We need to return UserUtteranceReverted() and ActionReverted() events from our mapped action.</br>
      This will delete the user's latest message, along with any events that happened after it, from the dialog history.
      2. Do not include the intent-action interaction in your stories.
      3. Just define it in the domain file intent and its trigger, always use actions. Even if it's simple message.

## Channel Specific Responses

- Every platform has some specific format/templlate set for specific messages.
- For example:
  - Facebook has quick replies for buttons similarly, Slack has different formats for buttons.</br>
    Or
  - For displaying products Facebook Messanger user Geric templates.</br>
    Or
  - A custom product display option on your website chatbot widget.
- We can create Channel specific responses using creating custom output payloads that will only work in certain channels.

- ### **Custom Output Payloads using Utterance Templates**

  - Can send any arbitrary output to the output channel using the **custom: key** in the utterance.
  - If you have certain response templates that would like to send only to specific channels, you can specify with the **channel: key**
  - Apart from this, Rasa in-built provides some custom outputs.
  - For example: Rasa has inbuilt quick replies for Facebook or Custom Buttons for Telegram.

- ### **Custom Output Payloads using Action**

  - If we want to send custom output payloads using actions:
    - Use the tracker method:
      - **tracker.get_latest_input_channel()**
  - Change the output payload based on the channel.

## External Events

- Suppose we want to send a remainder/alert whenever the prices drop.</br>
Or
- Send an alert to our employees whenever they forgot to log their attendance.
- Using the trigger_intent_endpoint API.
- We need to create a program external to Rasa & make it send messages to the **trigger_intent_endpoint** of our convertation whatever we want to send the alert.
