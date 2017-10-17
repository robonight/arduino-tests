# robonight

```sh
pushd arduino-tests && docker build --tag arduino-test .  && popd 

pushd arduino-gmock-sample && docker run -it -v $(pwd):/arduino/project arduino-test && popd
```
