# rabbitmq-example
Using FetchContent module from CMake to download and build the rabbitmq-c wrapper for the rabbitmq library.

Rabbitmq-c wrapper here: https://github.com/alanxz/rabbitmq-c

Understanding CMake and how the FetchContent module works:
Cmake useful tutorials:
* http://www.saoe.net/blog/using-cmake-with-external-projects/
* https://pabloariasal.github.io/2018/02/19/its-time-to-do-cmake-right/
* https://cmake.org/cmake/help/git-stage/guide/importing-exporting/index.html
* http://cmake.3232098.n2.nabble.com/How-to-link-against-projects-added-through-FetchContent-td7597224.html

```
cd rabbitmq-example
cmake -Bbuild
cmake --build build
```

Note: overriding default options. Building and linking only `rabbitmq-static`.

