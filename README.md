# The Beginner's Guide to eBPF Programming for Networking

As seen at Cloud Native eBPF Day 2021. 

## Setup

Create a container that we can issue curl requests to. 

```
docker run -d --rm --name backend-A -h backend-A --env TERM=xterm-color nginxdemos/hello:plain-text

# Get the IP address of this target 
docker exec -it backend-A ip a 
```

Create a privileged container from which we can run eBPF programs. We will attach most of our programs to its `eth0` virtual
interface. 

```
docker run --rm -it -v /usr:/usr -v /home:/home -v /sys:/sys --privileged --env TERM=xterm-color -h container ubuntu
```

Assuming you cloned this repo into your home directory, the mount of `/home`
means you can `cd /home/<user name>/ebpf-networking` within this container to
find this example code.

In a separate terminal window, observe the debug trace output: 

```bash
sudo cat /sys/kernel/debug/tracing/trace_pipe
```

## Prerequisites

These examples use [BCC](https://github.com/iovisor/bcc)

## Examples

See the
[slides](https://speakerdeck.com/lizrice/beginners-guide-to-ebpf-programming-for-networking)
and video (coming soon) for more info on the different examples included here,
and how to use them. 

Examples include 
* Kprobe on tcp_v4_connect() kernel function
* Attaching a socket filter to a raw socket 
* XDP 
* Traffic control - adding a filter on ingress 

