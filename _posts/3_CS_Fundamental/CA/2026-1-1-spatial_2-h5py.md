---
layout: post
title: Glossary - Operating systems
status: ongoing
categories: computer_system
author: exma23
---

# **1. 16/7/2026**
## **A. h5py introduction**
2 kind of objects:
- datasets: array-like collections of data
	- Like numpy arrays, datasets have both a shape and a data type
		```
			.shape, .dtype

			array-style slicing:
			[0], [start:end:step]
		```
- groups: folder-like containers that hold datasets and other groups
- Rule of thumbs:
		Groups work like dictionaries, and datasets work like numpy arrays

	```
		h5py.File: acts like a python dictionary
	```

Creating a file:
- Setting `mode` to `w` when the File object is initialized
	```
		import h5py
		import numpy as np
		f = h5py.File("mytestfile.hdf5", "w")
	```
	Other modes:
	- `w`: write
	- `a`: stands for all (read/write/create/access)
	- `r+`: read/write access
	- `w- or x`: create file, fail if exists
- `create_dataset`
	```
		dset = f.create_dataset("mydataset", (100,), dtype='i')
	```
- `File` is a context manager, the following code works too:
	```
		import h5py
		import numpy as np

		with h5py.File("mytestfile.hdf5", "w") as f:
			dset = f.create_dataset("mydataset", (100,), dtype="i")
	```

## **B. Groups and hierarchical organization**
"HDF" stands for hierarchical data format. Every object in an HDF5 file has a name, and they are arranged in a POSIX-style hierarchy with `/`-separators:
- "folders" in this system are called groups. The `File` object we created is itself a group, in this case the root group, named `/`:
	```
		f.name = '/'
	```
	Create a subgroup is accomplished via `create_group`. But we need to open the file in the "append" mode first (Read/write if exists, create otherwise)
	```
		f = h5py.File("mydataset.hdf5", "a")
		grp = f.create_group("subgroup")
	```
- `Group` objects also have the `create_*` methods like File, also can specify a full path:
	```
		dset2 = grp.create_dataset("another_dataset", (50,), dtype='f')
		dset2.name == '/subgroup/another_dataset'

		dset3 = f.create_dataset('subgroup2/dataset_three', (10,), dtype='i')
		dset3.name == '/subgroup2/dataset_three'
	```

Iterating over a group provides the names of its members:
```
	for name in f:
		print(name)

	"mydataset" in f == True
	"subgroup/another_dataset" in f == True
```

Other methods:
- `keys()`, `values()`, `items()`, `iter()`,`get()`
## **C. Attributes**
You can store metadata right next to the data it describes. All groups and datasets support attached named bits of data called `attrs` proxy object:
```
	dset.attrs['temperature'] = 99.5
	'temperature' in dset.attrs == True
```
## **D. Groups**
-  **File** object is *root group*, also the entry point into the file:
```
	f = h5py.File('foo.hdf5', 'w')
		f.name == '/'
```

Names of all objects in the file are all text strings `str`.
=> These will be encoded with the HDF5-approved UTF-8 encoding before being passes to the HDF5 C library
=> Objects path name may also be retrieved using byte strings, which will be passed on to HDF5 as-is.
- Create groups:
```
	grp = f.create_group("bar")
	grp.name == '/bar'
	subgrp = grp.create_group("baz")
	subgrp.name == "/baz/baz"

	grp3 = f["/some/long"]
	grp3.name == "/some/long"
```
- Groups have: `keys()`, `values()` can use standard syntax to:
```
	del subgroup["MyDataset"]
```
Note:
***
When using h5py from Python 3, `keys()` - `values()` - `items()` methods will return *view-like objects* instead of lists (to avoid fully loading into the disk). These objects support membership testing and iteration, but can't be sliced like lists
***


```
| HDF5 code | meaning                          |
| --------- | -------------------------------- |
| `"b"`     | signed 8-bit int                 |
| `"B"`     | unsigned 8-int bit               |
| `"h"`     | signed 16-bit int                |
| `"H"`     | unsigned 16-bit int              |
| `"i"`     | signed 32-bit int                |
| `"I"`     | unsigned 32-bit int              |
| `"l"`     | signed long (platform-dependent) |
| `"L"`     | unsigned long                    |
| `"f"`     | 32-bit float                     |
| `"d"`     | 64-bit float                     |
```

