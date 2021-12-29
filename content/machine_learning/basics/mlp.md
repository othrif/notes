---
title: "Multi-layer perceptron (MLP) from scratch"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### MLP API


```python
import numpy as np
import sys


class NeuralNetMLP(object):
    """ Feedforward neural network / Multi-layer perceptron classifier.

    Parameters
    ------------
    n_hidden : int (default: 30)
        Number of hidden units.
    l2 : float (default: 0.)
        Lambda value for L2-regularization.
        No regularization if l2=0. (default)
    epochs : int (default: 100)
        Number of passes over the training set.
    eta : float (default: 0.001)
        Learning rate.
    shuffle : bool (default: True)
        Shuffles training data every epoch if True to prevent circles.
    minibatch_size : int (default: 1)
        Number of training examples per minibatch.
    seed : int (default: None)
        Random seed for initializing weights and shuffling.

    Attributes
    -----------
    eval_ : dict
      Dictionary collecting the cost, training accuracy,
      and validation accuracy for each epoch during training.

    """
    def __init__(self, n_hidden=30,
                 l2=0., epochs=100, eta=0.001,
                 shuffle=True, minibatch_size=1, seed=None):

        self.random = np.random.RandomState(seed)
        self.n_hidden = n_hidden
        self.l2 = l2
        self.epochs = epochs
        self.eta = eta
        self.shuffle = shuffle
        self.minibatch_size = minibatch_size

    def _onehot(self, y, n_classes):
        """Encode labels into one-hot representation

        Parameters
        ------------
        y : array, shape = [n_examples]
            Target values.
        n_classes : int
            Number of classes

        Returns
        -----------
        onehot : array, shape = (n_examples, n_labels)

        """
        onehot = np.zeros((n_classes, y.shape[0]))
        for idx, val in enumerate(y.astype(int)):
            onehot[val, idx] = 1.
        return onehot.T

    def _sigmoid(self, z):
        """Compute logistic function (sigmoid)"""
        return 1. / (1. + np.exp(-np.clip(z, -250, 250)))

    def _forward(self, X):
        """Compute forward propagation step"""

        # step 1: net input of hidden layer
        # [n_examples, n_features] dot [n_features, n_hidden]
        # -> [n_examples, n_hidden]
        z_h = np.dot(X, self.w_h) + self.b_h

        # step 2: activation of hidden layer
        a_h = self._sigmoid(z_h)

        # step 3: net input of output layer
        # [n_examples, n_hidden] dot [n_hidden, n_classlabels]
        # -> [n_examples, n_classlabels]

        z_out = np.dot(a_h, self.w_out) + self.b_out

        # step 4: activation output layer
        a_out = self._sigmoid(z_out)

        return z_h, a_h, z_out, a_out

    def _compute_cost(self, y_enc, output):
        """Compute cost function.

        Parameters
        ----------
        y_enc : array, shape = (n_examples, n_labels)
            one-hot encoded class labels.
        output : array, shape = [n_examples, n_output_units]
            Activation of the output layer (forward propagation)

        Returns
        ---------
        cost : float
            Regularized cost

        """
        L2_term = (self.l2 *
                   (np.sum(self.w_h ** 2.) +
                    np.sum(self.w_out ** 2.)))

        term1 = -y_enc * (np.log(output))
        term2 = (1. - y_enc) * np.log(1. - output)
        cost = np.sum(term1 - term2) + L2_term
        
        # If you are applying this cost function to other
        # datasets where activation
        # values maybe become more extreme (closer to zero or 1)
        # you may encounter "ZeroDivisionError"s due to numerical
        # instabilities in Python & NumPy for the current implementation.
        # I.e., the code tries to evaluate log(0), which is undefined.
        # To address this issue, you could add a small constant to the
        # activation values that are passed to the log function.
        #
        # For example:
        #
        # term1 = -y_enc * (np.log(output + 1e-5))
        # term2 = (1. - y_enc) * np.log(1. - output + 1e-5)
        
        return cost

    def predict(self, X):
        """Predict class labels

        Parameters
        -----------
        X : array, shape = [n_examples, n_features]
            Input layer with original features.

        Returns:
        ----------
        y_pred : array, shape = [n_examples]
            Predicted class labels.

        """
        z_h, a_h, z_out, a_out = self._forward(X)
        y_pred = np.argmax(z_out, axis=1)
        return y_pred

    def fit(self, X_train, y_train, X_valid, y_valid):
        """ Learn weights from training data.

        Parameters
        -----------
        X_train : array, shape = [n_examples, n_features]
            Input layer with original features.
        y_train : array, shape = [n_examples]
            Target class labels.
        X_valid : array, shape = [n_examples, n_features]
            Sample features for validation during training
        y_valid : array, shape = [n_examples]
            Sample labels for validation during training

        Returns:
        ----------
        self

        """
        n_output = np.unique(y_train).shape[0]  # number of class labels
        n_features = X_train.shape[1]

        ########################
        # Weight initialization
        ########################

        # weights for input -> hidden
        self.b_h = np.zeros(self.n_hidden)
        self.w_h = self.random.normal(loc=0.0, scale=0.1,
                                      size=(n_features, self.n_hidden))

        # weights for hidden -> output
        self.b_out = np.zeros(n_output)
        self.w_out = self.random.normal(loc=0.0, scale=0.1,
                                        size=(self.n_hidden, n_output))

        epoch_strlen = len(str(self.epochs))  # for progress formatting
        self.eval_ = {'cost': [], 'train_acc': [], 'valid_acc': []}

        y_train_enc = self._onehot(y_train, n_output)

        # iterate over training epochs
        for i in range(self.epochs):

            # iterate over minibatches
            indices = np.arange(X_train.shape[0])

            if self.shuffle:
                self.random.shuffle(indices)

            for start_idx in range(0, indices.shape[0] - self.minibatch_size +
                                   1, self.minibatch_size):
                batch_idx = indices[start_idx:start_idx + self.minibatch_size]

                # forward propagation
                z_h, a_h, z_out, a_out = self._forward(X_train[batch_idx])

                ##################
                # Backpropagation
                ##################

                # [n_examples, n_classlabels]
                delta_out = a_out - y_train_enc[batch_idx]

                # [n_examples, n_hidden]
                sigmoid_derivative_h = a_h * (1. - a_h)

                # [n_examples, n_classlabels] dot [n_classlabels, n_hidden]
                # -> [n_examples, n_hidden]
                delta_h = (np.dot(delta_out, self.w_out.T) *
                           sigmoid_derivative_h)

                # [n_features, n_examples] dot [n_examples, n_hidden]
                # -> [n_features, n_hidden]
                grad_w_h = np.dot(X_train[batch_idx].T, delta_h)
                grad_b_h = np.sum(delta_h, axis=0)

                # [n_hidden, n_examples] dot [n_examples, n_classlabels]
                # -> [n_hidden, n_classlabels]
                grad_w_out = np.dot(a_h.T, delta_out)
                grad_b_out = np.sum(delta_out, axis=0)

                # Regularization and weight updates
                delta_w_h = (grad_w_h + self.l2*self.w_h)
                delta_b_h = grad_b_h # bias is not regularized
                self.w_h -= self.eta * delta_w_h
                self.b_h -= self.eta * delta_b_h

                delta_w_out = (grad_w_out + self.l2*self.w_out)
                delta_b_out = grad_b_out  # bias is not regularized
                self.w_out -= self.eta * delta_w_out
                self.b_out -= self.eta * delta_b_out

            #############
            # Evaluation
            #############

            # Evaluation after each epoch during training
            z_h, a_h, z_out, a_out = self._forward(X_train)
            
            cost = self._compute_cost(y_enc=y_train_enc,
                                      output=a_out)

            y_train_pred = self.predict(X_train)
            y_valid_pred = self.predict(X_valid)

            train_acc = ((np.sum(y_train == y_train_pred)).astype(np.float) /
                         X_train.shape[0])
            valid_acc = ((np.sum(y_valid == y_valid_pred)).astype(np.float) /
                         X_valid.shape[0])

            sys.stderr.write('\r%0*d/%d | Cost: %.2f '
                             '| Train/Valid Acc.: %.2f%%/%.2f%% ' %
                             (epoch_strlen, i+1, self.epochs, cost,
                              train_acc*100, valid_acc*100))
            sys.stderr.flush()

            self.eval_['cost'].append(cost)
            self.eval_['train_acc'].append(train_acc)
            self.eval_['valid_acc'].append(valid_acc)

        return self
```

