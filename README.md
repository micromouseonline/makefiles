# Makefile project examples

Here are some sample makefile projects that can be used as templates. Mostly, this is about me learning how to use makefiles so do not expect excellence or even anything that works for you. They are probably worth exactly what you are paying for them.

* ***generic makefile*** is for building a simple project on the desktop. It will build a mixed C/C++ project with the files in two directories - ```src``` and ```inc```. The project name is assigned to the variable ```PROJECT_NAME```.  This is a prety simple Makefile and is most likely quite naive. There are some simple C and C++ source files to make a basic project. The Makefle are a number of targets:

    * ```all```: is the default target and makes the ```project``` target. It is there in case the default behaviour should be more than just a simple build..

    * ```project```: builds the complete project in a subdirectory called ```build```. All the object and dependency files are geerated in the ```build``` directory in a directory structure that replicates that of the sources. The project executable is named from the ```PROJECT_NAME``` variable. Which seems reasonable.

    * ```clean```: removes all the object files and dependency files from the ```build``` directory as well as the generated executable.

    * ```rebuild```: is equivalent to running ```make clean; make``` and forces a complete rebuild of all components.

    * ```run```: will build the project and then attempt to execute the generated binary. Just for the lazy.

    * ```info```: simply lists some important Makefile variables for testing. Included will be a list of the source and object files. This could get big in a more complex project. There is probably a way to do this with ```make``` but this seems more tailored to the needs of a particular project. Handy when modifying and testing the Makefile.

More samples may follow one day.

