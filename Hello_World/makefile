PROJECT_NAME        := main



CC := arm-linux-gnueabihf-g++
LD := arm-linux-gnueabihf-ld

HOST_CC := g++

#include "lcd.h"
CFLAGS := -Wall -Wextra

PROJECT_DIR = $(shell pwd)

# PROJECT_DIR =.

OUT_DIR :=$(PROJECT_DIR)/out

#Create an Variable to store all include directories
INCLUDE_DIRS =$(PROJECT_DIR)/inc

# Include files 
INCLUDE_FILES =$(foreach DIR, $(INCLUDE_DIRS), $(wildcard $(DIR)/*.h ))

#Create an Variable to store all source directories
SRC_DIRS = $(PROJECT_DIR)/src

# SOURCES files
SRC_FILES =$(foreach DIR, $(SRC_DIRS), $(wildcard $(DIR)/*.cpp))

# OBJECTS files
OBJECT_FILES =$(addprefix $(OUT_DIR)/, $(notdir $(patsubst %.cpp, %.o, $(SRC_FILES))))


INC_DIR_OPT :=$(foreach DIR,$(INCLUDE_DIRS),-I$(DIR))


CCOPT :=$(INC_DIR_OPT)

vpath %.cpp  $(SRC_DIRS)
vpath %.h  $(INCLUDE_DIRS)

$(OUT_DIR)/%.o: %.cpp $(INCLUDE_FILES)
	$(CC) $(CCOPT) $(CFLAGS) -c $< -o $@

HOST_OUT_DIR := $(OUT_DIR)

$(HOST_OUT_DIR)/%.o: %.cpp $(INCLUDE_FILES)
	$(HOST_CC) $(CCOPT) $(CFLAGS) -c $< -o $@

TARGET := $(PROJECT_NAME)

$(TARGET): $(OBJECT_FILES)
	$(CC) $(CFLAGS)  $^ -o $(OUT_DIR)/$@

HOST_TG := $(PROJECT_NAME)

$(HOST_TG): $(OBJECT_FILES)
	$(HOST_CC) $^ -Wall -Wextra -g -o $(HOST_OUT_DIR)/$@ -B $(SRC_FILES)

.PHONY:
build: create  $(TARGET)
	@echo Build successfully!

.PHONY:
# host: create $(HOST_TG)
	# @echo Build successfully

.PHONY:
create:
	 mkdir $(OUT_DIR)


clean:
	rm -r $(OUT_DIR)

.PHONY:
print-%:
	@echo $($(subst print-,,$@))

