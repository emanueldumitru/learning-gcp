### Introduction to tensorflow

- Understand the key components of TensorFlow
- Use the tf.data library to manipulate data and large datasets
- Create machine learning models in TensorFlow
- Use Keras sequential and functional APIs for model creation with TensorFlow 2.x
- Train, deploy and productionize ML models at scale with Cloud AI Platform



numeric programming library
regularization can improve the performance of the model

open-source framework for numeric computation that uses directed graphs


nodes represent mathematical operations
edges represent arrays of data


a tensor is an n-dimensional of data

rank 0 - scalar
rank 1 tensor - vector
rank 2 tensor - matrix
rank 3 tensor
rank 4 tensor

flow to the graph

portable between different devices
CPUs, GPUs, TPUs


portable, powerfull, production ready
the first repository on github for machine learning

represent numeric computations using a Directed Acyclic Graph ( DAG )

Tensorflow API


- TF runs on different hardware ( GPU, CPU, TPU, Android)
- C++ api is quite low level ( Core TF C++ )
- Python API gives you full control ( Core Tensorflow Python )
- Components useful when building custom NN models ( tf.losses, tf.metrics, tf.optimizers, etc. )
- high leve apis for distributed training ( **tf.estimator**, tf.keras, tf.data )

Run TF at scale with AI Platform

tf.losses - Cross-Entropy loss function for Classification

tensors are immutable structures


### Components of TensorFlow: Tensors and Variables

a tensor is an N-dimensional array of data

scalar ```tf.constant(3)``` shape ()

vector ```tf.constant([3,5,7])``` shape (3,)

matrix ```tf.constant([[3,5,7],[4, 6, 8]])``` shape (2,3)

3d tensor ```tf.constant([[[3,5,7], [4,6,8]],[[1,2,3], [4,5,6]]])``` shape(2,2,3)

nd tensor ```tf.stack([x3,x4])``` shape (2,4,2,3)

tf.constnat produce tensor with constant values
tf.variable produce tensors that can be modified

tf.shape

tensors can be sliced 

tf.reshape

```x = tf.Variable(2.0m dtype=tf.float32, name = 'my_variable') ``` 
model weights

tf.matmul

Tensorflow can compute the derivative of a function with respect to any parameter

GradientTape records operations for Automatic Differentiation


**Lab for tensors and variables**
**Lab for Writing low-level tensorflow code**



### Design and build a tensorflow input data pipeline

Parameters the values inside the values held by the model

You can build with Tensorflow your own customer layers and models by extending / subclassed

ResNet50 v1.5 on NVIDIA@ Tesla@V100s on Google Cloud 
ResNet50 best model for image classification


Training and Inference phase

tf.data.API
- build complex input pipelines from simple, reusable pieces
- build pipelines for multiple data types
- handle large amounts of data; perform complex transformations


Creating a dataset from in-memory tensors

from_tensors, from_tensors_slices - tensorflow can work with in-memory and with files


bucketized_columns
embedding_columns
tf.data.Dataset

feature columns

