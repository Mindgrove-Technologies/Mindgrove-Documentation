# Run RISCV and AAPG tests

## Running RISCV tests

### To run individual tests
    ```make
    make test opts='--test=<testName> --suite=<testSuite>'
    ```
    example
    ```make
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
```make
make regress opts='--filter=rv64'
```

#### Available flags
- filter (used for specifying the list of riscv tests)
- list (used for specifying the list of aapg tests)
- debug (used to display the running command)
- proc (specifies the number of cores to be used) {min:1 ,max:os.cpu_count()}


## Generating and running AAPG test

### To generate random aapg test
```make
 make aapg opts='--config=rv64imafdc* --test_count=40 --parallel=16' CONFIG_ISA=RV64IMAFDC
```
### To generate aapg test with certain seed value
```make
make aapg opts="--config=<testConfig> --test_count=1 --parallel=6 --aapg_opts='--seed=<seed_value>'" CONFIG_ISA=RV64IMAFDC
```
