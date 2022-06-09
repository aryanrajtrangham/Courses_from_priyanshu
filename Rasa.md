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
- Rasa has inbuilt models for doing this

## Process Pipeline Notes
- Define the processing stages the incoming user messages will have to go through untill the model output is produces.
- Sequence Matters!
- Rasa NLU, by default, comes with a bunch of prebuilt components (& even pipelines) for us to use.
- Once the pipeline is defined: Each component is called once after another & produced the output which is either directly added to Rasa NLU model output, or used an input or other components.

## Training Notes
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
- ### **Q. When to use Pre-trained model as a starting point**
    - Pre-trained model is used on similar language & domain dataset.
    - This process will tend to work of the features are general, meaning suitable to both base and target tasks, instead of specific to the base task.
- ### **Advantages**
    - Better model performance with less training data required.
    - Faster training with less iteration times.
    - Lower training data required for the task at hand.
    - When the pre-trainined model is from the same domain, it will pick up domain specific vocabulary.