### Get data


```python
import sys
import gzip
import shutil
import os

if (sys.version_info > (3, 0)):
    writemode = 'wb'
else:
    writemode = 'w'

zipped_mnist = [os.path.join('/tmp/',f) for f in os.listdir('/tmp/') if f.endswith('ubyte.gz')]
for z in zipped_mnist:
    with gzip.GzipFile(z, mode='rb') as decompressed, open(z[:-3], writemode) as outfile:
        outfile.write(decompressed.read()) 
```


```python
import os
import struct
import numpy as np
 
def load_mnist(path, kind='train'):
    """Load MNIST data from `path`"""
    labels_path = os.path.join(path, 
                               '%s-labels-idx1-ubyte' % kind)
    images_path = os.path.join(path, 
                               '%s-images-idx3-ubyte' % kind)
        
    with open(labels_path, 'rb') as lbpath:
        magic, n = struct.unpack('>II', 
                                 lbpath.read(8))
        labels = np.fromfile(lbpath, 
                             dtype=np.uint8)

    with open(images_path, 'rb') as imgpath:
        magic, num, rows, cols = struct.unpack(">IIII", 
                                               imgpath.read(16))
        images = np.fromfile(imgpath, 
                             dtype=np.uint8).reshape(len(labels), 784)
        images = ((images / 255.) - .5) * 2
 
    return images, labels

X_train, y_train = load_mnist('/tmp/', kind='train')
print('Rows: %d, columns: %d' % (X_train.shape[0], X_train.shape[1]))
X_test, y_test = load_mnist('/tmp/', kind='t10k')
print('Rows: %d, columns: %d' % (X_test.shape[0], X_test.shape[1]))
```

    Rows: 60000, columns: 784
    Rows: 10000, columns: 784


