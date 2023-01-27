# Run RISCV and AAPG tests

## Getting Started

- After building the core , we would need to run tests to verify if the implementation of core is correct.
- Riscv tests are used as sanity and AAPG tests are used for more regressive testing

## Prerequisites
- Verilator
- riscv-gnu-toolchain
- Python 3.0+


## Running RISCV tests
- Type all these commands in the home directory of the core
- Make sure all the prerequisite are loaded onto the shell's Path before running the commands
- Only the failed tests are stored in <home_directory>/verification/workdir

### To run individual tests
```bash
make test opts='--test=<testName> --suite=<testSuite>'
```
Example
```bash
 make test opts='--test=add --suite=rv64ui' 
```
    
#### Available flags
1. test
2. suite
3. sim (default=bluespec)
4. type (default=p)
5. debug (used to display the running command)
6. timeout

### To run batch of riscv-tests
```bash
make regress opts='--filter=rv64'
```

#### Available flags
- filter (used for specifying the list of riscv tests)
- list (used for specifying the list of aapg tests)
- debug (used to display the running command)
- proc (specifies the number of cores to be used) {min:1 ,max:os.cpu_count()}


## Generating and running AAPG test
- All the generated tests are available at <home_directory>/verification/workdir/aapg/ and the list is available at <home_directory>/verification/workdir

### To generate random aapg test
```bash
 make aapg opts='--config=rv64imafdc* --test_count=40 --parallel=16' CONFIG_ISA=RV64IMAFDC
```
### To generate aapg test with certain seed value
```bash
make aapg opts="--config=<testConfig> --test_count=1 --parallel=6 --aapg_opts='--seed=<seed_value>'" CONFIG_ISA=RV64IMAFDC
```
   
