INCLUDE_DIR ?= "include"

CC = gcc
CFLAGS = -g -I$(INCLUDE_DIR) -llibrary

OBJ = obj

OBJDIR = $(OBJ)/objects
OBJS = $(addprefix $(OBJDIR)/, $(patsubst %.c, %.o, $(wildcard *.c)))
OBJS += $(addprefix $(OBJDIR)/, $(patsubst src/%.c, %.o, $(wildcard src/*.c)))

BINFOLDER = $(OBJ)
BIN = $(BINFOLDER)/test

.PHONY: all
all : $(OBJ) $(OBJDIR) $(BIN)

$(OBJ):
	mkdir $(OBJ)

$(OBJDIR):
	mkdir $(OBJDIR)

$(BIN) : $(OBJS)
	$(CC) $(OBJS) -o $(BIN) $(CFLAGS)

$(OBJDIR)/%.o : %.c
	$(CC) $(CFLAGS) -c $< -o $@

$(OBJDIR)/%.o : src/%.c
	$(CC) $(CFLAGS) -c $< -o $@

.PHONY: run
run:
	@./$(BIN)

.PHONY: clean
clean:
	rm -rf $(OBJ)
