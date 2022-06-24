## RASA NLU (Natural language Processing)
- Understand user's input which is usually unsructered text.
- **Output :** Structure Data for furtther processing
    - Intent
    - Entities
- ### **Intent**
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
- ### **Entities**
    - Entities are objects /topic useful in further knowing the purpose of User's inputs.
    - What's the price of **Iphone X**?
        - We figures user wants to know the price through intent classfication. But Price of what?<br>
        Iphone X <- Entity (Smartphone)


## Installation options
- Rasa will run on python < python3.9
- Installed packages
    - rasa
    - spacy
    - rasa-x --extra-index-url https://pypi.rasa.com/simple
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
    - Referencing it inside the Rasa NLU pipeline configuration file.<br>
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
            * Can be changed but recommended to use Dafault
