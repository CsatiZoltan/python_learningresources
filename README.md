# python_learningresources
Links to books, repositories, blogs and videos about useful Python resources


## Language

### Language fundamentals

- [Difference between lists and tuples](https://stackoverflow.com/questions/626759/whats-the-difference-between-lists-and-tuples)
- [Create dictionary from two lists](https://stackoverflow.com/questions/209840/convert-two-lists-into-a-dictionary)
- [Index a list with another list](https://stackoverflow.com/a/1012197/4892892)
- [Single list from a list of lists](https://stackoverflow.com/questions/952914/how-to-make-a-flat-list-out-of-list-of-lists); example and expected output:
   ```python
   nested_list = [['some'], ['items']]
   flat_list = ['some', 'items']
   ```
   - [List comprehension](https://stackoverflow.com/a/952952/4892892)
      ```python
      flat_list = [item for sublst in nested_list for item in sublst]
      ```
   - [Chaining](https://stackoverflow.com/a/953097/4892892)
      ```python
      import itertools
      flat_list = list(itertools.chain.from_iterable(nested_list))
      # equivalently: flat_list = list(itertools.chain(*nested_list))
      ```
   - [Monoid](https://stackoverflow.com/a/952946/4892892)
      ```python
      flat_list = sum(nested_list, [])
- [Slice assignment](https://stackoverflow.com/questions/32448414/what-does-colon-at-assignment-for-list-do-in-python?)
   
   ```python
   
   ```
- [Using the `else` clause in `for` and `while` loops](https://stackoverflow.com/questions/9979970/why-does-python-use-else-after-for-and-while-loops)
- [Function arguments](https://www.blog.pythonlibrary.org/2022/06/28/python-101-an-intro-to-functions)

   As of Python 3.8, [positional-only arguments](https://peps.python.org/pep-0570/) are supported. These arguments cannot by passed as keywords.
   The forward slash, /, indicates to Python that all arguments before the forward-slash are positional-only arguments. Anything following the forward slash are positional or keyword arguments up to the *. The asterisk indicates that everything following it are keyword-only arguments.
   For instance, calling the function
   ```python
   def positional(name, age, /, a, b, *, key):
       pass
   ```
   Here are some invalid calls to this function:
   ```python
   >>> positional(name='Mike')
   TypeError: positional() got some positional-only arguments passed as keyword arguments: 'name'
   >>> positional('Mike', 17, 2, b=3)
   TypeError: positional() missing 1 required keyword-only argument: 'key'
   >>> positional('Mike', 17, 2, 3, 'test')
   TypeError: positional() takes 4 positional arguments but 5 were given
   >>> positional('Mike', 17, 2, b=3, keyword='test')
   TypeError: positional() got an unexpected keyword argument 'keyword'
   ```
   Some valid function calls are
   ```python
   positional('Mike', 17, 2, 3, key='test')
   positional('Mike', 17, 2, b=3, key='test')
   ```


### File handling

- [Append text file in the middle](https://stackoverflow.com/questions/10507230/insert-line-at-middle-of-file-with-python)

### Conventions

A major design priciple behind Python was that code should be easily read. Conventions greatly improve the readability of your code, making it ''Pythonic''.



## Packaging  

The directory structure of a Python project should be created so that it is easily testable, deployable and put under continuous integration. Some links I found useful:

- https://github.com/yngvem/python-project-structure
- https://www.kennethreitz.org/essays/repository-structure-and-python
- https://hynek.me/articles/testing-packaging/



## NumPy

- [NumPy version](https://stackoverflow.com/a/1520264/4892892)
   ```python
   import numpy
   print numpy.__version__
   ```
   or from the command line:
   ```python
   python -c 'import numpy; print(numpy.__version__)'
   ```
- Print information about the CPU
   ```python
   import numpy.distutils.cpuinfo.cpu
   cpu.info()
   ```
- Figure out which BLAS and LAPACK implementations are used by your NumPy (and therefore SciPy, etc.)
   ```python
   import numpy.distutils.system_info
   get_info('blas_opt')
   get_info('lapack_opt')
   ```
   [Here](https://github.com/numpy/numpy/blob/v1.19.0/numpy/distutils/system_info.py#L401-L485) is the list of all options for `get_info`.



## Best practices

- [How to order methods in a class?](https://stackoverflow.com/questions/10289461/what-is-a-good-way-to-order-methods-in-a-python-class)



## Visualization

### Plotting with Matplotlib

Browse the extensive [gallery](https://matplotlib.org/3.1.1/gallery/index.html) for examples, read the [User's Guide](https://matplotlib.org/3.1.1/contents.html), or check the [tutorials](https://matplotlib.org/3.1.1/tutorials/index.html).
Two types of plotting:
- pyplot: high-level MATLAB-like plotting for simple interactive plotting
   - [tutorial](https://matplotlib.org/3.1.1/tutorials/introductory/pyplot.html)
   - [gallery](https://matplotlib.org/3.1.1/gallery/index.html#pyplots-examples)
   - [API](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.html)
- object-oriented API
   - [gallery](https://matplotlib.org/3.1.1/gallery/index.html)
 
Links to APIs I often use:
- [Figure class](https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.figure.Figure.html)
- [axes module](https://matplotlib.org/3.2.1/api/axes_api.html)

[Positioning the legend](https://matplotlib.org/3.2.2/api/_as_gen/matplotlib.axes.Axes.legend.html#matplotlib.axes.Axes.legendhttps://matplotlib.org/3.2.2/api/_as_gen/matplotlib.axes.Axes.legend.html#matplotlib.axes.Axes.legend)


### Class hierarchy

If you install Pylint, it comes with [Pyreverse](https://www.logilab.org/blogentry/6883). Type
```python
pyreverse -o <output_format> <module_name>
```
to the terminal to save the class hierarchy fetched from the module `<module_name>` in `<output_format>` (`png`, `svg`, `eps`, `pdf`, `dot`, etc.). Note that `module_name` must be importable. If `module_name` is a package that contains other packages or modules, all the contents of the package will be parsed. To select a subpackage or a module, use the slash; e.g. to process only *f2py* from *numpy*, use
```python
pyreverse -o png numpy/f2py
```
It is often useful for the end user to ignore the tests. You can ignore a directory by giving the `--ignore` flag. In the example above:
```python
pyreverse -o png --ignore tests numpy/f2py
```
For further options, check the documentation:
```python
pyreverse --help
```


## GUIs

- view *pandas* DataFrame objects

  [PandasDataFrameGUI](https://github.com/bluenote10/PandasDataFrameGUI) supports useful data analysis (filtering, sorting, plotting, etc.) and has few dependencies. A common mistake is that your code already imported *matplotlib*, which selected a backend other than `'WXAgg'`. The solution is to load *matplotlib* **before** you use your own code, with
  ```python
  import matplotlib
  matplotlib.use('WXAgg')
  ```
  as shown [here](https://github.com/bluenote10/PandasDataFrameGUI/issues/3#issuecomment-324940242).
  
  
  ## Online
  
  ### Binder
  
  - [Generate custom badges](https://mybinder.readthedocs.io/en/latest/howto/badges.html#generate-custom-launch-badges-for-your-binder-repository): the link you need to insert comes from [MyBinder](https://mybinder.org/).
