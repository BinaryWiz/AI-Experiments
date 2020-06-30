# Product Matching Neural Network

## Notes

### Fasttext
* I have just been experimenting with the FastText word embedding matrix
   * I got the largest one they had (600 billion tokens) and it works with n-grams so even if a word is not explicitly in the word embedding, it will stil find a similar word to it and get a word embedding based on that.

### My Network
* As a prototype for this network, I think its is going to be fairly simply
   * It is going to be an embedding matrix using the FastText model, then I will have two of the same networks (LSTM) for each title, making a siamese network, and then it will go to a dense layer (or 2) and end at a softmax, which will make the prediction of whether the two titles are actually the same.
   * Model: Embedding (FastText) -> LSTM * 2 -> LSTM * 2 -> Dense -> Dense -> Softmax

### Dataset
* For the training data, I am going to use the WDC Gold Standard database of products (http://webdatacommons.org/largescaleproductcorpus/v2/index.html)

* After further looking at the data, it seems like each product in the dataset as a cluser_id.
   * Essentially, this means that we can just use the cluster_id to build the positive examples of matches and use random examples outside of the cluster to build our negative training examples

* Update 6/29/2020: The way the dataset works is that for each entry in it, there is a title_right and a title_left. These are the two titles represented in a pair. There is a label that tells you whether the titles represent the same product or not. Using this, we already have built a dataset of positive and negative example pairs.
   * I also have created a seperate CSV file that is a simpler version of teh original dataset. It ony containes the titles with a label (either 0 or 1)

   * I need to figure out a way to have the embedding matrix not be part of the model itself, but still use it.

* The WDC Product Data researchers also did their own experiments, and they actually have a model that they trained using their own custom fasttext encoding model
   * They got about 90% accuracy on their training set which included computers, cameras, watches and shoes
      * They used a regular vanilla RNN which I find odd because an LSTM would surely capture the relatability between the tokens much better than a standard LSTM
   * I find this odd because computers and cameras do not make up a lot of the training set
      * There are 26 million offers, with office products making up about 13.13% of the dataset, so surely they could have used some of those
      * If the issue were the correlation between the different product categories (electronics related to book related to health related to toys etc.), then why would they pair computers and cameras with watches and shoes?
