THE <b>MATH<spam class="RandM">ish</spam></b> OF THE ALGORITHM

/---/

GANs
<spam class="RandM">generative adversarial network</spam>

/---/

<div class="clear-image">
<img src="2018/images/ucode-being-smarter-than-AI/GANs.png" alt="">
</div>

/---/

```python
def build_generator(self):
    model = Sequential()
    //TODO: create generator network model
    return model

def build_discriminator(self):
    model = Sequential()
    //TODO: create discriminator network model
    return model
```

/---/

CNN + YOLO
<spam class="RandM">convolutional weights + you only look once</spam>

/---/

<div class="clear-image">
<img width="60%" src="2018/images/ucode-being-smarter-than-AI/cnn.jpg" alt="">
</div>

Notes:
Un único modelo pero con un número significativo de layers (capas)
Estas capas se componen de redes convulacionales y otras que os dejo a vosotros investigar

/---/

<div class="clear-image">
<img width="60%" src="2018/images/ucode-being-smarter-than-AI/lt.png" alt="">
</div>

Notes:
Ya tiene un amplio conocimiento para resolver un problema y este se aplica a resolver otro problema diferente pero que guarde una relación con el primero.
Ejemplo: modelo entrenado para clasificar caniches se puede reentrenar para que sea capaz de claseificar gatos.

/---/

<div class="clear-image">
<img src="2018/images/ucode-being-smarter-than-AI/tb.png" alt="">
</div>

Notes:
Prueba error con hyperparameter (hiperparámetros) que veremos a continuación.
Herramientas de visualización