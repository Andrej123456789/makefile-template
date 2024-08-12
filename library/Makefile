# Directory of include files
INCLUDE_DIR ?= "include"

# Compiler and compiler flags
CC = gcc
CFLAGS = -fno-stack-protector -ffreestanding -Wall -Wextra -g -I$(INCLUDE_DIR)

# Folder for object libraries and compiled library
OBJ = obj
OBJDIR = $(OBJ)/objects
BIN = $(OBJ)/library.a

# Source files
SRC = $(wildcard *.c)
SRC_2 = $(wildcard src/*.c)

OBJS = $(addprefix $(OBJDIR)/, $(patsubst %.c, %.o, $(SRC)))
OBJS += $(addprefix $(OBJDIR)/, $(patsubst src/%.c, %.o, $(SRC_2)))

# Path where to install library
LIB_DIR ?= /usr/local/lib
INCLUDE_INSTALL_DIR ?= /usr/local/include/library

.PHONY: all
all: $(OBJ) $(OBJDIR) $(BINFOLDER) $(BIN)

$(OBJ):
	mkdir -p $(OBJ)

$(OBJDIR):
	mkdir -p $(OBJDIR)

$(BINFOLDER):
	mkdir -p $(BINFOLDER)

$(BIN): $(OBJS)
	ar -r $(BIN) $^

$(OBJDIR)/%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

$(OBJDIR)/%.o: src/%.c
	$(CC) $(CFLAGS) -c $< -o $@

.PHONY: clean
clean:
	rm -rf $(OBJ)

install: $(BIN)
	@echo "====> Installing library.a to $(LIB_DIR)"
	install -d $(LIB_DIR)
	install $(BIN) $(LIB_DIR)/liblibrary.a
	@echo "====> Installing headers to $(INCLUDE_INSTALL_DIR)"
	install -d $(INCLUDE_INSTALL_DIR)
	rsync -a $(INCLUDE_DIR)/ $(INCLUDE_INSTALL_DIR)/
	@echo "====> Configuring GCC"
	echo $(LIB_DIR) | sudo tee /etc/ld.so.conf.d/freelibc.conf
	sudo ldconfig
