# ecal-orchestration-sample

Demonstrating a simple orchestration of two components using a service interface.

## How to build

```bash
mkdir _build
cd _build
cmake ..
cmake --build .
```

## What to prepare

To get a deterministic behavior you need to run all components and the orchestrator on the same machine and activate the local ipc handshake feature by setting the global ecal.ini parameter `memfile_ack_timeout` to a timeout in milliseconds like here

```ini
[publisher]
use_inproc                = 0
use_shm                   = 2
use_tcp                   = 0
use_udp_mc                = 2

memfile_minsize           = 4096
memfile_reserve           = 50
memfile_ack_timeout       = 1000 << now all publisher will wait up to 1 seconds for feedback (including processed callback) from a connected subscriber
memfile_buffer_count      = 1
memfile_zero_copy         = 0

share_ttype               = 1
share_tdesc               = 1
```

## How to run

First start the components `ecal_sample_component1` and `ecal_sample_component2`. Finally start the orchestrator `ecal_sample_orchestrator`. If all is orchestrated correctly component2 should look like this

![image](https://user-images.githubusercontent.com/49162693/199268774-a345e756-0a66-41e8-b0d3-6e68ec6bcb06.png)

In case of inconsitent subscription, component2 two will log an error like this.

![image](https://user-images.githubusercontent.com/49162693/199269064-1a0e415f-be28-4dd3-ae76-ef484c55ac69.png)