### Train MLP


```python
n_epochs = 75
nn = NeuralNetMLP(n_hidden=100, 
                  l2=0.01, 
                  epochs=n_epochs, 
                  eta=0.0005,
                  minibatch_size=100, 
                  shuffle=True,
                  seed=1)

nn.fit(X_train=X_train[:55000], 
       y_train=y_train[:55000],
       X_valid=X_train[55000:],
       y_valid=y_train[55000:])
```

    75/75 | Cost: 9515.78 | Train/Valid Acc.: 97.94%/97.60%  




    <__main__.NeuralNetMLP at 0x112ea8850>



### Plot cost and accuracy


```python
import matplotlib.pyplot as plt


plt.plot(range(nn.epochs), nn.eval_['cost'])
plt.ylabel('Cost')
plt.xlabel('Epochs')
#plt.savefig('images/12_07.png', dpi=300)
plt.show()

```


![png](mlp_9_0.png)



```python
plt.plot(range(nn.epochs), nn.eval_['train_acc'], 
         label='Training')
plt.plot(range(nn.epochs), nn.eval_['valid_acc'], 
         label='Validation', linestyle='--')
plt.ylabel('Accuracy')
plt.xlabel('Epochs')
plt.legend(loc='lower right')
#plt.savefig('images/12_08.png', dpi=300)
plt.show()
```


![png](mlp_10_0.png)


### Determine test accuracy and plot some examples


```python
y_test_pred = nn.predict(X_test)
acc = (np.sum(y_test == y_test_pred)
       .astype(np.float) / X_test.shape[0])

print('Test accuracy: %.2f%%' % (acc * 100))
```

    Test accuracy: 96.93%



```python
miscl_img = X_test[y_test != y_test_pred][:25]
correct_lab = y_test[y_test != y_test_pred][:25]
miscl_lab = y_test_pred[y_test != y_test_pred][:25]

fig, ax = plt.subplots(nrows=5, ncols=5, sharex=True, sharey=True)
ax = ax.flatten()
for i in range(25):
    img = miscl_img[i].reshape(28, 28)
    ax[i].imshow(img, cmap='Greys', interpolation='nearest')
    ax[i].set_title('%d) t: %d p: %d' % (i+1, correct_lab[i], miscl_lab[i]))

ax[0].set_xticks([])
ax[0].set_yticks([])
plt.tight_layout()
#plt.savefig('images/12_09.png', dpi=300)
plt.show()

```


![png](mlp_13_0.png)


### Break MLP API for learning


```python
def _onehot(y, n_classes):
    onehot = np.zeros((n_classes, y.shape[0]))
    for idx, val in enumerate(y.astype(int)):
        onehot[val, idx] = 1.
    return onehot.T
```


