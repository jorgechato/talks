<spam class="RandM">Coding</spam>

<div class="clear-image">
<img width="60%" src="2018/images/ucode-being-smarter-than-AI/time.png" alt="">
</div>

Notes:
Vamos a ver unas Redes neuronales (que no las que os propongo en el reto), pero os ayudarán a entender como el algoritmo pasa a ser código.

/---/

<div class="clear-image">
<img src="2018/images/ucode-being-smarter-than-AI/autoencoder.png" alt="">
</div>
<spam class="RandM">Basic autoencoder</spam>

/---/

```python
from keras.layers import Input, Dense
from keras.models import Model

# this is the size of our encoded representations
encoding_dim = 32  # 32 floats -> compression of factor 24.5, assuming the input is 784 floats

model = Model()
# this is our input placeholder
model.add(Input(shape=(784,)))
# "encoded" is the encoded representation of the input
model.add(Dense(encoding_dim, activation='relu'))
# "decoded" is the lossy reconstruction of the input
model.add(Dense(784, activation='sigmoid'))
```

Notes:
Las capas que componen la red neuronal
Número de neuronas en esa capa
Funciones de activación

/---/

<div class="clear-image">
<img width="60%" src="2018/images/ucode-being-smarter-than-AI/lstm.png" alt="">
</div>
<spam class="RandM">
Small LSTM Recurrent Neural Network
</spam>

/---/

```python
from keras.models import Sequential
from keras.layers import Dense
from keras.layers import Dropout
from keras.layers import LSTM

model = Sequential()
# First layer with an extra layer which include our input
model.add(LSTM(256, input_shape=(X.shape[1], X.shape[2])))
model.add(Dropout(0.2))
model.add(Dense(y.shape[1], activation='softmax'))
model.compile(loss='categorical_crossentropy', optimizer='adam')
```

Notes:
Dropout activa o desactiva aleatoriamente neuronas para que a la hora de entrenar no aprenda a hacer un ejercicio sino todos.
El mejor equivalente es el aprender de memoria para un examen un ejercicio concreto, luego llegas al examen y ves que el ejercicio es ligeramente diferente.
Para evitar eso la mejor manera es desactivar algunas neuronas aleatoriamente para evitar el overfitting.

We can now define our LSTM model. Here we define a single hidden LSTM layer with 256 memory units. The network uses dropout with a probability of 20. The output layer is a Dense layer using the softmax activation function to output a probability prediction for each of the 47 characters between 0 and 1.

The problem is really a single character classification problem with 47 classes and as such is defined as optimizing the log loss (cross entropy), here using the ADAM optimization algorithm for speed.

/---/

<div class="clear-image">
<img src="2018/images/ucode-being-smarter-than-AI/linear.png" alt="">
</div>
<spam class="RandM">
Simple linear regression
</spam>

/---/

```python
from keras.models import Sequential
from keras.layers import Dense

model = Sequential()
model.add(Dense(
                1,
                activation='linear',
                input_shape=2,
                kernel_initializer='glorot_uniform'
                )
        )
## Compile our model using the method of least squares (mse) loss function 
## and a stochastic gradient descent (sgd) optimizer
model.compile(loss='mse', optimizer='sgd'
```