---
title: "[MachineLearning] How to build a spam classifier"
date: 2021-10-09T18:44:20+02:00
draft: false
---

Detecting Spam messages is one of the first tasks assigned to Machine Learning algorithms, and Bayesian classifiers are the perfect choice for this job. Let’s see more about Machine Learning spam detection with a little bit of theory and fully functional implementation in Python.

Bayes’ theorem is a cornerstone of statistics, it correlates the conditional probability (prior probability) of an event to the probability measure (posterior probabilities) of the same event. By applying this concept to our spam detection problem, the Bayesian classifier allows us to determine whether a message is a spam or not by evaluating all the words that compose it and associating them with a probability. But now talk about coding: let’s see together how to transform these concepts into a Machine Learning algorithm.

As always for Machine Learning coding, the first thing to get is the dataset. For these tests, we can use the 2007 TREC Spam Corpus dataset. Read the agreement and download “trec07” [dataset from here](https://plg.uwaterloo.ca/~gvcormac/treccorpus07/).

Now all these (labeled) emails must be loaded into an object that Python can handle. These data must also be split into two groups: the train-set and the test-set for results validation.

```python
def _loadDataset(self):
        # Labels to dictionary
        labels_dictionary = {}
        with open(self.labels_path) as label_file:
            for line in label_file:
                    label_id = re.findall(r'\d+', line)[0]

                    if "spam" in line:
                        labels_dictionary[label_id] = False
                    else:
                        labels_dictionary[label_id] = True

        # Load Email + Label
        for label_id in labels_dictionary.keys():
            file_path = self.dataset_path + 'inmail.' + label_id
            mail_content = self._read_mail(file_path)

            self.mails.append(mail_content)
            self.labels.append(labels_dictionary[label_id])

    def _read_mail(self, mail_path):
        mail_content = ''

        with open(mail_path, encoding='utf-8', errors='replace') as mail_file:

            mail_message = email.message_from_file(mail_file)

            # Read subject
            if mail_message and mail_message['Subject']:
                mail_content += mail_message['Subject']
                mail_content += ' '

            # Read body
            if mail_message and mail_message['Subject']:
                mail_content += mail_message['Subject']
                mail_content += ' '
            
            mail_content += self._extract_body(mail_message)

        return mail_content

    def _extract_body(self, mail_message):
        body = ''
        for part in mail_message.walk():
            if part.get_content_type() == 'text/plain' or part.get_content_type() == 'text/html':
                body += str(part.get_payload())

        return body
```

We have the mails and labels loaded in two lists. Before creating a Bayesian model it is necessary to process this data. The process is called vectorization and involves the transformation of the content of the emails into an array of integers that evaluate the number of times a given word is present in the message. SKLearn has a tool that allows you to do this.

```python
# Vectorization
self.vectorizer = CountVectorizer()
mail_train_vector = self.vectorizer.fit_transform(mail_train)
mail_test_vector = self.vectorizer.transform(mail_test)
```

Now we have everything we need: we can train the model and evaluate the results.

```python
# Naive Bayes Classifier
self.classifier = MultinomialNB()
self.classifier.fit(mail_train_vector, labels_train)

# Save model
try:
    pickle.dump(self.classifier, open(weights_path, 'wb'))
    pickle.dump(self.vectorizer, open(weights_path + '.vec', 'wb'))
except Exception as exptn:
    print("WARNING: Isn't possible to save the model on disk!")


# Measurements
predictions = self.classifier.predict(mail_test_vector)
training_result = classification_report(labels_test, predictions, target_names=['SPAM', 'NOT SPAM'])
training_result += '\n' + 'Classification accuracy {:.1%}'.format(accuracy_score(labels_test, predictions))
return training_result
```

{{ < youtube M6OCiyBFW3U > }}

In this [GitHub repository](https://github.com/gslf/ML-SpamDetection) you will find a ready-to-use class and a CLI interface to train and classify all messages. To use the environment setup and start using the Spam Detector use these commands:

```python
> python3 -m venv venv 

## For Linux & MacOS
> source venv/bin/activate 
## For Windows
> venv\Scripts\activate

> pip3 install -r requirements.txt 

> python3 main.py 
```

