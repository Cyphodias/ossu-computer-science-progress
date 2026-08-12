# ubuntu desktop

The desktop is the dedicated Linux workstation for Computer Science study, development and practical experimentation.

## purpose

- Linux development
- programming assignments and projects
- algorithms and data-structure implementations
- systems programming
- networking practice
- database work
- containers and virtualization
- machine-learning and AI development

## baseline environment

- current supported Ubuntu release used for the workstation
- Git
- Python
- GCC/G++
- GDB
- Make
- CMake
- SSH/OpenSSH
- standard Linux command-line tools
- VS Code or equivalent development environment

## course-oriented tooling

### programming

- Python
- C/C++
- Java or other languages required by coursework
- compilers
- debuggers
- build systems
- testing frameworks

### systems

- process and memory inspection tools
- systemd tools
- filesystem utilities
- networking utilities
- `strace` and related tracing/debugging tools

### networking

- Wireshark
- tcpdump
- iproute2
- DNS/network diagnostic tools

### databases

- SQLite
- PostgreSQL where required
- database clients and command-line tools

### containers and virtualization

- container runtime as required
- QEMU/KVM where appropriate
- tools for creating isolated test environments

### AI / machine learning

- Python virtual environments
- NumPy
- pandas
- scientific-computing libraries
- PyTorch or other frameworks required by current study

## configuration philosophy

The desktop should remain a clean, reproducible Linux development environment. Course-specific dependencies should preferably be isolated using virtual environments, containers or dedicated VMs rather than turning the base system into an unmaintainable dependency collection.

## public documentation rule

Do not record private network information, credentials, personal identifiers, private keys or other sensitive system details.
