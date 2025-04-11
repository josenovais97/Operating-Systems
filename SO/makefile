# Makefile

CC = gcc
CFLAGS = -Wall -Wextra

all: sort stats report

sort: sort.c
	$(CC) $(CFLAGS) -o sort sort.c

stats: stats.c
	$(CC) $(CFLAGS) -o stats stats.c

report: report.c
	$(CC) $(CFLAGS) -o report report.c

clean:
	rm -f sort stats report

