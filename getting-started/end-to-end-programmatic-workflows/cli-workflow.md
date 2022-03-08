# CLI workflow

Building a machine learning model requires multiple processes. Those steps are slightly different depending on which task you want to accomplish. However, in this document, we will abstract them into the following three steps.

* [Experiment](../../user-guide/experiment/): Build a baseline machine learning model
* [Sweep](../../user-guide/sweep/): Optimize hyperparameters
* [Model registry](../../user-guide/model-registry/): Update the best model

The tutorial below is the process of creating a model for image classification with the MNIST dataset using the [VESSL Client CLI](../../api-reference/what-is-the-vessl-cli-sdk.md). Here all CLI commands are one-liners, but you can also select multiple options using the prompter for practical usage.

### Requirements

{% hint style="info" %}
If you haven't created an **organization** or a **project** on VESSL, please go [end-to-end programmatic workflows](./) and follow the instructions.
{% endhint %}

* [Organization](../../user-guide/organization/)
* [Project](../../user-guide/project/)
* [VESSL Client](../../api-reference/what-is-the-vessl-cli-sdk.md) (>= 0.1.34)

{% hint style="warning" %}
Don't forget to replace all **uppercase letters** below with your object names.
{% endhint %}

### Experiment: Build a baseline model

#### 1. Configure VESSL Client with the organization name and the project name

