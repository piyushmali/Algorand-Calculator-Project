# Algorand-Calculator-Project

This repository contains a simple smart contract developed on the Algorand blockchain. The contract allows for the calculation of the sum of two numbers. It was created using the Algorand Developer Tutorial and the Playground template.

## Smart Contract Implementation

The smart contract is implemented in the `calculator.py` file located in the `Algorand-Calculator-Project/playground/calculator` directory. The code uses the Beaker framework for smart contract development with PyTeal.

```python
import beaker as bk
import pyteal as pt

class MyState:
    result = bk.GlobalStateValue(pt.TealType.uint64)

app = bk.Application("Calculator", state=MyState())

@app.external
def add(a: pt.abi.Uint64, b: pt.abi.Uint64, *, output: pt.abi.Uint64) -> pt.Expr:
    add_result = a.get() + b.get()
    return pt.Seq(
        app.state.result.set(add_result),
        output.set(add_result)
    )

@app.external(read_only=True)
def read_result(*, output: pt.abi.Uint64) -> pt.Expr:
    return output.set(app.state.result)

if __name__ == "__main__":
    spec = app.build()
    spec.export("artifacts")
```

## Quick Start

To quickly get started with the Algorand Calculator Smart Contract, follow these steps:

1. Ensure you have AlgoKit installed and run `algokit bootstrap all` in this directory.
2. Open this directory in Visual Studio Code for a more enhanced experience.
3. Open the smart contract at `playground/calculator/calculator.py`.
4. Press F5 to start the execution.
5. This will initiate the LocalNet, build the smart contract, deploy it, and call the contract.

## Detailed Instructions

### Initial Setup

To set up the project for development, follow these instructions:

1. Clone this repository to your local machine.
2. Install the following pre-requisites:
   - Install `AlgoKit` - [Link](https://github.com/algorandfoundation/algokit-cli#install): Make sure you can execute `algokit --version`.
   - Bootstrap your local environment by running `algokit bootstrap all` within this folder. This step will:
     - Install `Poetry` - [Link](https://python-poetry.org/docs/#installation): The minimum required version is `1.2`. Verify by running `poetry -V`, which should return `1.2` or higher.
     - Run `poetry install` in the root directory. This will set up a `.venv` folder with a Python virtual environment and install all Python dependencies.
3. Open the project and start debugging/developing using the following options:
   - Visual Studio Code:
     1. Open the repository root in VS Code.
     2. Install the recommended extensions.
     3. Press F5 (or your mapped debug key) with a contract open (default: [`playground/calculator/calculator.py`](./playground/calculator/calculator.py)). By default, it will run the `demo.py` file in the same folder as the contract using the `Demo current contract (+ LocalNet)` configuration. This will start LocalNet, build the contract, and deploy it to LocalNet.
        > **Note:**
        > If you are using Windows, make sure to select the Python Interpreter before the first run:
        > 1. Open the command palette (Cmd/Ctrl + Shift + P).
        > 2. Search for `Python: Select Interpreter`.
        > 3. Select `./.venv/Scripts/python.exe`.
   - IDE (e.g., PyCharm):
     1. Open the repository root in your IDE.
     2. The IDE should automatically detect it as a Poetry project and set up a Python interpreter and virtual environment.
     3. Press Shift+F9 (or your mapped debug key) to start debugging with breakpoints.
   - Other editors:
     1. Open the repository root in your preferred text editor.
     2. In a terminal, run `poetry shell`.
     3. Run the [demo script](./playground/hello_world/demo.py) `python playground/hello_world/demo.py` using your preferred debugger.

### Subsequently

1. If you update the source code to the latest version and new dependencies are added, run `algokit bootstrap all` again.
2. Follow step 3 above to continue development.

## Tools Used

The following tools are used in this project:

- [Algorand](https://www.algorand.com/): A Layer 1 Blockchain. Explore the [Developer portal](https://developer.algorand.org/) and discover [Why Algorand?](https://developer.algorand.org/docs/get-started/basics/why_algorand/).
- [AlgoKit](https://github.com/algorandfoundation/algokit-cli): A comprehensive tool for developers building on the Algorand network. Check out the [docs](https://github.com/algorandfoundation/algokit-cli/blob/main/docs/algokit.md) and get started with the [intro tutorial](https://github.com/algorandfoundation/algokit-cli/blob/main/docs/tutorials/intro.md).
- [Beaker](https://github.com/algorand-devrel/beaker): A smart contract development framework for PyTeal. Dive into the [docs](https://beaker.algo.xyz) and explore the [examples](https://github.com/algorand-devrel/beaker/tree/master/examples).
- [PyTEAL](https://github.com/algorand/pyteal): Python language binding for Algorand smart contracts. Refer to the [docs](https://pyteal.readthedocs.io/en/stable/) for more information.
- [AlgoKit Utils](https://github.com/algorandfoundation/algokit-utils-py): A set of core Algorand utilities that simplify building solutions on Algorand.
- [Poetry](https://python-poetry.org/): A powerful Python packaging and dependency management tool.

We hope you find this project and its README file helpful in exploring the world of Algorand blockchain and smart contract development. Happy coding!
