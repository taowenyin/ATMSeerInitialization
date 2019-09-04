# ATM - Auto Tune Models（自动调整模型）

# Overview

自动调整模型（ATM）是一个以易用为主要目的的自动机器学习系统。简而言之，你给ATM一个分类任务和一个CSV文件的数据集，那么ATM就会试图构建它所能构建的模型中最佳的模型。ATM基于这篇[文章](https://dai.lids.mit.edu/wp-content/uploads/2018/02/atm_IEEE_BIgData-9-1.pdf)，并且该项目是MIT的[Human-Data Interaction (HDI) Project](https://hdi-dai.lids.mit.edu/)项目中的一部分。

# 开始

## 安装

### 需求

**ATM** 是基于[Python 2.7, 3.5, 以及 3.6](https://www.python.org/downloads/)进行开发和测试。

此外，虽然没有严格的要求，但还是强烈建议使用[virtualenv](https://virtualenv.pypa.io/en/latest/)，以避免其他软件干扰 **ATM** 的运行。

接下来在Python3.6环境下使用最少的代码来创建部署 **ATM** 的virtualenv环境：

```bash
pip install virtualenv
virtualenv -p $(which python3.6) atm-venv
```

接下来你需要执行，并载入virtualenv环境：

```bash
source atm-venv/bin/activate
```

记住每次启动一个新的 **ATM** 控制台都要执行它！

### 安装PIP

创建完virtualenv环境，并且载入环境后，我们建议使用[pip](https://pip.pypa.io/en/stable/)来安装 **ATM** ：

```bash
pip install atm
```

这条指令将会从[PyPi](https://pypi.org/)上拉取并安装最新的ATM。 

### 从源码进行安装


或者，在激活virtualenv后，你也可以从存储库的`stable`分支中克隆一份，并从源代码安装，方法是在源码上运行“make install”：

```bash
git clone git@github.com:HDI-Project/ATM.git
cd ATM
git checkout stable
make install
```

### 为开发安装

如果您想为项目做出贡献，那么还需要一些步骤来为项目的开发做准备。

首先，请前往[项目的Github页面](https://github.com/hdi-project/atm)，点击页面右上角的 **fork** 按钮，在您自己的用户名下创建项目的fork。

然后，克隆你的fork，并从master创建一个以你将要处理的问题的编号为名称的分支：

```bash
git clone git@github.com:{your username}/ATM.git
cd ATM
git branch issue-xx-cool-new-feature master
git checkout issue-xx-cool-new-feature
```

最后，使用下面的命令来安装项目，这些安装是一些额外的依赖项，用于代码的整理和测试。

```bash
make install-develop
```

在开发期间要定期使用命令“make lint”和“make test”。

## 数据格式

ATM的输入为CSV文件，具有一下特性：

* 使用单个逗号，`,`，最为分隔符。
* 它的第一行是包含列名称的标题。
* 有一列包含需要预测的目标变量。
* 其余的列都是用于预测目标列的变量或特性。
* 每一行对应一个完整的训练样本。

以下是一个CSV文件的前5行，其中包含了4个特征和一个名为“class”的目标列，例如：

```
feature_01,feature_02,feature_03,feature_04,class
5.1,3.5,1.4,0.2,Iris-setosa
4.9,3.0,1.4,0.2,Iris-setosa
4.7,3.2,1.3,0.2,Iris-setosa
4.6,3.1,1.5,0.2,Iris-setosa
```

这个CSV文件可以使用本地文件的方式传递给ATM，也可以使用AWS S3 Bucket或者符合规范的URL。

你能在[atm-data S3 Bucket in AWS](https://atm-data.s3.amazonaws.com/index.html)中找到Demo所使用的数据集。


## 快速开始

在这个简短的教程中，我们将会引导你完成一系列的步骤，从而帮助你探究 **ATM** 中的一些Python API。

### 1. 获取一个Demo数据

运行 **ATM** 的第一步是获取将在本教程其余部分中所使用的Demo数据集。

本Demo所使用的数据集是pollution.csv，你可以通过浏览器[在这里](https://atm-data.s3.amazonaws.com/pollution_1.csv)下载该数据集，或者使用如下的指令：

```bash
atm download_demo pollution_1.csv
```

### 2. 创建一个ATM对象

在获取Demo数据集后就需要创建一个ATM对象。

```python
from atm import ATM

atm = ATM()
```

默认情况下，假如ATM对象没有任何参数，那么它将在当前的工作目录下创建一个名叫 `atm.db` 的SQLite数据库.

假如你要链接到其他数据库或者改变SQLite数据库的位置，那么就需要参考[API Reference](https://hdi-project.github.io/ATM/api/atm.core.html)中有效的参数列表。

### 3. 搜索最佳模型

一旦你有了 **ATM** 对象, 你就可以使用 `atm.run` 方法来启动在CSV文件中的目标列的最佳预测模型搜索。

这个函数能够接收本地的CSV文件路径，也可以接收一个HTTP的URL或者AWS S3的资源。

例如，我已经下载了数据集[pollution_1.csv](https://atm-data.s3.amazonaws.com/pollution_1.csv)到当前工作目录，那么我们就可以调用 `run` 像如下这样:

```python
results = atm.run(train_path='pollution_1.csv')
```

或者，我们可以使用ATM数据集的HTTPS的URL：

```python
results = atm.run(train_path='https://atm-data.s3.amazonaws.com/pollution_1.csv')
```

最后一种，假如我们的数据集在S3 Bucket，那么我们可以通过这个URL格式 `s3://{bucket}/{key}` 来下载该文件：

```python
results = atm.run(train_path='s3://atm-data/pollution_1.csv')
```

为了能够在私有的S3 Bucket上下载数据集，就需要进行[AWS认证文件](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/setup-credentials.html)的配置，或者在创建 `ATM` 对象时传递 `access_key` 和 `secret_key` 参数.

这个 `run` 函数将会运行 `Datarun` ，并且进度条将会显示对不同模型的测试和调整。

```python
Processing dataset demos/pollution_1.csv
100%|##########################| 100/100 [00:10<00:00,  6.09it/s]
```

一旦 `Datarun` 运行完成，那么就会有消息打印出来。我们也可以探索这个 `results` 对象.

### 4. 了解results对象

Onc一旦Datarun运行完毕，我们就可以通过多种方式探索 `results` 对象:

**a. 得到Datarun的结果**

 `describe` 方法将会返回Datarun运行后的结果：

```python
results.describe()
```

它将会打印一个简单的描述，类似于下面的内容：

```python
Datarun 1 summary:
    Dataset: 'demos/pollution_1.csv'
    Column Name: 'class'
    Judgment Metric: 'f1'
    Classifiers Tested: 100
    Elapsed Time: 0:00:07.638668
```

**b. 得到最佳分类的结果**

 `get_best_classifier` 方法将会打印在Datarun中找到的关于最佳分类的信息，这个信息包括所使用的方法和最佳的超参：

```python
results.get_best_classifier()
```

将会输出类似于下面的内容：

```python
Classifier id: 94
Classifier type: knn
Params chosen:
    n_neighbors: 13
    leaf_size: 38
    weights: uniform
    algorithm: kd_tree
    metric: manhattan
    _scale: True
Cross Validation Score: 0.858 +- 0.096
Test Score: 0.714
```

**c. 了解分数**

 `get_scores` 方法将会返回一个包含所有分类测试信息的 `pandas.DataFrame`对象，这个对象包含交叉验证分数和所选用的模型。

```python
scores = results.get_scores()
```

scores有类似于下面的内容：

```python
  cv_judgment_metric cv_judgment_metric_stdev  id test_judgment_metric  rank
0       0.8584126984             0.0960095737  94         0.7142857143   1.0
1       0.8222222222             0.0623609564  12         0.6250000000   2.0
2       0.8147619048             0.1117618135  64         0.8750000000   3.0
3       0.8139393939             0.0588721670  68         0.6086956522   4.0
4       0.8067754468             0.0875180564  50         0.6250000000   5.0
...
```

### 5. 预测

一旦我们找到了最佳分类模型，那么我们就可以使用他进行预测。

要进行预测，我们可以使用如下的几个步骤：

**a. 导出最佳模型**

 `export_best_classifier` 方法能够序列化，并保存选中的最佳模型到指定位置：

```python
results.export_best_classifier('path/to/model.pkl')
```

假如这个模型保存完毕，那么将会有如下信息打印：

```python
Classifier 94 saved as path/to/model.pkl
```

如果提供的路径是存在，那么可以通过添加参数 `force=True` 的方法来进行覆盖。

**b. 载入导出的模型**

一旦模型被导出，那么就可以使用  `atm.Model` 类中的 `load` 方法在读取一个已经保存的模型：

```python
from atm import Model

model = Model.load('path/to/model.pkl')
```

一旦你载入了这个模型，你就可以传递新的数据集到它的 `predict` 方法中进行预测：

```python
import pandas as pd

data = pd.read_csv(demo_datasets['pollution'])

predictions = model.predict(data.head())
```


# 接下来？

关于 **ATM** 更加详细的信息，以及所有的可能性和特性, 都可以访问这个[文档站点](https://HDI-Project.github.io/ATM/)。

在那你可以学习更多的[命令行接口](https://hdi-project.github.io/ATM/cli.html)，以及它的[REST API](https://hdi-project.github.io/ATM/rest.html)。同时，[如果对ATM做贡献](https://HDI-Project.github.io/ATM/community/contributing.html)也可以帮我我们开发进行的特性或者更酷的想法。