```python
def _sigmoid(z):
    """Compute logistic function (sigmoid)"""
    return 1. / (1. + np.exp(-np.clip(z, -250, 250)))
```


```python
def _forward(X, w_h, b_h, w_out, b_out):
    """Compute forward propagation step"""
    
    # step 1: net input of hidden layer
    # [n_examples, n_features] dot [n_features, n_hidden]
    # -> [n_examples, n_hidden]
    z_h = np.dot(X, w_h) + b_h
    
    # step 2: activation of hidden layer
    a_h = _sigmoid(z_h)
    
    # step 3: net input of output layer
    # [n_examples, n_hidden] dot [n_hidden, n_classlabels]
    # -> [n_examples, n_classlabels]
    z_out = np.dot(a_h, w_out) + b_out
    
    # step 4: activation output layer
    a_out = _sigmoid(z_out)
    
    return z_h, a_h, z_out, a_out
```


```python
def _compute_cost(y_enc, output, l2, w_h, w_out):
        """Compute cost function.

        Parameters
        ----------
        y_enc : array, shape = (n_examples, n_labels)
            one-hot encoded class labels.
        output : array, shape = [n_examples, n_output_units]
            Activation of the output layer (forward propagation)

        Returns
        ---------
        cost : float
            Regularized cost

        """
        L2_term = (l2 *
                   (np.sum(w_h ** 2.) +
                    np.sum(w_out ** 2.)))

        term1 = -y_enc * (np.log(output))
        term2 = (1. - y_enc) * np.log(1. - output)
        cost = np.sum(term1 - term2) + L2_term
        
        
        return cost
```


```python
def predict(X, w_h, b_h, w_out, b_out):
        """Predict class labels

        Parameters
        -----------
        X : array, shape = [n_examples, n_features]
            Input layer with original features.

        Returns:
        ----------
        y_pred : array, shape = [n_examples]
            Predicted class labels.

        """
        z_h, a_h, z_out, a_out = _forward(X, w_h, b_h, w_out, b_out)
        y_pred = np.argmax(z_out, axis=1)
        return y_pred
```


