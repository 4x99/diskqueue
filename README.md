# DiskQueue

Disk-based FIFO queue

---

## Features

- FIFO
- High performance

---

## Getting Started

```
go get -u github.com/4x99/diskqueue
```

```
package main

import (
	"fmt"
	"github.com/4x99/diskqueue"
	"log"
)

func main() {
	// start
	diskqueue.Config.Path = "/tmp"
	queue, err := diskqueue.Start()
	if err != nil {
		log.Fatalln(err)
	}

	// write data
	err = queue.Write([]byte("data"))
	fmt.Println(err)

	// read data
	if data, err := queue.Read(); err != nil {
		fmt.Println(data)
	}
}
```

---

## Default Config

```
Config = &config{
	Path:              "data",
	FilePerm:          0600,
	BatchSize:         100,
	BatchTime:         time.Second,
	SegmentSize:       50 * 1024 * 1024,
	SegmentLimit:      2048,
	CheckpointFile:    ".checkpoint",
	MinRequiredSpace:  1024 * 1024 * 1024,
}
```
