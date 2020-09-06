## Day 1:

- Implementation of namespaces, control groups, chroot (3 features) in Linux kernel is what enables Containers.\
a. Containers are just normal Linux Processes with additional configuration applied.\
b. The concept of namespaces is to limit what processes can see and access certain parts of the system, such as other network interfaces or processes.\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;When a container is started, the container runtime, such as Docker, will create new namespaces to sandbox the process.\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;By running a process in it's own Pid namespace, it will look like it's the only process on the system.\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The available namespaces are:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* Mount (mnt)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* Process ID (pid)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* Network (net)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* Interprocess Communication (ipc)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* UTS (hostnames)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* User ID (user)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;* Control group (cgroup)\
c. Chroot provides the ability for a process to start with a different root directory to the parent OS. This allows different files to appear in the root.\
d. Cgroups (Control Groups) limit the amount of resources a process can consume.\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;These concepts are prevalent in Unix variants. As a result, Windows support for Docker is poor. You run containers in a VM(!) which defeats the purpose of Dockers.\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The Unix variants (FreeBSD, other Linux distros) are all clones on Unix.\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;This means system call interoperability isn’t an issue.\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;So, a docker built on macOS (BSD based) will run on Linux.
- Linux Containers/Docker technically speaking is not a virtualization technology. They run natively on the Host OS. More a OS virtualization.
- A Docker image is a private file system just for your container. It provides all the files and code your container needs. Running a container launches your application with private resources, securely isolated from the rest of your machine. Save and share your image on Docker Hub to enable other users to easily download and run the image on any destination machine.
- LXC, pronounced LexC (Canonical, Ltd. who make Ubuntu)

- “K8s is user space application
- Montevista is an embedded Linux distro based in Bay Area, 1999, 
- Cisco is big on x86 for a long time
- My customer wants to run 1000 VMs on a high end node.
- A startup by name Viata (here in the Bay; bought by Brocade) created a virtual router running in a (KVM based) VM.
- OpenCL 1.0 - future of virtualization
- OpenVZ  - earliest container project.
- CoreOS is container focused (not everything in the Linux) Linux OS.
- Tectonic = CoreOS + K8s
- K8s - intuitively represents the SDN model.
- Racket/Racquet does stateful pod migration working with K8s.
- Docker is and will be written in Golang as libcontainer is in Golang.
- Government will step in and break up Intel into smaller companies just like Bell Labs. For the reason of National Security.
- Openstack is too complex compared to K8s.
- Look up SDxCentral
- Intel bought Altera (FPGA; beat all the competition; smart move; buy their stock)
- ARM is the new Qualcomm (fabless design; they have more lawyers than engineers to keep get royalties. 25 cents per chip.)
- jetdoc1 - instructor’s docker hub repo
- AT&T runs Cisco containers in production.
- Vagrant is lightweight Virtualbox.
- Sonic is Microsoft Linux distro for routers/switches/data-centers.
- US Defense stuck with Windows - IT old-school, apprehensive of security with Linux

- Hypervisor based VM <-> System based containers (needs a full rootfs) <-> docker containers (or lightweight containers). These 3 can coexist in a system.
- The hypervisor on which the VM runs fools the OS - makes for HW abstraction layer.
- Containers (Docker, LXC, KVM) run natively on the OS. That’s why they give good performance. You cannot install OS on the container. Docker runs a single application usually out-of-the-box.
- Security and interoperability are the important concerns for containers.
	Will you run Cisco and Arista container side by side?
- Namespaces represents a logical boundary for containers.
- Control groups control resources allocated to namespaces. cgroup can control Kernel subsystems which in turn control resources on the system.
- Chroot makes the container think it has its own root filesystem (starting with root) that way it doesn’t look outside
- If you are a native process/container with root permissions you can access all the resources of all other containers.

- VMs are heavy - every VM has its own copy of the OS - heavy - but, that’s an advantage as well. VMs can also share resources like containers, but needs more work (unlike the containers) enabling that.
- Startup and tear down of VMs very slow - in the order of a microsecond.
- Docker Engine essentially does provisioning the containers. Containers running don’t go through the Docker engine at runtime. Docker image on VM vs container environment.
- !Back storage driver vs Host file system
	Just one back storage driver is needed to enable multiple containers.
- By definition, a container needs at least one process running inside. That process ID (though different from inside the container) is unique in the host.

## Day 2:

- DPDK - data path SDK (from Intel) to accelerate NICs and packet processing
- Throughput continues to be a challenge for Service Providers (unlike Data Centers). That’s because the specialized HW (ASICs, DSP) implementing VNFs provide high throughput which can’t be met with container based systems. Service Providers are usually vendor locked.
- Docker is well documented.
- It’s common to find docker containers run inside a VM.
- Docker website has a rich variety of images. Don’t have to reinvent the wheel.
- Upfront cost is what makes a customer decide between a virtualized router vs a router as a box. The former has the advantage of having any number of ports, say 1000, unlike on the box.
- Docker file is more like a makefile to build an image.
- Docker wait command - use case - transcoding of imported video (container 1) prior to streaming it (container 2).

## Day 3:

- Registry which manages push/pull of images is available as a docker.
- Creating an image from the beginning with a Dockerfile is recommended for production.
- Why create many ‘veth’s per container? Service chaining!


## Day 4:

- Data centers demand a high level of security.
- Fort Knox in Kentucky is where the treasury’s gold depository.
- Secure TCP using TLS.
- Use OpenSSL to generate and self-sign certificates.
- DPDK is available for both x86 and arm.
- Tetration - network analytics - deep network inspection - $0.5 million - expensive Cisco solution
- FD.io (“Fido”) is Vector Packet Processing software solution from Cisco. But poor documentation. FD.io blows DPDK of the water in terms of throughput.
- DPDK might help FD.io. Now Ligato, a combo of  FD.io+ DPDK.
- Software arm of arm.
- Jeff Bezos coined the term “two-pizza-teams”. Gave birth for the notion of microservices.
- Small Linux distros: busybox > puppy linux > DSL (damn small linux)
- https://netfilter.org/ -> IP tables invented here.
- Suricata is way better than Snort.
