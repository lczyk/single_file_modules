# single-file modules

Central repository for single-file python modules with useful stuff i've had to do in varous projects. The idea is that, while you might not want to take up more pip dependencies, you still don't want to write all the code for some things from scratch, and want a somewhat version-controlled version of it.


- [compare_json](https://github.com/lczyk/compare_json)
- [environ_get](https://github.com/lczyk/environ_get)
- [geturl](https://github.com/lczyk/geturl)
- [kv](https://github.com/lczyk/kv)
- [type_conversion_dict](https://github.com/lczyk/type_conversion_dict)
- [unwrap_type](https://github.com/lczyk/unwrap_type)
- [xpc](https://github.com/lczyk/xpc)


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
