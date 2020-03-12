# python_learningresources
Links to books, repositories, blogs and videos about useful Python resources

## GUIs

- view *pandas* DataFrame objects

  [PandasDataFrameGUI](https://github.com/bluenote10/PandasDataFrameGUI) supports useful data analysis (filtering, sorting, plotting, etc.) and has few dependencies. A common mistake is that your code already imported *matplotlib*, which selected a backend other than `'WXAgg'`. The solution is to load *matplotlib* **before** you use your own code, with
  ```python
  import matplotlib
  matplotlib.use('WXAgg')
  ```
  as shown [here](https://github.com/bluenote10/PandasDataFrameGUI/issues/3#issuecomment-324940242).
