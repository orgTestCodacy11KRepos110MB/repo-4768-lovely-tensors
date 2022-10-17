lovely tensors
================

<!-- WARNING: THIS FILE WAS AUTOGENERATED! DO NOT EDIT! -->

## Install

``` sh
pip install lovely
```

## How to use

How often do you find yourself debuggin a neural network? You dump a
tensor to the cell output, and see this:

``` python
numbers
```

    tensor([[[-0.3541, -0.3369, -0.4054,  ..., -0.5596, -0.4739,  2.2489],
             [-0.4054, -0.4226, -0.4911,  ..., -0.9192, -0.8507,  2.1633],
             [-0.4739, -0.4739, -0.5424,  ..., -1.0390, -1.0390,  2.1975],
             ...,
             [-0.9020, -0.8335, -0.9363,  ..., -1.4672, -1.2959,  2.2318],
             [-0.8507, -0.7822, -0.9363,  ..., -1.6042, -1.5014,  2.1804],
             [-0.8335, -0.8164, -0.9705,  ..., -1.6555, -1.5528,  2.1119]],

            [[-0.1975, -0.1975, -0.3025,  ..., -0.4776, -0.3725,  2.4111],
             [-0.2500, -0.2325, -0.3375,  ..., -0.7052, -0.6702,  2.3585],
             [-0.3025, -0.2850, -0.3901,  ..., -0.7402, -0.8102,  2.3761],
             ...,
             [-0.4251, -0.2325, -0.3725,  ..., -1.0903, -1.0203,  2.4286],
             [-0.3901, -0.2325, -0.4251,  ..., -1.2304, -1.2304,  2.4111],
             [-0.4076, -0.2850, -0.4776,  ..., -1.2829, -1.2829,  2.3410]],

            [[-0.6715, -0.9853, -0.8807,  ..., -0.9678, -0.6890,  2.3960],
             [-0.7238, -1.0724, -0.9678,  ..., -1.2467, -1.0201,  2.3263],
             [-0.8284, -1.1247, -1.0201,  ..., -1.2641, -1.1596,  2.3786],
             ...,
             [-1.2293, -1.4733, -1.3861,  ..., -1.5081, -1.2641,  2.5180],
             [-1.1944, -1.4559, -1.4210,  ..., -1.6476, -1.4733,  2.4308],
             [-1.2293, -1.5256, -1.5081,  ..., -1.6824, -1.5256,  2.3611]]])

Was it really useful?

What is the shape of the tensor?  
What are the statistics?  
Are any of the values `nan` or `int`?  
Is it an image of a man holding a tench?

``` python
import lovely_tensors.tensors as lt
```

    ModuleNotFoundError: No module named 'lovely_tensors'

``` python
# A very short tensor
print(lt.lovely(numbers.view(-1)[:2]))
```

``` python
# A slightly longer tensor
print(lt.lovely(numbers.view(-1)[:6].view(2,3)))
```

``` python
t = numbers.view(-1)[:12].clone()

t[0] *= 10000
t[1] /= 10000
t[2] = float('inf')
t[3] = float('-inf')
t[4] = float('nan')
t = t.reshape((2,6))

print(t)
print("\n")

# A spicy tensor
print(lt.lovely(t))

# A zero tensor
print(lt.lovely(torch.zeros(10, 10)))
```

``` python
# Too long to show values
lt.lovely(numbers)
```

Now the important queston - is it the Tenchman?

``` python
lt.show_rgb(numbers)
```

*Maaaaybe?* Looks like someone normalized him.

``` python
in_stats = { "mean": (0.485, 0.456, 0.406), "std": (0.229, 0.224, 0.225) }
lt.show_rgb(numbers, in_stats)
```

There can be no doubt.

One last thing - let’s monkey-patch `torch.Tensor` for convenience.

``` python
lt.monkey_patch()

t
```

``` python
t.verbose
```

``` python
t.plain
```

``` python
numbers.rgb
```

``` python
# The values are the same, but we de-norm before displaying.
numbers.denorm=in_stats
numbers.rgb
```
