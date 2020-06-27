# Product Matching Neural Network

## Notes
* I have just been experimenting with the FastText word embedding matrix
   * I got the largest one they had (600 billion tokens) and it works with n-grams so even if a word is not explicitly in the word embedding, it will stil find a similar word to it and get a word embedding based on that.

* As a prototype for this network, I think its is going to be fairly simply
   * It is going to be an embedding matrix using the FastText model, then I will have two of the same networks (LSTM) for each title, making a siamese network, and then it will go to a dense layer (or 2) and end at a softmax, which will make the prediction of whether the two titles are actually the same.
   * Model: Embedding (FastText) -> LSTM * 2 -> LSTM * 2 -> Dense -> Dense -> Softmax

* For the training data, I am going to use the WDC Gold Standard database of products (http://webdatacommons.org/largescaleproductcorpus/v2/index.html)