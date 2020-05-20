---
title: Typing a sentinel argument with typeshed and mypy
date: 2020-05-20
---

While writing code for my [Weave](https://github.com/razzius/weave) project, I encountered a type error when adding a command line interface to my Flask application:

```sh
$ mypy --ignore-missing-imports --follow-imports=silent server/cli.py
server/cli.py:11: error: Unexpected keyword argument "cli_group" for "Blueprint"
```

The offending code:

```python
from flask import Blueprint

blueprint = Blueprint("cli", __name__, cli_group=None)
```

The new `cli_group` argument had not been added to the stub library, [typeshed](https://github.com/python/typeshed).

The function declaration source code is:

```python
# a singleton sentinel value for parameter defaults
_sentinel = object()

class Blueprint(_PackageBoundObject):

    def __init__(
        self,
        <arguments>,
        cli_group=_sentinel,
    ):
```

Blueprint uses a sentinel as a default argument to know when the user explicitly passes `None`, as I did.

Users will never pass the sentinel explicitly, but we still need to include that type. Sentinel is an `object` instance, but so is everything else, so typing it as `Union[Optional[str], object]` is no different than just typing it as `object`. The solution:

class _Sentinel(object): ...

def __init__(self, <arguments>, cli_group: Union[Optional[str], _Sentinel] = ...) -> None: ...

Note that the ellipsis are actually in the stub code as a literal, so I used <arguments> as a placeholder.
Importing this into my code base

The [pull request made it in to typeshed relatively quickly](https://github.com/python/typeshed/pull/4011), but even when I installed the master branch of mypy, the error still persisted in my code. This is because mypy uses a submodule of typeshed. The solution is to fork mypy and update typeshed there. If my changes hadn't been merged into typeshed yet, I could fork that as well.

```sh
# Using clone-cd from my fish functions to cd automatically
# (https://github.com/razzius/fish-functions#clone-cd-url-destination-source)
clone-cd https://github.com/python/mypy
# Go into typeshed submodule
cd mypy/typeshed
git pull
# Back out to mypy
cd ..
git commit -am 'Update mypy/typeshed'
# Create a fork
hub fork
git push razzius
```

Now to incorporate my fork into my project using Pipenv:

```sh
pipenv install --dev -e git+https://github.com/razzius/mypy.git#egg=mypy
```

At some point, typeshed will be updated in mypy and mypy will release a new edition, and I can go back to the mainline then.

```sh
$ mypy --ignore-missing-imports --follow-imports=silent server/cli.py
```
```
Success: no issues found in 1 source file
```
