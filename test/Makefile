CFLAGS		+= -std=gnu99 -Wall -Wextra -g \
		   -D_GNU_SOURCE \
		   -Wno-unused-parameter \
		   -Wmaybe-uninitialized \
		   -Wredundant-decls \
		   -Wcast-align \
		   -Wsign-compare \
		   -Wno-missing-field-initializers
TEST_COMMON	:= kdbus-enum.o kdbus-util.o
CC		:= $(CROSS_COMPILE)gcc

TESTS= \
	test-kdbus \
	test-kdbus-daemon \
	test-kdbus-fuzz \
	test-kdbus-benchmark \
	test-kdbus-activator \
	test-kdbus-monitor \
	test-kdbus-chat

all: $(TESTS)

%.o: %.c ../kdbus.h
	@echo '  TARGET_CC $@'
	@$(CC) $(CFLAGS) -DKBUILD_MODNAME=\"$(KBUILD_MODNAME)\" -c $< -o $@

test-%: $(TEST_COMMON) test-%.o
	@echo '  TARGET_LD $@'
	@$(CC) $(CFLAGS) $^ -o $@

clean::
	rm -f *.o $(TESTS)
