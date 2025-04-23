# Blockchain Miner

A simple package to understand how blockchains work.

## Installation

```shell
go get github.com/sam-the-programmer/blockchainminer
```

Then, import it with...

```go
import (
	m "github.com/sam-the-programmer/blockchainminer/miner"
)
```

<br>

## Usage

The bulk of the API is here. More detail is on [pkg.go.dev](https://pkg.go.dev/github.com/s4m-mo/blockchainminer)

```go
package main

import (
	"fmt"

	"github.com/s4m-mo/blockchainminer/hash"
	"github.com/s4m-mo/blockchainminer/miner"
)

func main() {
	transactionString := "<BlockNum-0>\nAlice->Bob->20\nBob->Charlie->10\nCharlie->Alice->5\n[PrevBlockHash]\n%v"
	m := miner.NewMiner(
		transactionString,
		hash.SHA256,
		10000,
	)

	m.SetSearchSize(100000000000)
	m.SetDifficulty(6)
	m.SetHashTimes(1)
	m.SetOutputLevel(1)

	solution, hasFound := m.ThreadedMine()
	if hasFound {
		fmt.Println("\n\n", solution, "\n", hash.SHA256(hash.SHA256(fmt.Sprintf(transactionString, solution))))
	}
}

```

<br>

