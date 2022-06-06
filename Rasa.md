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
        - Make sure you have more or less similar amount of examples for each intent.
        - Rasa inbuilt users balanced branching strategy, it tries to make sure.
- Punctuation like ,;"' <smileys> are ignored by Rasa while training.
- Named Entity Recognition is Case Sensitive (but customizable).





