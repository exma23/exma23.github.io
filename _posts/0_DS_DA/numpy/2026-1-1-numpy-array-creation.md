---
layout: post
title: Numpy array creation
status: ongoing
categories: data_analysis
author: exma23
---

# **22/9/2026**
## **I. Basic**
Important attributes of `ndarray` objects:
- `ndarray.dim`: number of axes (dimensions) of the array.
- `ndarray.shape`: a tuple whose length is the number of axes.
- `ndarray.size`: total number of elements of the array, equal to the product of the elements of `shape`.
- `ndarray.dtype`, `ndarray.itemsize`
Several ways to create arrays:
- Call `array` with only 1 arguments. `array` transforms sequences of sequences into two-dimensional arrays, sequences of sequences into three-dimensional arrays, and so on. The type can also be specified at creation time.
    ```
        a = np.array([2,3,4])
        b = np.array([(1.5,2,3), (4,5,6)], dtype=np.complex128)
    ```
- Create arrays without specifying the values:
    ```
        # 1. zeros
        a = np.zeros((3,4))
        # 2. ones
        b = np.ones((2,3,4), dtype=np.int16)
        # 3. empty (random values depending on the state of the memory)
        c = np.empty((2,3))
        # 4. arange (start, begin, step)
        d = np.arange(10,30,5)
        e = np.arange(0,2,0.3)
        # 5. linspace (start, bgein, number of elements)
        e = np.linspace(0, 2 * pi, 100)
    ```
- Basic operations:
    - `+, -, *`: element-wise
    - `@, A.dot(B)`: matrix product
    - `+=, *=`: modifying existing array
    - Specify `axis` parameter you can apply an operation along the specified axis of an array
- Universal functions: familiar mathematical functions such as `sin, cos, sqrt, exp`
## **II.  Slicing**
Standard rules of sequence slicing apply to basic slicing on a per-dimension basis:
- Basic slice syntax: `i:j:k` (`i` is the starting index, `j` is the stopping index, `k` is the step). This selects `i, i + k, ..., i + (m-1)k` where `m = q + r, j - i = qk + r`, so that `i + (m - 1)k < j`.
    ```
        x = np.arange(0, 9, 1)
        x[1:7:2]
        array([1,3,5])
    ```
- Negative `i, j` are interpreted as `n + i` and `n + j` where `n` is the number of elements in the corresponding dimension. Negative `k` makes stepping go towards smaller indices
    ```
        x[-2:10]
        array([8,9])
        x[-3:3:-1]
        array([7,6,5,4])
    ```
- Slicing without specify `i, j`:
    - If `i` is not given it defaults to 0 for `k > 0` and `n - 1` for `k < 0`.
    - If `j` is not given it defaults to `n` for `k > 0` and `- n - 1` for `k < 0`.
    - If `k` is not given, it defaults to 1.
    ```
        # first dim
        arr[i::k] == arr[i::k, :, :] == arr[i::k, ...]
        # second dim
        arr[:, i::k, ...] == arr[:, i::k, :]
        # dimension 6th in 9-dim array
        arr[..., i:k, :, :]

    ```
- If the number of objects in the selection tuple is less than `N`, then `:` is assumed for any subsequent dimensions. For example
    ```
        x = np.array([[[1], [2], [3]], [[4], [5], [6]]])
        x.shape = (2,3,1)
        x[1:2]
        array([[[4], [5], [6]]])
    ```
- If the selection tuple has all entries `:` except the `p`-th entry which is a slice object `i:j:k`, then the returned array has dimension `N` formed by stacking, along the `p`-th axis, the subarrays returned by integer indexing of elements `i, i + k, ..., i + (m-1)k < j`
-Basic slicing with more than one non-`:` entry in the slicing tuple, acts like repeated application of slicing using a single non-`:` entry, where the non-`:` entries are sucessively taken (with all other non-`:` entries replaced by `:`). Thus, `x[ind1,... ind2,:]` acts like `x[ind1][..., ind2, :]` under basic slicing
- Each `newaxis` object in the selection tuple serves to expand the dimensions of the resulting selection by one unit-length dimension. The added dimension is the position of the `newaxis` object in the selection tuple. `newaxis` is an alias for `None` and `None` can be used in place of this with the same result. This can be handy to combine two arrays in a way that otherwise would require explicit reshaping operations. For example:
    ```
        x = np.arange(5)
        x[:, np.newaxis] + x[np.newaxis, :]
        (== x.reshape(5, 1) + x.reshape(1, 5)
        = [[0], [1], [2], [3], [4]]  + [[0, 1, 2, 3, 4]])
        array([[0, 1, 2, 3, 4],
                [1,2,3,4,5]])
    ```
