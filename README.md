# single-file modules

Central repository for single-file python modules (SFM) with useful stuff i've had to do in various projects. The idea is that, while you might not want to take up more pip dependencies, you still don't want to write all the code for some things from scratch, and want a somewhat version-controlled version of it.


- [compare_json](https://github.com/lczyk/compare_json)
- [environ_get](https://github.com/lczyk/environ_get)
- [geturl](https://github.com/lczyk/geturl)
- [kv](https://github.com/lczyk/kv)
- [type_conversion_dict](https://github.com/lczyk/type_conversion_dict)
- [unwrap_type](https://github.com/lczyk/unwrap_type)
- [xpc](https://github.com/lczyk/xpc)


While not directly inspired by Sean Barretts [stb](https://github.com/nothings/stb) libraries, now that i think about it there are a lot of similarities in approach / motivation.

## Spec

- Each SFM comes in a single file (duh) and includes everything it might possibly need in it. This includes `__version__`, `__doc__`, `__author__` or `__authors__` in the case of multiple authors. Each SFM ought to also include `__changelog__`.
- Each SFM which is a library of functions to be imported ought to include the `__all__` variable to facilitate `*` import and clearly mark which functions are private (preceded with an underscore) or public.
- Each SFM depends *only* on python standard library. Exceptions are:
    - SFMs which *explicitly* depend on a *small number* of external packages to do their core job. For example an SFM which does something using `joblib`. This SFM ought to have `joblib` in its name to indicate that that is the dependency.
    - Optional dependencies which are checked at runtime and, if not present, don't prevent the SFM form performing it's core functionality. For example optionally imported `colorlog` in [xpc](https://github.com/lczyk/xpc).
- Each SFM is tested for all current versions of python. If there is no good need to stop supporting an old version (e.g. major syntax changes, type-checker or runtime incompatibility with newer version, excessive hacks or external dependencies needed for it to work ), that version will keep being supported. 
- The primary use pattern of a SFM is to just vendor it -- just copy it to wherever you need it. If you want a newer version, you're the package manager.
- The use of double underscore prefix (e.g. `__variable`) in non-python functions (aka. `__init__` or `__call__` are obviously ok) is heavily discouraged. While functions/variables can be marked as private with single underscore, python applies some additional name mangling to `__` names which makes them less accessible to the user. This goes against the spirit of SFMs.
- Majority of the checks ought to be done in tests. We don't mind having fat tests. We do want to keep the SDFs themselves clean and small.

## Install

Just copy the single-module file to your project and import it.

```bash
cp ./src/<NAME>/<NAME>.py src/your_package/_<NAME>.py
```

Or even better, without checking out the repository:

```bash
curl https://raw.githubusercontent.com/lczyk/<NAME>/main/src/<NAME>/<NAME>.py > src/your_package/_type_conversion_dict.py
```

Note that like this *you take stewardship of the code* and you are responsible for keeping it up-to-date. If you change it that's fine (keep the license pls). That's the point here. You can also copy the code to your project and modify it as you wish.

If you want you can also build and install it as a package, but then the source lives somewhere else. That might be what you want though. 🤷‍♀️

```bash
pip install flit
flit build
ls dist/*
pip install dist/*.whl
```
