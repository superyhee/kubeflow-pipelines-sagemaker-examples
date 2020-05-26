## Examples for using Amazon SageMaker components in Kubeflow Pipelines

![Demo_pipeline](pipeline.png)

### First component:
Runs an Amazon SageMaker hyperparameter tuning job to optimize the following hyperparameters:

* learning-rate: [0.0001, 0.1] log scale
* optimizer : [sgd, adam]
* batch-size: [32, 128, 256]
* model-type: [resnet, custom model]

**Input**: N/A <br>
**Output**: best hyperparameters

### Second component:
During hyperparameter search in the previous step, models are only trained for 10 epochs to determine well performing hyperparameters. In the current step the best hyperparameters are taken and the epochs are updated to 80 to give the best hyperparameters an opportunity to deliver higher accuracy in the next step.

**Input**: best hyperparameters <br>
**Output**: best hyperparameters with updated epochs (80)

### Third component:
Run an Amazon SageMaker training job using the best hyperparameters and for higher epochs.

**Input**: best hyperparameters with updated epochs (80) <br>
**Output**: training job name

### Fourth component:
Create an Amazon SageMaker model artifact

**Input**: training job name <br>
**Output**: model artifact name

### Fifth component:
Deploy a model with Amazon SageMaker deployment 

**Input**: model artifact name <br>
**Output**: N/A
