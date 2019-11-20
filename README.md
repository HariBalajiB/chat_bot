# Simple ChatBot
Types of Chat Bot's
In the world of machine learning and AI there are many different kinds of chat bots. Some chat bots are virtual assistants, others are just there to talk to, some are customer support agents and you've probably seen some of the ones used by businesses to answer questions. For this tutorial we will be creating a relatively simple chat bot that will be be used to answer frequently asked questions.

Install Packages
Before starting to work on our chatbot we need to download a few python packages. Please note as of writing this these packages will ONLY WORK IN PYTHON 3.6. Hopefully this will be fixed in the future.
We will simply use pip to install the following:
- numpy
- nltk
- tensorflow
- tflearn

Simply go to CMD and type: pip install "package name". Where you will replace "package_name" with all of the entries listed above.

Training Data
Now it's time to understand what kind of data we will need to provide our chatbot with. Since this is a simple chatbot we don't need to download any massive datasets. We will just use data that we write ourselves. To follow along with the tutorial properly you will need to create a .JSON file that contains the same format as the one seen below. I've called my file "intents.json".What we are doing with the JSON file is creating a bunch of messages that the user is likely to type in and mapping them to a group of appropriate responses. The tag on each dictionary in the file indicates the group that each message belongs too. With this data we will train a neural network to take a sentence of words and classify it as one of the tags in our file. Then we can simply take a response from those groups and display that to the user. The more tags, responses, and patterns you provide to the chatbot the better and more complex it will be.

Loading our JSON Data
We will start by importing some modules and loading in our json data. Make sure that your .json file is in the same directory as your python script!

Extracting Data
Now its time to take out the data we want from our JSON file. We need all of the patterns and which class/tag they belong to. We also want a list of all of the unique words in our patterns (we will talk about why later), so lets setup some blank lists to store these values.Now its time to loop through our JSON data and extract the data we want. For each pattern we will turn it into a list of words using nltk.word_tokenizer, rather than having them as strings. We will then add each pattern into our docs_x list and its associated tag into the docs_y list.

Word Stemming
You may have heard me talk about word stemming in the previous tutorial. Stemming a word is attempting to find the root of the word. For example, the word "thats" stem might be "that" and the word "happening" would have the stem of "happen". We will use this process of stemming words to reduce the vocabulary of our model and attempt to find the more general meaning behind sentences.

Bag of Words
Now that we have loaded in our data and created a stemmed vocabulary it's time to talk about a bag of words. As we know neural networks and machine learning algorithms require numerical input. So out list of strings wont cut it. We need some way to represent our sentences with numbers and this is where a bag of words comes in. What we are going to do is represent each sentence with a list the length of the amount of words in our models vocabulary. Each position in the list will represent a word from our vocabulary. If the position in the list is a 1 then that will mean that the word exists in our sentence, if it is a 0 then the word is nor present. We call this a bag of words because the order in which the words appear in the sentence is lost, we only know the presence of words in our models vocabulary.
As well as formatting our input we need to format our output to make sense to the neural network. Similarly to a bag of words we will create output lists which are the length of the amount of labels/tags we have in our dataset. Each position in the list will represent one distinct label/tag, a 1 in any of those positions will show which label/tag is represented.
Finally we will convert our training data and output to numpy arrays.

Developing a Model
Now that we have preprocessed all of our data we are ready to start creating and training a model. For our purposes we will use a fairly standard feed-forward neural network with two hidden layers. The goal of our network will be to look at a bag of words and give a class that they belong too (one of our tags from the JSON file).We will start by defining the architecture of our model. Keep in mind that you can mess with some of the numbers here and try to make an even better model! A lot of machine learning is trial an error.

Training & Saving the Model
Now that we have setup our model its time to train it on our data! To do these we will fit our data to the model. The number of epochs we set is the amount of times that the model will see the same information while training.

Loading a Model
In the last tutorial we set up and trained a model for our chatbot. Now preproccesing our data and training the model took a little bit of time, time that we don’t want to wait each time we want to use the model. So the first step of this tutorial is going to be changing some aspects of our code to load our model and data if it has already been created. Keep in mind that after doing this if you want to make changes to the model you will have to delete the saved model files or rename them.With these tweaks we will only retrain the model and recreate our data if we haven’t done so already.

Making Predictions
Now its time to actually use the model! Ideally we want to generate a response to any sentence the user types in. To do this we need to remember that our model does not take string input, it takes a bag of words. We also need to realize that our model does not spit out sentences, it generates a list of probabilities for all of our classes. This makes the process to generate a response look like the following:
– Get some input from the user
– Convert it to a bag of words
– Get a prediction from the model
– Find the most probable class
– Pick a response from that class

The bag_of_words function will transform our string input to a bag of words using our created words list. The chat function will handle getting a prediction from the model and grabbing an appropriate response from our JSON file of responses.

Now run the program and enjoy chatting with your bot!
