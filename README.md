# Train and Save Model on Iris data set using Keras
### Exported Model configured for Tensorflow Serving

There is a lack of simple documentation on to train a model for classification 
and save it using keras for Tensorflow Serving. Hopefully this example will lighten the way to productionize 
AI.


### Getting Environment Set Up
Clone Repo
```angular2html
git clone git clone https://github.com/brianalois/iris_keras_tensorflow_serving.git
cd iris_keras_tensorflow_serving
```

### PIPENV
#### Use Pipenv because we are awesome develoeprs
I am using pipenv in order to standardize environments, kind or like the famous NPM for node

###### Install Pipenv
https://docs.pipenv.org/
```angular2html
pip install pipenv
```
or if you are using mac install with homebrew
```angular2html
brew install pipenv
```

#### Install Dependencies
run this in the repo directory, installs files from Pipfile
```angular2html
pipenv install
```
#### Run it using pipenv
```angular2html
pipenv run python index.py
```
#### Sample REST calls

##### Predict
###### Request
```
curl -d '{"signature_name" :"predict-iris",  "instances": [[1.0,2.0,5.0,0.3],[0.1,0.2,0.3,0.4]]}'  -X POST http://localhost:8501/v1/models/myiris:predict
```

###### Response
```
{
    "predictions": [[0.257784516, 0.526633084, 0.215582326], [0.394048154, 0.392151684, 0.213800162]
    ]
}
```

##### Classify
###### Request
```
curl -d '{"signature_name" :"serving_default", "examples": [{"x":[1.0,2.0,5.0,0.3]}] }' -X POST http://localhost:8501/v1/models/myiris:classify
```

###### Response
```
{
    "results": [[["Iris-versicolor", 0.526633084], ["Iris-setosa", 0.257784516], ["Iris-virginica", 0.215582326]]
    ]
}
```

### No Pipenv
#### Don't want to use Pipenv because I am not awesome
If you do not want to use **pipenv** then you must install these dependencies
You must have tensorflow keras, and numpy installed(obviously)
```angular2html
pip install numpy
pip install tensorflow keras pandas sklearn
```
run the file to export the trained model
```angular2html
python index.py
```
#### Variables

There are 2 variables starting at line 18

**model_version**: change this to change the 
name of the folder of the specific model version
```angular2html
model_version = "1"
```
**epoch**: the higher this number is the more accurate the model, but the longer it will take to train. 5000 is good, but may take a while
```angular2html
epoch = 100
```