## **III. Advanced indexing**
Advanced indexing always returns a copy of the data (contrast with basic slicing that returns a view)
### **1. Integer array indexing**
- Integer array indexing allows selection of arbitrary items in the array based on their N-dimensional index. Each integer array represents a number of indices into that dimension. Negative values are permitted in the index arrays and works as they do with single indices or slices.:
    ```
        x = np.arange(10, 1, -1)
        x[np.array([3,3,1,8])]
        array([7,7,9,2])
        x[np.array([3,3,-3,8])]
        array([7,7,4,2])
    ```
- If the index values are out of bounds, then an `IndexError` is thrown. Advanced indices always are broadcast and iterated as one:
    ```
        result[i_1, ..., i_M] == x[ind_1[i_1, ..., i_M]
                                    ind_2[i_1, ..., i_M],
                                    ...,
                                    ind_N[i_1, ..., i_M]]
    ```
    Note that the resulting shape is identical to the broadcast indexing array shapes  `ind_1, ..., ind_N`. If the indices cannot be broadcast to the same shape, an exception is raises.

- The simples multidimensional case:
    ```
        y = np.arange(35).reshape(5,7)
        y[np.array([0,2,4]), np.array([0,1,2])] == array([0, 15, 30])
    ```
In this case, if the index arrays have a matching shape, and there is an index array for each dimension of the array being indexed, the resultant array has the same shape as the index arrays, and the values correspond to the index set for each position in the index arrays. If the index arrays do not have the same shape, there is an attempt to broadcast them to the same shape (if they cannot, an exception is raised)
    ```
        y[np.array([0,2,4]), 1] == array([1, 15, 29])
    ```
The broadcasting mechanism permits index arrays to be combined with scalars for other indices. The effect is that the scalar value is used for all the corresponding values of the index arrays.
- It is possible to partially index an array with index arrays. It results in the construction of a new array where each value of the index array selects one row from the array being indexed and the resultant array has the resulting shape (number of index elements, size of row). For example:
    ```
        y[np.array([0,2,4])]
        array([[0, 1, 2, ...],
               [14, 15, 16, ...],
               [28, 29, 30, ...]])
    ```
In general, the shape of the resultant array will be the concatenation of the shape of the index array (or the shape that all the index arrays were broadcast to) with the shape of any unused dimensions (those not indexed) in the array being indexed. From each row, a specific element should be selected. The column index specifies the element to choose for the corresponding row.
    ```
        x = np.array([[1,2], [3,4], [5,6]])
        x[[0,1,2], [0,1,0]] = array([1,4,5])
    ```
- Broadcasting can be applied for array indexing. Below is an example. To use advanced indexing one needs to select all elements explicitly. However, since the indexing arrays above just repeat themselves, broadcasting can be used to simplify this. This broadcasting can also be achieved by using the function `ix_`:
    ```
        # 1. first version
        x = np.array([[0, 1, 2],
                      [3, 4, 5],
                      [6, 7, 8],
                      [9, 10, 11]])
        rows = np.array([[0, 0],
                         [3, 3]], dtype=np.intp)
        columns = np.array([[0,2],
                            [0,2]], dtype=np.intp)
        x[rows, columns] = array([[0,2],
                                  [9,11]])

        # 2. simplified version
        rows = np.array([0,3], dtype=np.intp)
        columns = np.array([0,2], dtype=np.intp)
        rows[:, np.newaxis] = array([[0],
                                     [3]])
        x[rows[:, np.newaxis], columns] = array([[0,2],
                                                 [9,11]])
        # 3. same version with ix_
        x[np.ix_(rows, columns)] = array([[0,2],
                                         [9, 11]])
    ```
    `np.ix_`: construct an open mesh from multiple sequences. This function takes N 1-D sequences and returns N outputs with N dimensions each. It converts multiple 1D index lists into indices with shapes suitable for obtaining the Cartesian product of all of them.
    ```
    # Example 1: select rows [1, 3] and columns [0, 4]
    A = np.arange(20).reshape(4, 5)
    A[np.ix_([1, 3], [0, 4])]
    # [[ 5,  9],
    #  [15, 19]]
    # Example 2: Cartesian product of 3 index lists
    A = np.arange(10 * 10 * 10).reshape(10, 10, 10)
    A[np.ix_([1, 3], [0, 4], [6, 7])].shape
    # (2, 2, 2), which is 2 × 2 × 2 = 8 combinations
    ```
