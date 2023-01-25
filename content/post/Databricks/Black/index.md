---
title: Databricks + Black
summary: An introduction to using Black with Databricks
tags:
  - Intro
  - Databricks
date: 2023-01-25
ShowToc: true
UseHugoToc: true
TocOpen: true
draft: false

image:
  filename: featured
  focal_point: Smart
  preview_only: false
weight: 10

---



## Databricks + Black = Magic
Databricks now have the support of Black - a python code formatter (**In Public Preview**)

Black is preinstalled on clusters using Runtime >= 11.2, for older version run  `%pip install black==22.3.0 tokenize-rt==4.2.1` to install necessary libraries

You can access Black within your notebook by presssing `ctr + shift + f` or by going to `Edit -> Format cell(s)`


```python
# Example unformatted

def is_unique(
               s
               ):
    s = list(s
                )
    s.sort()
 
 
    for i in range(len(s) - 1):
        if s[i] == s[i + 1]:
            return 0
    else:
        return 1

```


```python
# Example formatted using Black

def is_unique(s):
    s = list(s)
    s.sort()

    for i in range(len(s) - 1):
        if s[i] == s[i + 1]:
            return 0
    else:
        return 1
```

Using Databricks built-in Black support allows the developer to adopt to the PEP8 standard. Keeping your code well-fromatted, clean and readable. 

To quote Black's README:

> Black is the uncompromising Python code formatter. By using it, you agree to cede control over minutiae of hand-formatting. In return, Black gives you speed, determinism, and freedom from pycodestyle nagging about formatting. You will save time and mental energy for more important matters. 

Black: [Gtihub](https://github.com/psf/black)  
Databricks: [Docs](https://docs.databricks.com/notebooks/notebooks-code.html#format-python-cells)

