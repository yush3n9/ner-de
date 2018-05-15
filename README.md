# ner-name
Optimized NER for german language with spaCy

## Setup Instructions:
* virtualenv venv -p /usr/bin/python3
* source venv/bin/activate
* pip install -r requirements.txt
* python -m spacy download de
* python -m rasa_nlu.train -c configs/spacy_regex_mb_nlu_model_config.json

## Training nlu model:
python -m rasa_nlu.train -c configs/spacy_regex_mb_nlu_model_config.json

## Cross validate of nlu model:
python -m rasa_nlu.evaluate -d data/nlu_traindata.json -c configs/spacy_regex_mb_nlu_model_config.json --mode crossvalidation
```
INFO:__main__:CV evaluation (n=10)
INFO:__main__:F1-score: 0.837 (0.052)
INFO:__main__:Precision: 0.914 (0.000)
INFO:__main__:Accuracy: 0.849 (0.044)
INFO:__main__:Finished evaluation
```

## Start nlu as server and test with curl
python -m rasa_nlu.server  -c configs/spacy_regex_mb_nlu_model_config.json
```
curl -XPOST localhost:5000/parse -d '{"q":"Ich bin Tanja Schmitt, geboren am 12.12.2000", "project":"ner-de", "model":"spacy_regex_mb"}'
```
