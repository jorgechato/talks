<spam class="clear-image">
<img height="70px" src="2018/images/ucode-how-to-train-deep-learning-models-in-the-cloud/fh.png" alt=""></spam>
<spam class="RandM">floydhub</spam>

Notes:
Floydhub es el equivalente de heroku en AI.
Para los que no conozcais heroku, es una plataforma como servicio. Permite construir, ejecutar y operar aplicaciones en la nube.
Puedes desplegar las aplicaciones como si usases un vcs como git.

/---/

<spam class="clear-image">![](2018/images/ucode-how-to-train-deep-learning-models-in-the-cloud/fast-style.png)</spam>

/---/

```bash
$ tree -d
.
├── examples
│   ├── content
│   ├── results
│   ├── style
│   └── thumbs
├── images
└── src
```

/---/

```bash
$ pip3 install floyd-cli
```

Notes:
Llegados a este punto, todos deberíais tener instalado python 3.X y pip3.

/---/

```bash
$ floyd login

Authentication token page will now open in your browser. Continue? [Y/n]: y
Please copy and paste the authentication token.
This is an invisible field. Paste token and press ENTER:
Login Successful as jorgechato
```

/---/

```bash
$ floyd init fast-style-transfer

Project name does not yet exist on floydhub.com. Create your new project on floydhub.com:
	https://www.floydhub.com/projects/create
Press ENTER to use project name "fast-style-transfer" or enter a different name:
Project "fast-style-transfer" initialized in current directory
```

/---/

```bash
$ floyd run --gpu --env tensorflow-0.12:py2 --data narenst/datasets/coco-train-2014/1:images --data narenst/datasets/neural-style-transfer-pre-trained-models/1:models --data floydhub/datasets/imagenet-vgg-verydeep-19/3:vgg "python style.py --vgg-path /vgg/imagenet-vgg-verydeep-19.mat --train-path /images/train2014 --style examples/style/brown.jpg --base-model-path /models/commic-1.ckpt --epoch 1 --total-iterations 10 --checkpoint-dir /output"

Creating project run. Total upload size: 11.7MiB
Syncing code ...
[================================] 12278606/12278606 - 00:00:08
Error: You do not have enough credits to run this job. Please buy a powerup to continue running jobs
```

Notes:
--data montamos una unidad que ya está en los servidores de floydhub para que sea accesible en nuestro proyecto.

vgg = visual geametry group

Si el modelo requiere poco poder de computación, floydhub es la opción más rápida.
En cambio, si ese modelo (como hemos visto en el ejemplo) requiere más poder de procesamiento, Google cloud es la mejor opción.