# The Cosette Solver (Backend)

This is a reimplementation of the Cosette solver in Rust aiming for high performance and better SQL feature coverage.
The theory behind the solver is described in [this paper](https://www.vldb.org/pvldb/vol11/p1482-chu.pdf).
It currently expect input generated from [this parser](https://github.com/cosette-solver/cosette-parser).

## Usage

After downloading the source, build the source with
```sh
cargo build --release
```
The current setup of the solver has the Z3 solver as a runtime dependency,
so you need to have the `z3` executable in the `PATH` when running Cosette.
The build should produce an executable, or you can use `cargo` to run:
```sh
cargo run --release -- <inputs>
```
where the `<inputs>` are paths to input files or directories containing the files.
The results will be simply printed out currently, with the name of each file and their result (provable/not provable).
You can set the environment variable to `RUST_LOG=info` when running and get a (very) verbose output.
This is useful for debugging as it prints out how expressions are simplified in the solver at various stages.

Then input files should be generated by the parser.
They are all in JSON format.
The directory `tests/RelOptRulesTest/` contains such files that are directly extracted from the [Calcite](https://calcite.apache.org/) project.
You may try out running these inputs by
```sh
cargo run --release -- tests/RelOptRulesTest/
```
WARNING: many test cases in this folder contain features that we haven't support yet.
Only ~170 out of all ~380 cases are actually provable for now.
