# MPI-based Producer-Consumer Simulation

This project simulates a producer-consumer system using MPI (Message Passing Interface) in C, where producers generate work items and send them to a broker, which then distributes them to consumers.

## Overview

The program consists of three main components:
- **Producer**: Each producer generates work and sends it to the broker.
- **Broker**: The broker receives work from producers and dispatches it to consumers upon request.
- **Consumer**: Each consumer requests work from the broker and processes the received work.

This simulation demonstrates basic principles of parallel computing and communication using MPI.

## Features
- **Asynchronous Communication**: The program uses non-blocking MPI operations (`MPI_Isend` and `MPI_Recv`) to send and receive messages between processes.
- **Time Management**: The broker checks the elapsed time during communication and can abort the process if it exceeds a predefined threshold.
- **Work Production and Consumption**: Producers generate work based on a formula and send it to the broker. Consumers request and process work from the broker.
- **Synchronization**: The program synchronizes communication between producers, consumers, and the broker using MPI.

## Requirements
- **MPI Library**: You need to have an MPI implementation installed. For example, you can install OpenMPI or MPICH.
- **C Compiler**: A C compiler like GCC is required to compile the code.

## Compilation and Execution

1. **Install MPI**:
   Ensure that you have an MPI library installed. For OpenMPI, you can install it on Linux systems using:
   ```bash
   sudo apt-get install openmpi-bin openmpi-common libopenmpi-dev


2. **Compile the Program**:
   Use the `mpicc` compiler to compile the code:

   ```bash
   mpicc -o producer_consumer producer_consumer.c
   ```

3. **Run the Program**:
   Use `mpirun` or `mpiexec` to run the program with multiple processes. For example, to run with 4 processes:

   ```bash
   mpirun -np 4 ./producer_consumer <time_threshold>
   ```

   Where `<time_threshold>` is the time limit (in seconds) after which the broker will abort the communication.

## Program Flow

1. **Producers** generate work units and send them to the broker.
2. **Broker** receives work from producers and stores it. The broker then sends work to consumers upon request.
3. **Consumers** request work from the broker, process the work, and continue until the communication time limit is reached or all work is consumed.

## Variables and Functions

* **time\_rec**: Defines the time threshold (in seconds) after which the broker sends an "ABORT" message to the processes.
* **MPI\_Isend** and **MPI\_Recv**: Used for asynchronous communication between producers, the broker, and consumers.
* **MPI\_Waitany**: Waits for any of the non-blocking send/receive operations to complete.

## Example Output

For producers:

```
Producer 1 sent message 5 to Broker
Producer 1 received message ACK from Broker
```

For consumers:

```
Consumer 2 sent message Req to Broker
Consumer 2 received message 7 from Broker
```

## Authors

* **Your Name**: \[Your email/contact information]

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

