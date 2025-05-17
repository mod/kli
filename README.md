# A Simple CLI library. Dependency free.

[![GoDoc](https://godoc.org/github.com/mod/kli?status.svg)](https://godoc.org/github.com/mod/kli)

### Features

  * Nested Subcommands
  * Uses the standard library `flag` package
  * Auto-generated help
  * Custom banners
  * Hidden Subcommands
  * Default Subcommand
  * Dependency free

### Example

```go
package main

import (
   "fmt"
   "log"

    "github.com/mod/kli"
)

func main() {

	// Create new cli
	cli := kli.NewCli("Flags", "A simple example", "v0.0.1")

	// Name
	name := "Anonymous"
	cli.StringFlag("name", "Your name", &name)

	// Define action for the command
	cli.Action(func() error {
		fmt.Printf("Hello %s!\n", name)
		return nil
	})

	if err := cli.Run(); err != nil {
		fmt.Printf("Error encountered: %v\n", err)
	}

}
```

#### Generated Help

```shell
$ flags --help
Flags v0.0.1 - A simple example

Flags:

  -help
        Get help on the 'flags' command.
  -name string
        Your name
```

### Usage

Install the package:

```shell
go get github.com/mod/kli
```

Import in your Go code:

```go
import "github.com/mod/kli"
```

Create a new CLI application:

```go
cli := kli.NewCli("AppName", "Description", "v1.0.0")
```

Add flags, commands, and actions as needed:

```go
// Adding flags
cli.StringFlag("config", "Path to config file", &configPath)
cli.BoolFlag("verbose", "Enable verbose output", &verbose)
cli.IntFlag("port", "Port to listen on", &port)

// Adding a subcommand
cmd := cli.NewSubCommand("start", "Start the application")
cmd.Action(func() error {
    // Command logic here
    return nil
})

// Run the CLI
if err := cli.Run(); err != nil {
    log.Fatal(err)
}
```