Space requirement: ~20GB (riscv-gnu-toolchain with dependencies), ~2GB (compiled tool only)

Complete script:
```bash
git clone --recursive https://github.com/riscv/riscv-gnu-toolchain
cd riscv-gnu-toolchain/
./configure --prefix=/opt/riscv --with-arch=rv32i --with-abi=ilp32
sudo make
export PATH=$PATH:/opt/riscv/bin
source ~/.bashrc
```

1. Clone repo and its dependencies and cd to it
```bash
git clone --recursive https://github.com/riscv/riscv-gnu-toolchain
cd riscv-gnu-toolchain/
```

2. configuration for installing with correct architecture (rv32i2p0)
```bash
./configure --prefix=/opt/riscv --with-arch=rv32i --with-abi=ilp32
```

3. compile the tools to destination
```bash
sudo make
```

4. source the tools to PATH to make them usable
```bash
export PATH=$PATH:/opt/riscv/bin
source ~/.bashrc
```
