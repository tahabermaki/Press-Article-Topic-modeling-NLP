The focus lies on (topic-specific) collection building, a field that is becoming increasingly interesting with better article separation. Very specific research problems are addressed, such as building up collections with ambiguous keywords or working with certain genres. In order to best meet the needs of digital humanities scholars, NLP methods are adapted in new ways, the output is human-readable and the processed newspaper articles can be exported in the form of the original file. In addition, the notebooks allow the users to control the single steps and to choose what is best for their collection. While the NewsEye demonstrator offers the possibility to create datasets quickly and effectively, these notebooks offer possibilities to work on these collections according to specific questions.

# Topic-modeling-of-press-article
Topic modeling is a method of unsupervised classification of such documents, similar to clustering on numerical data, which finds natural groups of items even when we are not sure what we are looking for. In this project, we are going to extract the percentage of themes in each article that we have in the dataset.

Data preparation steps:
1. Tokenization: transforming a text into a series of individual tokens
2. Delete Stopwords: Creation of a personalized list of stopwords compatible with our data which can be further improved by adding words that do not interest us.
3. Lemmatization: giving words the canonical neutral form they have.
4. Creation of Bigram and Trigram Models: from our list of cleaned tokens, create bigrams and trigrams (pairs of words, which can carry meaning and which are therefore useful for the extraction topic).
5. Remove articles that are too short (Not important): To optimize the results of the model, we can avoid having articles with less than 30 tokens after cleaning.


# LDA Model:
LDA takes into account a corpus of documents, a number of k topics and produces topic probability distributions for each document.
It is important to note that when mentioning "topic 0" or "topic 1", these topics generally consist of probability distributions over several words that make up the topic.
For instance:
Topic 14 could consist of 40% "Class", 30% "child" and 20% "school"...
The Model Output would be:
• The distribution of words by subject.
• Breakdown of subjects by document.
*More information on the notebook*
Evaluation metric:
We use the consistency score in topic modeling to measure how interpretable topics are to humans. In this case, topics are represented by the first N words with the highest probability of belonging to that particular topic. In short, the consistency score measures how similar these words are to each other.


Number of topics:
We initialize our LDA model using Gensim and specify the desired Topics as 15.
This value can be improved thanks to the consistency value.
There is no single way to determine if the consistency score is good or bad. The score and its value depend on the data from which it is calculated. For example, in one case, the score of 0.5 may be sufficient but not acceptable in another case. The only rule is that we want to maximize this score.

Usually, the consistency score will increase with increasing number of subjects. This increase will decrease as the number of subjects increases. The compromise between the number of subjects and the consistency score can be achieved using the so-called elbow technique. The method consists of plotting the consistency score as a function of the number of subjects. We use the elbow of the curve to select the number of subjects.

Résultats : 
![image](https://user-images.githubusercontent.com/45733593/176407200-a144bdd4-9350-4f6c-b835-85380416860f.png)

 The consistency score we obtained for this model was:
 ![image](https://user-images.githubusercontent.com/45733593/176407245-2b6a88ed-d66e-45f0-bd9a-e364b00503f0.png)
As the figure indicates, we have succeeded in identifying Topics with an acceptable distance, i.e. there is no overlap between the topics.
(See notebook for interactive visualization)
For example Topic 9 represented by words like: city, town hall, work, municipality, municipal, union, public, land… can refer to the subject of the CITY.
Topic 5 and Topic 2 (the most interesting for the study) represented by words like: Price, customer, consumption, company, order, factory… refer to the subject of the COMPANY (ENTREPRISE in French)

The model returns a list of probability of belonging to a topic as follows:


![image](https://user-images.githubusercontent.com/45733593/176407147-b8625894-64d0-4eb1-a9e0-a4e3786bcc7b.png)