```python
def fit(X_train, y_train, X_valid, y_valid, epochs):
    
    # Parameters
    n_hidden = 30
#    epochs = 10
    shuffle = True
    minibatch_size = 100
    l2 = 0.01
    eta=0.0005
    
    print(f'X train shape: {X_train.shape}')
    print(f'y train shape: {y_train.shape}')
    print(f'X test shape: {X_valid.shape}')
    print(f'y test shape: {y_valid.shape}')
    
    n_output = np.unique(y_train).shape[0]  # number of class labels
    n_features = X_train.shape[1]
    
    print(f'\nNumber of outputs: {n_output}')
    print(f'Number of outputs: {n_features}')
    
    # Weight initialization

    random = np.random.RandomState(123)
    
    # weights for input -> hidden
    b_h = np.zeros(n_hidden)
    w_h = random.normal(loc=0.0, scale=0.1, size=(n_features, n_hidden))
    print(f'\nBias input -> hidden: {b_h.shape}')
    print(f'Weights input -> hidden: {w_h.shape}')
    
    # weights for hidden -> output
    b_out = np.zeros(n_output)
    w_out = random.normal(loc=0.0, scale=0.1, size=(n_hidden, n_output))
    print(f'\nBias hidden -> output: {b_out.shape}')
    print(f'Weights hidden -> output: {w_out.shape}')
    
    
    epoch_strlen = len(str(epochs))  # for progress formatting
    eval_ = {'cost': [], 'train_acc': [], 'valid_acc': []}
    
    y_train_enc = _onehot(y_train, n_output)
    print(f'\nY train: {y_train.shape}')
    print(f'\nY train encoding: {y_train_enc.shape}')
    
    # iterate over training epochs
    for i in range(epochs):
        
        # iterate over minibatches
        indices = np.arange(X_train.shape[0])
        
        if shuffle:
            random.shuffle(indices)
            
        
        for j, start_idx in enumerate(range(0, indices.shape[0] - minibatch_size + 1, minibatch_size)):
            
            #print(f'start_idx={start_idx+minibatch_size}/{indices.shape[0]} -> {j+1}/{indices.shape[0]/minibatch_size}')
            
            batch_idx = indices[start_idx:start_idx + minibatch_size]
            
            ##################
            # forward propagation
            ##################
            
            z_h, a_h, z_out, a_out = _forward(X_train[batch_idx], w_h, b_h, w_out, b_out)
            
            ##################
            # Backpropagation
            ##################
            
            # [n_examples, n_classlabels]
            delta_out = a_out - y_train_enc[batch_idx]
            
            # [n_examples, n_hidden]
            sigmoid_derivative_h = a_h * (1. - a_h)
            
            # [n_examples, n_classlabels] dot [n_classlabels, n_hidden]
            # -> [n_examples, n_hidden]
            delta_h = (np.dot(delta_out, w_out.T) * sigmoid_derivative_h)
            
            # [n_features, n_examples] dot [n_examples, n_hidden]
            # -> [n_features, n_hidden]
            grad_w_h = np.dot(X_train[batch_idx].T, delta_h)
            grad_b_h = np.sum(delta_h, axis=0)
            
            # [n_hidden, n_examples] dot [n_examples, n_classlabels]
            # -> [n_hidden, n_classlabels]
            grad_w_out = np.dot(a_h.T, delta_out)
            grad_b_out = np.sum(delta_out, axis=0)
            
            # Regularization and weight updates
            delta_w_h = (grad_w_h + l2*w_h)
            delta_b_h = grad_b_h # bias is not regularized
            w_h -= eta * delta_w_h
            b_h -= eta * delta_b_h
            
            delta_w_out = (grad_w_out + l2*w_out)
            delta_b_out = grad_b_out  # bias is not regularized
            w_out -= eta * delta_w_out
            b_out -= eta * delta_b_out
            
            
        #############
        # Evaluation
        #############
        # Evaluation after each epoch during training
        z_h, a_h, z_out, a_out = _forward(X_train, w_h, b_h, w_out, b_out)
        
        cost = _compute_cost(y_enc=y_train_enc, output=a_out, l2=l2, w_h=w_h, w_out=w_out)
        y_train_pred = predict(X_train, w_h, b_h, w_out, b_out)
        y_valid_pred = predict(X_valid, w_h, b_h, w_out, b_out)
        train_acc = ((np.sum(y_train == y_train_pred)).astype(np.float) /
                        X_train.shape[0])
        valid_acc = ((np.sum(y_valid == y_valid_pred)).astype(np.float) /
                        X_valid.shape[0])

        sys.stderr.write('\r%0*d/%d | Cost: %.2f '
                            '| Train/Valid Acc.: %.2f%%/%.2f%% ' %
                            (epoch_strlen, i+1, epochs, cost,
                            train_acc*100, valid_acc*100))
        sys.stderr.flush()
        eval_['cost'].append(cost)
        eval_['train_acc'].append(train_acc)
        eval_['valid_acc'].append(valid_acc)
        
    return eval_
```


```python
epochs = 10
eval_ = fit(X_train=X_train[:55000], 
       y_train=y_train[:55000],
       X_valid=X_train[55000:],
       y_valid=y_train[55000:], epochs=epochs)
```

    X train shape: (55000, 784)
    y train shape: (55000,)
    X test shape: (5000, 784)
    y test shape: (5000,)
    
    Number of outputs: 10
    Number of outputs: 784
    
    Bias input -> hidden: (30,)
    Weights input -> hidden: (784, 30)
    
    Bias hidden -> output: (10,)
    Weights hidden -> output: (30, 10)
    
    Y train: (55000,)
    
    Y train encoding: (55000, 10)


    10/10 | Cost: 31420.29 | Train/Valid Acc.: 91.69%/93.38%  


```python
import matplotlib.pyplot as plt


plt.plot(range(epochs), eval_['cost'])
plt.ylabel('Cost')
plt.xlabel('Epochs')
#plt.savefig('images/12_07.png', dpi=300)
plt.show()
```


![png](mlp_22_0.png)



```python
plt.plot(range(epochs), eval_['train_acc'], 
         label='Training')
plt.plot(range(epochs), eval_['valid_acc'], 
         label='Validation', linestyle='--')
plt.ylabel('Accuracy')
plt.xlabel('Epochs')
plt.legend(loc='lower right')
#plt.savefig('images/12_08.png', dpi=300)
plt.show()
```


![png](mlp_23_0.png)

