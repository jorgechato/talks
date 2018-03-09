
<spam class="RandM">
Advanced deep learning topics
</spam>

Notes:
2 partes: overfitting, export model

/---/

<spam class="RandM">
How to deal with overfitting ?
</spam>

/---/

<spam class="RandM">
Size of the network is a key thing
</spam>

Notes:
Mayor tamaño del modelo mas aprende
Red mas reducida menos aprende
Si el tamaño es muy grande puede mapear los datos como diccionario
Si se hace muy peqeño tiene el riesgo de caer en underfitting
No hay una formula magica, hay que empezar con pocos parametros y luego ir incrementando

/---/

<spam class="RandM">
Weight regularization
</spam>

Notes:
Es basicamente añadir una penalizacion en tiempo de entrenamiento para ayudar a regulizar las weights

/---/

```python

from keras import regularizers

model = models.Sequential()
model.add(layers.Dense(16, kernel_regularizer=regularizers.l2(0.001),
                       activation='relu', input_shape=(10000,)))
model.add(layers.Dense(16, kernel_regularizer=regularizers.l2(0.001),
                       activation='relu'))
model.add(layers.Dense(1, activation='sigmoid'))

```

/---/

<spam class="RandM">
Dropout
</spam>

Notes:
Es la tecnica mas efectiva para regulizaracion y prevencion de overfitting
Cuando aplicamos dropout a una layer lo que hacemos es desactivar aleatoriamente
un numero neuronas en el momento del entrenamiento, es decir la weight se pone 0


/---/

```python
model = models.Sequential()
model.add(layers.Dense(16, activation='relu', input_shape=(10000,)))
model.add(layers.Dropout(0.5))
model.add(layers.Dense(16, activation='relu'))
model.add(layers.Dropout(0.5))
model.add(layers.Dense(1, activation='sigmoid'))
```

/---/

<spam class="RandM">
To recap
</spam>

/---/

- <spam class="RandM"> Get more training data. </spam>
- <spam class="RandM"> Reduce the capacity of the network. </spam>
- <spam class="RandM"> Add weight regularization. </spam>
- <spam class="RandM"> Add dropout. </spam>

/---/

<spam class="RandM">
How can I port my current model to somewhere else??
</spam>

/---/

<spam class="RandM">
I need to have h5py
</spam>

/---/

```python
from keras.models import Sequential
from keras import models

model = Sequential()
...
# serialize model
model.save('my_model.h5')

# later...

# load model
model = models.load_model('my_model.hd5')

```
<spam class="RandM">
Option 1
</spam>

/---/

```python
from keras.models import model_from_json
from keras.models import Sequential

model = Sequential()
...

# serialize model to JSON
model_json = model.to_json()
with open("model.json", "w") as json_file:
    json_file.write(model_json)
# serialize weights to HDF5
model.save_weights("model.h5")
print("Saved model to disk")

# later...

# load json and create model
json_file = open('model.json', 'r')
loaded_model_json = json_file.read()
json_file.close()
loaded_model = model_from_json(loaded_model_json)
# load weights into new model
loaded_model.load_weights("model.h5")
print("Loaded model from disk")

```
<spam class="RandM">
Option 2
</spam>

/---/

<spam class="RandM">
I'm a brave person and I want to deploy my model into a iOS app
</spam>

/---/

<spam class="RandM">
What I need ?
</spam>

/---/

- <spam class="RandM"> A model created with keras </spam>
- <spam class="RandM"> XCode 9.0 and later </spam>
- <spam class="RandM"> coremltools pyhton library </spam>

/---/

```python
from coremltools.converters.keras import convert
from keras.models import Sequential

model = Sequential()
...
# In case the model accept a image as input will be more
# easier for iOS code declare in that way.
coreml_model = convert(model, image_input_names="input1")
coreml_model.save('my_model.mlmodel')


```
/---/

<div class="clear-image">
<img src="2018/images/ucode-being-smarter-than-AI/xcode.png" alt="">
</div>
