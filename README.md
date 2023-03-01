Below Steps allows u run setup build and run sample application within 5 min.

# Zephyr Docker Images
git clone https://github.com/alokprasad/zephyr-rtos-build-docker.git

cd zephyr-rtos-build-docker

sh build_docker.sh

mkdir zephyr-ws && chmod -R 777 zephyr-ws && cd zephyr-ws

docker run -ti -v $(pwd):/workdir zephyr-build-sys

## checkout rtos and build sample (only needed once)

user@dbee68a48bcd:/workdir$ west init .

user@dbee68a48bcd:/workdir$ west update

user@dbee68a48bcd:/workdir$ west zephyr-export

## sample Run


west build -b qemu_x86 zephyr/samples/hello_world

west build -t run

## Debugging gdb sample

west build -b qemu_x86 zephyr/samples/subsys/debug/gdbstub

west build -t run

In another shell connect to existing docker 
  docker exec -it  <docker_instance_via_docker_ps>  /bin/bash 
  
  gdb build/zephyr/zephyr.elf
  
  (gdb) target remote :5678  
