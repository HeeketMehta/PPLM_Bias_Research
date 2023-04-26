# Bias & Toxicity Mitigation of GPT - 2 Generated Text Using Custom PPLM

This is a research project undertaken by me (Heeket Mehta), under the guidance of Jessica Echterhoff and Prof. Julian McAuley at the University of California, San Diego. <br />

The goal is to prevent GPT - 2 from generating highly biased and toxic sentences, given a very unbiased, harmless, non-toxic and regular prompt. <br />
GPT - 2 is trained on biased data, and thus the auto-generated text is incredibly biased, and this project aims at mitigating and eliminating the toxicity by stirring GPT - 2 such that it produces unbiased and non-toxic statements. <br />

To do the above, we develop a custom PyTorch based Deep Learning Classification Model, which we fit on top of the Plug and Play Language Models (PPLM) developed by Uber AI. <br /><br />

Concepts - Data Science, Machine Learning, Deep Learning, Natural Language Processing <br />
Programming Language - Python, JSON <br />
Frameworks/Architecture/Technology - Artificial Neural Networks, Transformers <br />
Libraries - PyTorch, Pandas, NumPy, Sci-kit Learn, Tensorflow <br />


## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

What things you need to install the software - 

```
python==3.7.0
torch==1.7.0
nltk==3.4.5
colorama==0.4.4
transformers==3.4.0
torchtext==0.3.1
sentence-transformer
```

## Data Pre-Processing

The original data is obtained from - https://www.kaggle.com/competitions/jigsaw-toxic-comment-classification-challenge/leaderboard

Original Data File - 
```
train.csv
```
<br />
This original dataset contains various comments & sentences that are labelled as "Social Bias", "Identity Hate", "Obscene", "Severe Toxic", etc.
We process this data and reduce these into a single target variable `Total Bias` by performing a XOR operation across the row. <br />

Furthermore, we perform sentence encoding of the comments using BERT transformer, to obtain a sentence embedding vector of (1024,) shape for each sentence, which serves as a feature, and `Total Bias` is the target variable. <br />

The data is further processed for class imbalance and on normalizing the data, we get total of ~33,000 data samples, of balanced classes. (1-Toxic, 0-Non-Toxic). <br />

Cleaned Data File - 
```
balanced_train.csv
```
<br />

## Custom Deep Learning Classification Model

Based on the above data, we develop a PyTorch based classification model, that takes in the sentence embedding as the features and `Total Bias` as target variable and classifies into 2 classes. <br />

#### Model Summary/Architecture -- (INSERT IMAGE)

#### Model Performance -- (INSERT IMAGE)


<br />
The model weights are saved in `BERT_large_full_pytorch_model.pth` and meta data is saved as a JSON file in `meta_json_file_BERT_Large.json`, to be fit into the PPLM model.


## Plug and Play Language Models

The above custom PyTorch deep learning model is integrated with the PPLM code i.e. The model weights and meta Json data is integrated with the PPLM code. The custom classifier is fit into the PPLM under the name `custom_discriminator`. <br />
The files we modify to facilitate integration of our custom deep learning model with GPT-2 generator in PPLM are - 

```
PPLM/run_pplm.py
PPLM/run_pplm_discrim_train.py
```

The file that mainly runs the PPLM Code is 
```
PPLM_DL_Classification_Main.ipynb
``` 
where the `run_pplm_example` is the main function to run and display result. <br />
Note - Hyperparamter tuning too was performed on the above model.

## RESULTS OF PPLM 

# ((INSERT RESULTS HERE ))


## Performance Improvement


# ((INSERT RESULTS HERE ))

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc
