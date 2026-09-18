CC = mpicc
CFLAGS = -O3 -Wall
NP ?= 4
HOSTFILE ?= /shared/hosts

# Relative executable paths in sibling exercise directories
EX1 = ../Exercise01/sum_bcast
EX2 = ../Exercise02/sum_scatter
EX3 = ../Exercise03/sum_gather
EX4 = ../Exercise04/sum_reduce
EX5 = ../Exercise05/sum_allreduce
EX6 = ../Exercise06/sum_scan

TARGETS = $(EX1) $(EX2) $(EX3) $(EX4) $(EX5) $(EX6)

.PHONY: all clean run-local run-cluster help

# Default: compile all 6 programs
all: $(TARGETS)

../Exercise01/%: ../Exercise01/%.c
	$(CC) $(CFLAGS) -o $@ $<

../Exercise02/%: ../Exercise02/%.c
	$(CC) $(CFLAGS) -o $@ $<

../Exercise03/%: ../Exercise03/%.c
	$(CC) $(CFLAGS) -o $@ $<

../Exercise04/%: ../Exercise04/%.c
	$(CC) $(CFLAGS) -o $@ $<

../Exercise05/%: ../Exercise05/%.c
	$(CC) $(CFLAGS) -o $@ $<

../Exercise06/%: ../Exercise06/%.c
	$(CC) $(CFLAGS) -o $@ $<

# Run all 6 locally with configurable NP (default: 4)
run-local: all
	@echo "=========================================="
	@echo "Running all exercises locally (np=$(NP))"
	@echo "=========================================="
	@for exe in $(TARGETS); do \
		echo "\n>>> Running $$exe <<<"; \
		mpirun --oversubscribe -np $(NP) ./$$exe; \
	done

# Run all 6 on the EC2 cluster using the hostfile
run-cluster: all
	@echo "=========================================="
	@echo "Running all exercises on EC2 (np=$(NP))"
	@echo "=========================================="
	@for exe in $(TARGETS); do \
		echo "\n>>> Running $$exe on Cluster <<<"; \
		mpirun --hostfile $(HOSTFILE) --oversubscribe -np $(NP) ./$$exe; \
	done

clean:
	rm -f $(TARGETS)

help:
	@echo "Available targets:"
	@echo "  make all          - Compile all 6 MPI programs"
	@echo "  make run-local    - Run all 6 locally (use NP=X to set rank count)"
	@echo "  make run-cluster  - Run all 6 on EC2 cluster (use NP=X HOSTFILE=path)"
	@echo "  make clean        - Remove compiled binaries"
