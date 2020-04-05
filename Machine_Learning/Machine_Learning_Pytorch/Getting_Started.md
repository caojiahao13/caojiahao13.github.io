---
layout: default
title: "Jiahao Cao's homepage"
description: Machine Learning With Pytorch
theme: jekyll-theme-cayman
---

Here I follow the [official toturial](https://pytorch.org/tutorials/beginner/deep_learning_60min_blitz.html) to get start with PyTorch.

PyTorch is vary similar to Numpy, actually it is a replacement for NumPy to use the power of GPUs.

### 1.Basic methods
#### Creating a tensor in PyTorch
```
x = torch.empty(5, 3)
x = torch.rand(5, 3)
x = torch.zeros(5, 3, dtype=torch.long)
x = x.new_ones(5, 3, dtype=torch.double)  # new_* methods take in sizes

# Construct a tensor directly from data
x = torch.tensor([5.5, 3])

#create a tensor based on an existing tensor
# new_* :  the returned Tensor has the same torch.dtype and torch.device as this tensor.
x = x.new_ones(5, 3, dtype=torch.double)
# Returns a tensor with the same size,dtype,layout,deviece as input
x = torch.randn_like(x, dtype=torch.float)  
```

#### useful class functions
```
x.size() # return a torch.Size object ( actually a tuple)
```
#### operators
```
# addition
y = torch.rand(5, 3)
# 1.
print(x + y)
# 2.
torch.add(x, y)
# 3.
result = torch.empty(5, 3)
torch.add(x, y, out=result)
print(result)
# 4.
y.add_(x)
print(y)
```
* Any operation that mutates a tensor in-place is post-fixed with an ```_```. For example: ```x.copy_(y)```, ```x.t_()```, will change ```x```.

#### some functions

- ```torch.view()``` to resize/reshape tensor

```
x = torch.randn(4, 4)
y = x.view(16)
z = x.view(-1, 8)
```

- ```torch.item()``` to get the value as a Python number if ```x``` is a one element tensor.

#### Converting a Torch Tensor to a NumPy Array

The Torch Tensor and NumPy array will **share their underlying memory locations** (if the Torch Tensor is on CPU), and **changing one will change the other**.

```
# tensor to narray

a = torch.ones(5)
b = a.numpy()
a.add_(1)
print(a)
print(b)
# tensor([2., 2., 2., 2., 2.])
# [2. 2. 2. 2. 2.]

# narray to tensor

a = np.ones(5)
b = torch.from_numpy(a)
np.add(a, 1, out=a)
print(a)
print(b)
#[2. 2. 2. 2. 2.]
#tensor([2., 2., 2., 2., 2.], dtype=torch.float64)
```

* All the Tensors on the CPU **except a CharTensor** support converting to NumPy and back.

#### CUDA Tensors
```
# let us run this cell only if CUDA is available
# We will use ``torch.device`` objects to move tensors in and out of GPU
if torch.cuda.is_available():
   device = torch.device("cuda")          # a CUDA device object
   y = torch.ones_like(x, device=device)  # directly create a tensor on GPU
   x = x.to(device)                       # or just use strings ``.to("cuda")``
   z = x + y
   print(z)
   print(z.to("cpu", torch.double))       # ``.to`` can also change dtype together!
```

### 2.Autograd: automatic differentiation
