# Python style guide

## Introduction

This guide documents coding and style conventions for contributing to FragileTech Python projects.
 
## Code Style

1. Contributing to existing external projects - do not change the style.
2. Follow the [Python Style guide](https://docs.python-guide.org/writing/style/).
3. Use [PEP8](https://www.python.org/dev/peps/pep-0008/) with 99 char line length limit.
4. Class methods order: 
    1. `__init__`
    2. Attributes
    3. Static methods
    4. Class methods 
    5. Public methods
    6. Protected (`_`) methods
    7. Private (`__`) methods
5. Use double quotes `"`. When a string contains single or double quote characters, however, use the other one to avoid
 backslashes in the string.
6. Favor [f-strings](https://realpython.com/python-string-formatting/#3-string-interpolation-f-strings-python-36) 
when printing variables inside a string.
7. Do not use single letter argument names; use X and Y only in Scikit-learn context.
9. Use [Google style](https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html) for docstrings.
10. Format of TODO and FIXME: `# TODO(mygithubuser): blah-blah-blah`.
11. Add [Type hinting](https://docs.python.org/3/library/typing.html) when possible.
12. Use standard [argparse](https://docs.python.org/3/library/argparse.html) for CLI interactions. 
[Click](https://click.palletsprojects.com/en/7.x/arguments/) is also allowed when it improves the readability and maintainability of the code.


## Useful tips

1. **Each function should do only one thing**. If you find yourself writing a long function that does a lot of stuff, consider
splitting it into different functions.

2. **Give variables a meaningful name**. If names became too long, use abbreviations. This abbreviations should be explained
in comments when defining the variable for the first time.

3. Keep in mind that coding is creating abstractions that hide complexity. This means that you should be able to get an
idea of what a function does just by reading its documentation.   

4. **Avoid meaningless comments**. Assume the person who is reading your code already know how to code in python, and take
advantage of the syntax of the language to avoid using comments. For example, a comment is welcome when it can save you
reading several lines of code that do stuff which is difficult to understand. 

5. **Document the functions**, and make sure that it is easy to understand what all the parameters are. When working with tensors
and vectors, specify its dimensions when they are not obvious.

6. **Follow the [Zen of Python](https://www.python.org/dev/peps/pep-0020/)**, it is your best friend.

7. A well documented function lets you know what it does and how to use it without having to take a look at its code.
**Document all the functions**! It is a pain in the ass but it pays off.

## Code formatting

- We use [`black`](https://black.readthedocs.io/en/stable/change_log.html) for formatting the code. 
Run `black .` before committing to automatically format the code in a consistent way.

### Separating blocks of code with blank lines

Although using blank lines to separate code 
blocks may seem like a good idea, it has the following drawbacks:
- It does not offer any information regarding how and why you are defining different blocks of code.
- It makes code reviews more difficult: 
    * It forces the reviewer to make assumptions about why you decided to create the different blocks.
    * It removes context when showing possible suggestions about changes in the code.
    * Sparse code makes adds unnecessary scrolling time when reading the code.
    * Sparse code makes the code diffs less reliable.
    
If you want to separate different code blocks inside the same function there are better alternatives:
- **Write a comment** explaining what the code block you are defining with a blank line matters:
    * It helps the reviewer understand why you are separating different code blocks.
    * If the comment is meaningless you'll realize that it was an unnecessary line break.
    For example, imagine you are defining a fancy neural network as a `pytorch.nn.Module`:
    ```python
    super().__init__()
  
    self.device = device
  
    self.layer_1 = torch.nn.Linear(in_dim, out_dim)
    self.layer_2 = torch.nn.Linear(out_dim, out_dim)
  
    self.layer_3 = torch.nn.Linear(in_dim, out_dim)
    self.layer_4 = torch.nn.Linear(out_dim, in_dim)
    ```
    To understand if the blank lines you wrote to separate different code blocks are useful,
     you could write a comment to separate the different blocks:
    ```python
    super().__init__()
    # Device definition
    self.device = device
    # Encoder layers of my fancy DNN model
    self.layer_1 = torch.nn.Linear(in_dim, out_dim)
    self.layer_2 = torch.nn.Linear(out_dim, out_dim)
    # Decoder layers of my fancy DNN model
    self.layer_3 = torch.nn.Linear(in_dim, out_dim)
    self.layer_4 = torch.nn.Linear(out_dim, out_dim)
    ```
   When you do that you will realize that you almost spent more time reading the comments than the
    code blocks that they separate, and that the "device" comment you wrote is extremely obvious for anyone that
    is remotely familiar with `pytorch`. In that case, deleting taht blank line improves the 
    readability of your code.
     
    The comments about the blocks of your fancy neural network are indeed adding 
    some useful information, but there may be a better alternative. 
    Those comments are useful because they give information about what each layer is doing, 
    but this is something that could be improved by finding meaningful names to the defined layers.
     
   ```python
    super().__init__()
    self.device = device
    self.encoder_in = torch.nn.Linear(in_dim, out_dim)
    self.encoder_out = torch.nn.Linear(out_dim, out_dim)
    self.decoder_in = torch.nn.Linear(in_dim, out_dim)
    self.decoder_out = torch.nn.Linear(out_dim, out_dim)
   ```
  Now that the names are meaningful and there are no comments, we find that the different line length between
  `self.device` and `self.encoder_in = torch.nn.Linear(in_dim, out_dim)` makes it easier 
  to differentiate those two blocks. On the other hand `encoder` and `decoder` have the same length, 
  and that makes it difficult to spot quickly when the definition of the decoder starts. 
  Adding a comment between the two of them will improve the readability of the code:
  
  ```python
    super().__init__()
    self.device = device
    self.encoder_in = torch.nn.Linear(in_dim, out_dim)
    self.encoder_out = torch.nn.Linear(out_dim, out_dim)
    # Decoder layers of my fancy DNN model
    self.decoder_in = torch.nn.Linear(in_dim, out_dim)
    self.decoder_out = torch.nn.Linear(out_dim, out_dim)
   ```
  Keeping the comment about de encoder is not worth it in this case because its commenting a block of only
  two lines of code, but if the encoder had more layers it could be useful to make the code 
  more readable. Inside the `__init__` function, try to not add more than 1 comment per 5 lines of code.
    
- **Write a new function** to encapsulate the new code block:
    * It will reduce the cognitive load of the reviewer by abstracting the complexity of the code.
    * The function call will remove the need of additional comments.
    * It will make testing easier.
    
- **Use reserved words** in variable definitions and function calls to separate code blocks:
    Take advantage of the different color highlighting that reserved words have to make an implicit separation of blocks.
     For example, instead of:
    ```python
    my_var = do_one_thing(param_1=val_1, param_2=val_2, param_3=value_3)
    
    another_var = do_another_thing(my_var)
    return another_var
    ```
    You could do:
    ```python
    my_var = my_object.do_one_thing(param_1=val_1, param_2=val_2, param_3=value_3)
    return do_another_thing(my_var)
    ``` 

## Pycharm tips

1. Using [PyCharm](https://www.jetbrains.com/pycharm/download/#section=linux) as an IDE will help you highlight the most
 common mistakes amd help you enforce PEP8.


## Example codebase

Reading well-written Python code is also a way to improve your skills. Please avoid copying anything that has been written
by a researcher; it will likely be a compendium of bad practices. Instead, take a look at any of the following projects:

- [Django](https://github.com/django/django)

- [Flask](https://github.com/pallets/flask)

- [Jinja 2](https://github.com/pallets/jinja)

When it comes to Reinforcement Learning, please avoid at any cost using OpenAI baselines as an example.


## Resources

- **The Zen of Python in examples**: 
    - [Post in Medium](https://medium.com/@Pythonidaer/a-brief-analysis-of-the-zen-of-python-2bfd3b76edbf)
    - [Quora post](https://www.quora.com/What-do-different-aphorisms-in-The-Zen-of-Python-mean)
    - [Code example](https://gist.github.com/evandrix/2030615)
    
- **Idiomatic Python**:
    - Blog post about [Idiomatic Python](https://medium.com/the-andela-way/idiomatic-python-coding-the-smart-way-cc560fa5f1d6)    
    - [More Python Idioms](http://prooffreaderplus.blogspot.com/2014/11/top-10-python-idioms-i-wished-id.html)
