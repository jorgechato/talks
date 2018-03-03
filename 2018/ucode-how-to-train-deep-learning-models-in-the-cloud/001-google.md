<spam class="clear-image">
<img height="70px" src="2018/images/ucode-how-to-train-deep-learning-models-in-the-cloud/gc.png" alt=""></spam>
<spam class="RandM">google cloud</spam>

/---/

<spam class="clear-image">
<img width="500px" src="2018/images/ucode-how-to-train-deep-learning-models-in-the-cloud/access.png" alt=""></spam>
</spam>

/---/

<spam class="clear-image">![](2018/images/ucode-how-to-train-deep-learning-models-in-the-cloud/wellcome-google.png)</spam>

/---/

Set up your GCP project [here](https://cloud.google.com/ml-engine/docs/getting-started-training-prediction)

/---/

```
.
├── data
├── output
│   ├── census.hdf5
│   ├── export
│   │   └── saved_model.pb
│   └── logs
├── preprocess.py  # Run predictions
├── requirements.txt
├── setup.py  # pypi pkg
└── trainer
    ├── __init__.py  # Empty file (required)
    ├── model.py  # Implements the Keras model
    └── task.py  # Run the training of the model (HyperParam as flags)
```

/---/

<!-- <spam class="clear-image">
<img src="2018/images/ucode-how-to-train-deep-learning-models-in-the-cloud/training.png" alt=""></spam>
</spam> -->
Training

/---/

```bash
$ python -m trainer.task --train-files $TRAIN_DATA \
                       --eval-files $EVAL_DATA \
                       --train-steps $TRAIN_STEPS
                       --job-dir $MODEL_DIR
```

Notes:
Así es como ejecutaríamos nuestro modelo en local

/---/

```bash
$ gcloud ml-engine local train \
    --module-name trainer.task \
    --package-path trainer/ \
    --job-dir $MODEL_DIR \
    -- \
    --train-files $TRAIN_DATA \
    --eval-files $EVAL_DATA \
    --train-steps $TRAIN_STEPS
```

Notes:
job-dir se propaga a los flags del programa principal

/---/

```bash
$ gcloud ml-engine jobs submit training $JOB_NAME \
        --module-name $MAIN_APP_MODULE \
        --package-path trainer/ \
        --job-dir $JOB_DIR \
        --region europe-west1 \
        --config config.yaml \
        -- \
        --train-files $TRAIN_DATA \
        --eval-files $EVAL_DATA \
        --train-steps $TRAIN_STEPS
```

/---/

Predict

Notes:
La predicción se puede realizar en vuestra propia máquina (recomendado)

/---/

```bash
$ python preprocess.py sample.json
```

/---/

```bash
$ gcloud ml-engine local predict \
        --model-dir=$JOB_DIR/export \
        --json-instances sample.json
```

/---/

```bash
$ gcloud ml-engine jobs submit predict $JOB_NAME \
        --module-dir $JOB_DIR/export \
        --json-instances sample.json \
        --region europe-west1 \
        --config config.yaml
```