### **2. Boolean array indexing**
- Boolean index has exactly as many dimensions as it is supposed to work with. If `obj.ndim == x.ndim`, `x[obj]` returns a 1-dimensional array filled with the elements of `x` corresponding to the `True` values of `obj`. The search order will be row-major (errors will be raised if shapes do not match). `x[ind_1, boolean_array, ind_2]` is equivalent to `x[(ind_1,) + boolean_array.nonzero() + (ind_2,)]`. Example below:
    ```
        x = np.array([1., -1., -2., 3])
        x[x < 0] += 20
    ```
- In general, when the boolean array has fewer dimensions than the array being indexed, this is equivalent to `x[b, ...]`, which means x is indexed by b followed by as many: as are needed to fill out the rank of x. Thus the shape of the result is one dimension containing the number of True elements of the boolean array, followed by the remaining dimensions of the array being indexed
    ```
    x = np.arange(35).reshape(5, 7)
    b = x > 20
    b[:, 5] = array([False, False, False,  True,  True])
    x[b[:, 5]] = array([[21, 22, 23, 24, 25, 26, 27],
                        [28, 29, 30, 31, 32, 33, 34]])
    ```
    Advanced example
    ```
        x = np.array([[ 0,  1,  2],
              [ 3,  4,  5],
              [ 6,  7,  8],
              [ 9, 10, 11]])
        rows = (x.sum(-1) % 2) == 0
        columns = [0, 2]
        x[np.ix_(rows, columns)] = array([[ 3,  5],
                                          [9, 11]])
    ```
## **IV. Combined indexing (Not fully understood yet)**
When there is at least one slice (:), ellipsis (...) or newaxis in the index (or the array has more dimensions than there are advanced indices), then the behaviour can be more complicated. It is like concatenating the indexing result for each advanced index element. In effect, the slice and index array operation are independent.
```
    y = np.arange(35).reshape(5,7)
    y[np.array([0, 2, 4]), 1:3] = array([[ 1,  2],
                                         [15, 16],
                                         [29, 30]])

    # equivalent to
    y[:, 1:3][np.array([0, 2, 4]), :]
```
There are two parts to the indexing operation, the subspace defined by the basic indexing (excluding integers) and the subspace from the advanced indexing part. Two cases of index combination need to be distinguished:
- The advanced indices are separated by a slice, Ellipsis or newaxis. For example x[arr1, :, arr2].
    Suppose `x.shape` is (10, 20, 30) and `ind` is a (2, 5, 2)-shaped indexing `intp` array, then `result = x[..., ind, :]` has shape (10, 2, 5, 2, 30) because the (20,)-shaped subspace has been replaced with a (2, 5, 2)-shaped broadcasted indexing subspace. If we let i, j, k loop over the (2, 5, 2)-shaped subspace then `result[..., i, j, k, :] = x[..., ind[i, j, k], :]`. This example produces the same result as `x.take(ind, axis=-2)`.

    In this case, the dimensions resulting from the advanced indexing operation come first in the result array, and the subspace dimensions after that.
- The advanced indices are all next to each other. For example x[..., arr1, arr2, :] but not x[arr1, :, 1] since 1 is an advanced index in this regard.
    Let `x.shape` be (10, 20, 30, 40, 50) and suppose ind_1 and ind_2 can be broadcast to the shape (2, 3, 4). Then `x[:, ind_1, ind_2]` has shape (10, 2, 3, 4, 40, 50) because the (20, 30)-shaped subspace from X has been replaced with the (2, 3, 4) subspace from the indices. However, `x[:, ind_1, :, ind_2]` has shape (2, 3, 4, 10, 30, 50) because there is no unambiguous place to drop in the indexing subspace, thus it is tacked-on to the beginning. It is always possible to use `.transpose()` to move the subspace anywhere desired. Note that this example cannot be replicated using `take`

    In the second case, the dimensions from the advanced indexing operations are inserted into the result array at the same spot as they were in the initial array (the latter logic is what makes simple advanced indexing behave just like slicing).

## **V. Flat iterator indexing**
`x.flat` returns an iterator that will iterate over the entire array (in C-contiguous style with the last index varying the fastest). This iterator object can also be indexed using basic slicing or advanced indexing as long as the selection object is not a tuple. This should be clear from the fact that `x.flat` is a 1-dimensional view. It can be used for integer indexing with 1-dimensional C-style-flat indices. The shape of any returned array is therefore the shape of the integer indexing object.


# **III.  Broadcasting**
