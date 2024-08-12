CC = gcc
CFLAGS = -Wall -Wextra -pedantic -g -llibrary

OBJ = obj

OBJDIR = $(OBJ)/objects
OBJS = $(addprefix $(OBJDIR)/, $(patsubst %.c, %.o, $(wildcard *.c)))
OBJS += $(addprefix $(OBJDIR)/, $(patsubst src/%.c, %.o, $(wildcard src/*.c)))

BINFOLDER = $(OBJ)/executable
BIN = $(BINFOLDER)/program

.PHONY: all
all : $(OBJ) $(OBJDIR) $(BINFOLDER) $(BIN)

$(OBJ):
	mkdir $(OBJ)

$(OBJDIR):
	mkdir $(OBJDIR)

$(BINFOLDER):
	mkdir $(BINFOLDER)

$(BIN) : $(OBJS)
	$(CC) $(OBJS) -o $(BIN) $(CFLAGS)

$(OBJDIR)/%.o : src/%.c
	$(CC) $(CFLAGS) -c $< -o $@

$(OBJDIR)/%.o : %.c
	$(CC) $(CFLAGS) -c $< -o $@

.PHONY: run
run:
	@./$(BIN)

.PHONY: clean
clean:
	rm -rf $(OBJ)
