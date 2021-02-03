# Makefile mostly derived from: https://spin.atomicobject.com/2016/08/26/makefile-c-projects/
#
# (c) Peter Harrison Feb 2021
#
# these have defaults that should work but it is good to be explicit
CC = gcc
CXX= g++
RM = rm -f

# the final executable name
PROJECT_NAME=hello_dorothy

# the sources live in these folders
SRC_DIR=src
INC_DIR=inc

# describe the files to be built by doing a simple search
SRC_FILES = $(shell find $(SRC_DIR) -name *.cpp -or -name *.c -or -name *.s)
INC_DIRS = $(shell find $(INC_DIR) -type d)

# common flags used by both compilers. cpflags is meant for the preprocessor really.
# The -MMD flags additionaly create a .d file with the same name as the .o file.
CPPFLAGS = -Wall -Werror -Wextra -pedantic \
					-ffunction-sections \
	        -fdata-sections\
					-MMD -MP\
					$(addprefix -I,$(INC_DIRS))
# C language specific flags
CFLAGS = -std=gnu99
# C++ language specific flags
CXXFLAGS = -std=gnu++17
# Assembler specific flags
ASFLAGS=
# Linker flags if you need additional libraries
LDFLAGS=

# The first target is the default and will build the binary image
all: project
.PHONY: all

##############################################
#
# Build settings
#
PROJECT = $(BUILD_DIR)/$(PROJECT_NAME)
BUILD_DIR = ./build
# all the source files generate a .o file under the build directory with a corresponding path
OBJECTS = $(SRC_FILES:%=$(BUILD_DIR)/%.o)
# set the level of optimisation needed
OPT_FLAGS = -g -Og

# Gcc/Clang will automatically create the .d files containing dependencies.
DEP = $(OBJECTS:%.o=%.d)

#include the dep files
-include $(DEP)

project: $(PROJECT)
.PHONY: project

$(PROJECT) : $(OBJECTS)
	$(CXX) $(LDFLAGS) $^ -o $@

# How to build each file type. Explicit rules for clarity and flexibility.
# The potential dependency on header files is covered by having called `-include $(DEP)`.

# assembly
$(BUILD_DIR)/%.s.o: %.s
	@mkdir -p $(dir $@)
	$(AS) $(ASFLAGS) -c $< -o $@

# c source
$(BUILD_DIR)/%.c.o : %.c
	@mkdir -p $(dir $@)
	$(CC) $(CPPFLAGS) $(OPT_FLAGS) $(CFLAGS) -c $< -o $@

# c++ source
$(BUILD_DIR)/%.cpp.o : %.cpp
	@mkdir -p $(dir $@)
	$(CXX) $(CPPFLAGS) $(OPT_FLAGS) $(CXXFLAGS) -c $< -o $@

clean:
	@echo CLEANING...
	$(RM) $(BUILD_DIR)/$(TARGET_NAME) $(OBJECTS)
	$(RM) $(DEP)
	@echo
.PHONY: clean

rebuild: clean target
.PHONY: rebuild

run: target
	@echo
	@echo $(PROJECT)
	@echo
	@$(PROJECT)
	@echo
.PHONY: run

info:
	@echo CC: $(CC)
	@echo CXX: $(CXX)
	@echo RM: $(RM)
	@echo TARGET_NAME: $(PROJECT_NAME)
	@echo SRC_FILES: $(SRC_FILES)
	@echo INC_DIRS: $(INC_DIRS)
	@echo BUILD_DIR: $(BUILD_DIR)
	@echo OBJECTS: $(OBJECTS)
	@echo DEPS: $(DEP)
	@echo CFLAGS: $(CFLAGS)
	@echo CXXFLAGS: $(CXXFLAGS)
	@echo CPPFLAGS: $(CPPFLAGS)
	@echo OPT_FLAGS: $(OPT_FLAGS)
	@echo ASFLAGS: $(ASFLAGS)
	@echo LDFLAGS: $(LDFLAGS)
.PHONY: info
