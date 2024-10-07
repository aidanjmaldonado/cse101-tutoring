CC=clang
CFLAGS=-Wall -Wextra -Werror -std=c11 -pedantic

.PHONY: all
all: test test.c

%.o : %.c %.h
	$(CC) $(CFLAGS) $< -c

.PHONY: clean
clean:
	-rm test

.PHONY: format
format:
	clang-format -i *.c *.h

.PHONY: check-format
check-format:
	clang-format --dry-run --Werror *.c *.h