The first thing you need to do is to execute [`vessl configure`](../../api-reference/cli/getting-started.md#setup-a-vessl-environment) which will configure the client **** with the default **organization** and **project** we have created earlier. When a configuration is completed, there is no need to provide project or organization options to run commands.

{% tabs %}
{% tab title="one-liner" %}
```bash
vessl configure  \
    --organization "YOUR_ORGANIZATION_NAME"  \
    --project "YOUR_PROJECT_NAME"
```
{% endtab %}

{% tab title="prompter" %}
```bash
vessl configure

Please grant CLI access from the URL below.
https://vessl.ai/cli/grant-access?token=o0dyb21eu8fw

Waiting...

[?] Default organization: YOUR_ORGANIZATION_NAME
 > YOUR_ORGANIZATION_NAME

[?] Default project: YOUR_PROJECT_NAME
 > YOUR_PROJECT_NAME
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
You could view the current configuration with [`vessl list`](../../api-reference/cli/getting-started.md#view-the-current-configuration). You can change a default organization or project with [`vessl configure organization`](../../api-reference/cli/getting-started.md#change-the-default-organization) and [`vessl configure project`](../../api-reference/cli/getting-started.md#change-the-default-project) correspondingly.
{% endhint %}

#### 2. Create a dataset

To create a [dataset](../../user-guide/dataset/) on VESSL, run [`vessl dataset create`](../../api-reference/cli/vessl-dataset.md#create-a-dataset). Let's create a VESSL dataset from the public S3 dataset. Here is the public bucket URL that VESSL provides.

* Public MNIST dataset path: `s3://savvihub-public-apne2/mnist`

{% tabs %}
{% tab title="one-liner" %}
```bash
vessl dataset create "YOUR_DATASET_NAME" \
  --is-public -e "s3://savvihub-public-apne2/mnist"
```
{% endtab %}

{% tab title="prompter" %}
```bash
vessl dataset create --is-public -e "s3://savvihub-public-apne2/mnist"

Organization: YOUR_ORGANIZATION_NAME
Dataset name: YOUR_DATASET_NAME
```
{% endtab %}
{% endtabs %}

#### 3. Create a machine learning experiment&#x20;

You can use [`vessl experiment create`](../../api-reference/cli/vessl-experiment.md#create-an-experiment) to create a machine learning [experiment](../../user-guide/experiment/). Let's run an experiment by selecting one of the [clusters](../../user-guide/organization/organization-settings/configure-clusters.md) connected to the organization and deciding how many [resources](../../user-guide/organization/organization-settings/billing-information.md) to use. For this experiment, we will use the `aws-apne2-prod1` cluster managed by VESSL, and `v1.cpu-4.mem-13` that allocates 4 cores of CPU and 13GB of memory. Next, specify the [image URL](https://gallery.ecr.aws/vessl/kernels) and [start command](https://github.com/vessl-ai/examples/tree/main/mnist) to be used in the experiment container, and mount the dataset you made earlier. For more information on dataset mounting, please visit the [volume mount](../../user-guide/commons/volume-mount.md) page.

* GitHub repository of VESSL examples: [vessl-ai/examples](https://github.com/vessl-ai/examples)

{% tabs %}
{% tab title="one-liner" %}
```bash
vessl experiment create \
  -c "aws-apne2-prod1" \
  -r "v1.cpu-4.mem-13" \
  -i "public.ecr.aws/vessl/kernels:py36.full-cpu" \
  --dataset "/input:YOUR_DATASET_NAME"\
  -x "git clone https://github.com/vessl-ai/examples.git && pip install -r examples/mnist/keras/requirements.txt && python examples/mnist/keras/main.py --save-model --save-image"
```
{% endtab %}

{% tab title="prompter" %}
```
vessl experiment create --dataset /input:YOUR_DATASET_NAME

Organization: YOUR_ORGANIZATION_NAME
Project: YOUR_PROJECT_NAME
[?] Cluster: aws-apne2-prod1
 > aws-apne2-prod1

[?] Resource: v1.cpu-4.mem-13
   v1.cpu-0.mem-1
   v1.cpu-2.mem-6
   v1.cpu-2.mem-6.spot
 > v1.cpu-4.mem-13
   v1.cpu-4.mem-13.spot
   v1.t4-1.mem-13
   v1.t4-1.mem-13.spot
   v1.t4-1.mem-54
   v1.t4-1.mem-54.spot
   v1.t4-4.mem-163
   v1.t4-4.mem-163.spot
   v1.k80-1.mem-52
   v1.k80-1.mem-52.spot

[?] Image URL: public.ecr.aws/vessl/kernels:py36.full-cpu
 > public.ecr.aws/vessl/kernels:py36.full-cpu
   public.ecr.aws/vessl/kernels:py37.full-cpu
   public.ecr.aws/vessl/kernels:py36.full-cpu.jupyter
   public.ecr.aws/vessl/kernels:py37.full-cpu.jupyter
   tensorflow/tensorflow:1.14.0-py3
   tensorflow/tensorflow:1.15.5-py3
   tensorflow/tensorflow:2.0.4-py3
   tensorflow/tensorflow:2.2.1-py3
   tensorflow/tensorflow:2.3.2
   tensorflow/tensorflow:2.4.1
   tensorflow/tensorflow:2.3.0

Start command: git clone https://github.com/vessl-ai/examples.git && pip install -r examples/mnist/keras/requirements.txt && python examples/mnist/keras/main.py --save-model --save-image
```
{% endtab %}
{% endtabs %}

Noted that you can mount a GitHub **repository** to [project](../../user-guide/project/) so that you don't have to add a `git clone` command in every experiment. Likewise, **datasets** can be registered in the project in advance, and the dataset will be automatically mounted without having to give the `dataset_mounts` option when creating an experiment. For more information about those features, please refer to the [project repository & project dataset](../../user-guide/project/project-repository-and-project-dataset.md) page.

#### 4. View experiment results

For the image classification task, the experiment may take some minutes to finish. After confirming that the experiment you made has been completed on VESSL Web Console, the result can be viewed using [`vessl experiment read`](../../api-reference/cli/vessl-experiment.md#view-information-on-the-experiment).&#x20;

{% tabs %}
{% tab title="one-liner" %}
```bash
vessl experiment read "YOUR_EXPERIMENT_NAME"
```
{% endtab %}

{% tab title="prompter" %}
```
vessl experiment read 

Organization: YOUR_ORGANIZATION_NAME
Project: YOUR_PROJECT_NAME
[?] Experiment: 1-quasar-bat #1
 > 1-quasar-bat #1
```
{% endtab %}
{% endtabs %}

If you can't find your experiment name, then [`vessl experiment list`](../../api-reference/cli/vessl-experiment.md#list-all-experiments) will show all experiments in the default project.

#### 5. Create a model

In VESSL, you can create a [model from the outputs of the experiment](../../user-guide/model-registry/creating-a-model.md#creating-a-model-from-experiment). Before creating a model, you need to create a model repository. To create one run `vessl model-repository create` with the repository name.

{% tabs %}
{% tab title="one-liner" %}
```bash
vessl model-repository create "YOUR_MODEL_REPOSITORY_NAME"
```
{% endtab %}

{% tab title="prompter" %}
```
vessl model-repository create

Organization: YOUR_ORGANIZATION_NAME
Model repository name: YOUR_MODEL_REPOSITORY_NAME
```
{% endtab %}
{% endtabs %}

Then, run [`vessl model create`](../../api-reference/cli/vessl-model.md#create-a-model)with few options including the model repository name that you have just made.&#x20;

{% tabs %}
{% tab title="one-liner" %}
```bash
vessl model create "YOUR_MODEL_REPOSITORY_NAME" \
  --model-name "v0.0.1" \
  --source "experiment" \
  --experiment-id "YOUR_EXPERIMENT_ID" \ 
  --paths ["/"]
```
{% endtab %}

{% tab title="prompter" %}
```bash
vessl model create --model-name "v0.0.1"

Organization: YOUR_ORGANIZATION_NAME
Project: YOUR_PROJECT_NAME
[?] Model repository: YOUR_MODEL_REPOSITORY_NAME
 > YOUR_MODEL_REPOSITORY_NAME

[?] Source: From an experiment
 > From an experiment
   From local files

[?] Experiment: 1-quasar-bat #1
 > 1-quasar-bat #1

[?] Paths (Press -> to select and <- to unselect):
   X my_model 0 B
   X my_model/keras_metadata.pb 7.7 KB
   X my_model/saved_model.pb 88.8 KB
   X my_model/variables 0 B
   X my_model/variables/variables.data-00000-of-00001 1.2 MB
 > X my_model/variables/variables.index 1.4 KB
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you can't find your model repository name, run [`vessl model-repository list`](../../api-reference/cli/vessl-model.md#list-all-model-repositories) or if you can't find your experiment id, run [`vessl experiment list`](../../api-reference/cli/vessl-experiment.md#list-all-experiments).
{% endhint %}

### Sweep: Optimize hyperparameters

So far, we have run one machine learning [experiment](../../user-guide/experiment/) and made the results a [model](../../user-guide/model-registry/). Next, we will use the [sweep](../../user-guide/sweep/) to find the optimal hyperparameter value.

First, configure three sweep objective options.

* `-T` : objective type **** \[maximize|minimize]
* `-G` : target metric name
* `-M` : target value&#x20;

{% hint style="warning" %}
The target metric must be a value logged using [`vessl.log()`](../../api-reference/python-sdk/vessl.log/).
{% endhint %}

Next, we should specify the following common parameters.

* `--num-experiments` : the total number of experiments &#x20;
* `--num-parallel` : the number of experiments that run in parallel
* `--num-failed` : the number of experiments that could be failed

Next, define the search space of parameters with `-p`. As shown below, the `optimizer` is a **categorical** type and the option values are listed as an **array**. On the other hand, `batch_size` is an **int** value and the search **space** is set using **max**, **min**, and **step**. For more information on sweep see [creating a sweep](../../user-guide/sweep/creating-a-sweep.md).

{% hint style="warning" %}
You may find it easier to run [`vessl sweep create`](../../api-reference/cli/vessl-sweep.md#create-a-sweep) without any option but specify them through prompter.
{% endhint %}

{% tabs %}
{% tab title="one-liner" %}
```bash
vessl sweep create \
  -T "maximize" -G "0.99" -M "val_accuracy" \
  --num-experiments 4 --num-parallel 2 --num-failed 2 \
  -a random \
  -p "optimizer categorical list adam sgd adadelta" \
  -p "batch_size int space 64 256 8" \
  -c "aws-apne2-prod1" \
  -r "v1.cpu-4.mem-13" \
  -i "public.ecr.aws/vessl/kernels:py36.full-cpu" \
  --dataset "/input:YOUR_DATASET_NAME" \
  -x "git clone https://github.com/vessl-ai/examples.git && pip install -r examples/mnist/keras/requirements.txt && python examples/mnist/keras/main.py --save-model --save-image"
```
{% endtab %}

{% tab title="prompter" %}
```
vessl sweep create --dataset "/input:YOUR_DATASET_NAME"

Organization: YOUR_ORGANIZATION_NAME
Project: YOUR_PROJECT_NAME
[?] Objective type: maximize
 > maximize
   minimize

Objective metric: val_accuracy
Objective goal: 0.99
Maximum number of experiments: 4
Number of experiments to be run in parallel: 2
Maximum number of experiments to allow to fail: 2
[?] Sweep algorithm: random
   grid
 > random
   bayesian

Parameter #1 name: optimizer
[?] Parameter #1 type: categorical
 > categorical
   int
   double

[?] Parameter #1 range type: list
   space
 > list

Parameter #1 values (space separated): adam sgd adadelta
Add another parameter (y/n): y
Parameter #2 name: batch_size
[?] Parameter #2 type: int
   categorical
 > int
   double

[?] Parameter #2 range type: space
 > space
   list

Parameter #2 values ([min] [max] [step]): 64 256 8
Add another parameter (y/n): n
[?] Cluster: aws-apne2-prod1
 > aws-apne2-prod1

[?] Resource: v1.cpu-4.mem-13
   v1.cpu-0.mem-1
   v1.cpu-2.mem-6
   v1.cpu-2.mem-6.spot
 > v1.cpu-4.mem-13
   v1.cpu-4.mem-13.spot
   v1.t4-1.mem-13
   v1.t4-1.mem-13.spot
   v1.t4-1.mem-54
   v1.t4-1.mem-54.spot
   v1.t4-4.mem-163
   v1.t4-4.mem-163.spot
   v1.k80-1.mem-52
   v1.k80-1.mem-52.spot

[?] Image URL: public.ecr.aws/vessl/kernels:py36.full-cpu
 > public.ecr.aws/vessl/kernels:py36.full-cpu
   public.ecr.aws/vessl/kernels:py37.full-cpu
   public.ecr.aws/vessl/kernels:py36.full-cpu.jupyter
   public.ecr.aws/vessl/kernels:py37.full-cpu.jupyter
   tensorflow/tensorflow:1.14.0-py3
   tensorflow/tensorflow:1.15.5-py3
   tensorflow/tensorflow:2.0.4-py3
   tensorflow/tensorflow:2.2.1-py3
   tensorflow/tensorflow:2.3.2
   tensorflow/tensorflow:2.4.1
   tensorflow/tensorflow:2.3.0

Start command: git clone https://github.com/vessl-ai/examples.git && pip install -r examples/mnist/keras/requirements.txt && python examples/mnist/keras/main.py --save-model --save-image
```
{% endtab %}
{% endtabs %}

### Model Registry: Update the best model

Now that we have run several experiments using [sweep](../../user-guide/sweep/), let's find the **best** **experiment** using [`vessl sweep best-experiment`](../../api-reference/cli/vessl-sweep.md#find-the-best-sweep-experiment) which returns the experiment information that recorded the **best** **value** among the metric values set. In this example, since we have set to find the **maximum** value, the experiment with the **highest** **validation** **accuracy** will return.

{% tabs %}
{% tab title="one-liner" %}
```bash
vessl sweep best-experiment "YOUR_SWEEP_NAME"
```
{% endtab %}

{% tab title="prompter" %}
```
vessl sweep best-experiment

Organization: YOUR_ORGANIZATION_NAME
Project: YOUR_PROJECT_NAME
[?] Sweep: YOUR_SWEEP_NAME
 > YOUR_SWEEP_NAME
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
You can find the experiment id with [`vessl experiment read`](../../api-reference/cli/vessl-experiment.md#view-information-on-the-experiment).
{% endhint %}

Let's create a `v0.0.2` model with [`vessl model create`](../../api-reference/cli/vessl-model.md#create-a-model) from the output of best sweep experiment.

{% tabs %}
{% tab title="one-liner" %}
```bash
vessl model create "YOUR_MODEL_REPOSITORY_NAME" \
  --model-name "v0.0.2" \
  --source "experiment" \
  --experiment-id 8589948240 \
  --paths ["/"]
```
{% endtab %}

{% tab title="prompter" %}
```bash
vessl model create --model-name "v0.0.2"

Organization: YOUR_ORGANIZATION_NAME
Project: YOUR_PROJECT_NAME
[?] Model repository: YOUR_MODEL_REPOSITORY_NAME
 > YOUR_MODEL_REPOSITORY_NAME

[?] Source: From an experiment
 > From an experiment
   From local files

[?] Experiment: 1-quasar-bat #1
 > 1-quasar-bat #1

[?] Paths (Press -> to select and <- to unselect):
   X my_model 0 B
   X my_model/keras_metadata.pb 7.7 KB
   X my_model/saved_model.pb 88.8 KB
   X my_model/variables 0 B
   X my_model/variables/variables.data-00000-of-00001 1.2 MB
 > X my_model/variables/variables.index 1.4 KB
```
{% endtab %}
{% endtabs %}

If you want to view the performance of your model, you can check the latest metric value using `vessl model read`.

{% tabs %}
{% tab title="one-liner" %}
```bash
vessl model read "YOUR_MODEL_REPOSITORY_NAME" "YOUR_MODEL_NUMBER"
```
{% endtab %}

{% tab title="prompter" %}
```
vessl model read

Organization: YOUR_ORGANIZATION_NAME
[?] Model repository: YOUR_MODEL_REPOSITORY_NAME
 > YOUR_MODEL_REPOSITORY_NAME

[?] Model: 1
 > 1
   2
```
{% endtab %}
{% endtabs %}

Congratulation! We have looked at the overall workflow of using the **VESSL Client CLI**. The same process as this can be done with the [VESSL Client SDK](sdk-workflow.md) or through the [VESSL Web Console](../quickstart.md). Now, solve challenging machine learning tasks out there with your own code and dataset with VESSL.
