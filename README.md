# Compiler and flags
CC = gcc
CFLAGS = -Wall -Werror -Iinclude

# Directories
SRC_DIR = src
INCLUDE_DIR = include
BUILD_DIR = build

# Files related to Standard Types, Bit Math, and Documentation
STANDARD_TYPES_SRC = $(SRC_DIR)/standard_types.c
BIT_MATH_SRC = $(SRC_DIR)/bit_math.c
DOCUMENTATION_SRC = $(SRC_DIR)/documentation.c

# Object files
OBJS = $(BUILD_DIR)/standard_types.o $(BUILD_DIR)/bit_math.o $(BUILD_DIR)/documentation.o

# Output executable
TARGET = embedded_system_app

# Rules
all: $(TARGET)

$(TARGET): $(OBJS)
	$(CC) $(CFLAGS) -o $@ $^

$(BUILD_DIR)/%.o: $(SRC_DIR)/%.c | $(BUILD_DIR)
	$(CC) $(CFLAGS) -c $< -o $@

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

# Clean rule
clean:
	rm -rf $(BUILD_DIR) $(TARGET)

# Phony targets
.PHONY: all clean
