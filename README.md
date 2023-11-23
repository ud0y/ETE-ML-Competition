# ETE-ML-Competition
Mainly this was a classification problem but the provided dataset was very diverse. Given a book summary, we have to classify the genre of the book. I have mainly fine-tuned `csebuetnlp/banglabert` for classification.

# Data Preprocessing
After performing exploratory data analysis I have found that at max we have 10192 words in a sentence and on average 733 words in a sentence. In my preprocessing step, I have removed **hashtags**, **digits** (both Bangla and English), occurrences of **ZWNJ** or **ZWJ**, all types of **punctuations**, **emojis**. Also, I have **normalized** using `bnunicodenormalizer` and `unicodedata` library. I have replace 'ঃ' with a space as this character concated many words. With this, I have also **lowercased** all the English words. Then I removed stopwords (I have collected them from `bltk` and `nltk` library) from both Bangla and English text. I have also removed 10 most frequent words from the corpus. After all this steps 542 words on average in the dataset.

# Fine-tuning process
I have used HuggingFace `Trainer` API to finetune `csebuetnlp/banglabert` in google colab. 10% of the training set is used for validation and 90% for fine-tuning. The selected value for parameter is listed below,
- `learning_rate` = 6e-5
- `weight_decay`= 5e-7
- `num_train_epochs` = 5
- `evaluation_strategy` = 'epoch'
- `optim` = 'adafactor'
I have saved the best model on the lowest validation loss and the model can be found at HuggingFace using `Udoy/test-trainer-withoutMF-0-2` as the checkpoint.

# Inference
As I have saved my fine-tuned model in HuggingFace Hub it is easily accessible and using this I have predictions for the provided test set.

By following this process, I have received public score of 0.87607 and private score of 0.83187. 
