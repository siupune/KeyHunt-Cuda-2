# KeyHunt-Cuda-2 
_Hunt for Bitcoin private keys._
## This is a experimental project & right now going through a lot of changes, so bugs and errors can appears.

it's is a modified version of [KeyHunt-Cuda](https://github.com/kanhavishva/KeyHunt-Cuda/).


## Changes
- Removed endomorphism and curve symmetry.


# Usage

CPU and GPU can not be used together, because right now the program divides the whole input range into equal parts for all the threads, so use either CPU or GPU so that the whole range can increment by all the threads with consistency.

Minimum address should be more than 1000.

```
KeyHunt-Cuda-2.exe -h
Usage: KeyHunt-Cuda-2 [options...]
Options:
    -v, --version          Print version
    -c, --check            Check the working of the codes
    -u, --uncomp           Search uncompressed addresses
    -b, --both             Search both uncompressed or compressed addresses
    -g, --gpu              Enable GPU calculation
    -i, --gpui             GPU ids: 0,1...: List of GPU(s) to use, default is 0
    -x, --gpux             GPU gridsize: g0x,g0y,g1x,g1y, ...: Specify GPU(s) kernel gridsize, default is 8*(Device MP count),128
    -o, --out              Outputfile: Output results to the specified file, default: Found.txt
    -m, --max              Specify maximun number of addresses found by each kernel call
    -t, --thread           threadNumber: Specify number of CPU thread, default is number of core
    -l, --list             List cuda enabled devices
    -f, --file             Ripemd160 binary hash file path
    -a, --addr             P2PKH Address (single address mode)
    -s, --start            Range start in hex
    -e, --end              Range end in hex, if not provided then, endRange would be: startRange + 10000000000000000
    -h, --help             Shows this page

```

Single address mode:
```
KeyHunt-Cuda-2.exe -t 0 -g -i 0 -x 256,256 -s 1 -e 40080000e -a 17b6NGbyaFqe581jG2KG1wr6sTWHYuDuLB

KeyHunt-Cuda-2 v1.00

MODE         : COMPRESSED
DEVICE       : GPU
CPU THREAD   : 0
GPU IDS      : 0
GPU GRIDSIZE : 256x256
SSE          : YES
MAX FOUND    : 65536
ADDRESS      : 17b6NGbyaFqe581jG2KG1wr6sTWHYuDuLB (single address mode)
OUTPUT FILE  : Found.txt

Start Time   : Fri Apr  2 09:53:54 2021
Global start : 0000000000000000000000000000000000000000000000000000000000000001 (1 bit)
Global end   : 000000000000000000000000000000000000000000000000000000040080000E (35 bit)
Global range : 000000000000000000000000000000000000000000000000000000040080000D (35 bit)

GPU          : GPU #0 GeForce GTX 1650 (14x64 cores) Grid(256x256)

GPU 0 Thread 000000: 0000000000000000000000000000000000000000000000000000000000000001 : 0000000000000000000000000000000000000000000000000000000000040081
GPU 0 Thread 000001: 0000000000000000000000000000000000000000000000000000000000040081 : 0000000000000000000000000000000000000000000000000000000000080101
GPU 0 Thread 000002: 0000000000000000000000000000000000000000000000000000000000080101 : 00000000000000000000000000000000000000000000000000000000000C0181
                   .
GPU 0 Thread 065535: 00000000000000000000000000000000000000000000000000000004007BFF81 : 0000000000000000000000000000000000000000000000000000000400800001

[00:00:42] [CPU+GPU: 386.52 Mk/s] [GPU: 386.52 Mk/s] [C: 96%] [T: 16,642,998,272 (34 bit)] [F: 0]
==================================================================
PubAddress: 17b6NGbyaFqe581jG2KG1wr6sTWHYuDuLB
Priv (WIF): p2pkh:KwDiBf89QgGbjEhKnhXJuH7LrciVrZi3qYjgd9MLtbs3HaFEuy1K
Priv (HEX): 0x400800000
==================================================================
[00:00:44] [CPU+GPU: 382.63 Mk/s] [GPU: 382.63 Mk/s] [C: 101%] [T: 17,381,195,776 (35 bit)] [F: 1]

BYE
```

## Building
##### Windows
- Microsoft Visual Studio Community 2019 
- CUDA version 10.0
##### Linux
 - Edit the makefile and set up the appropriate CUDA SDK and compiler paths for nvcc. Or pass them as variables to `make` command.

    ```make
    CUDA       = /usr/local/cuda-11.0
    CXXCUDA    = /usr/bin/g++
    ```
 - To build CPU-only version (without CUDA support):
    ```sh
    $ make all
    ```
 - To build with CUDA:
    ```sh
    $ make gpu=1 CCAP=35 all
    ```

## License
KeyHunt-Cuda-2 is licensed under GPLv3.

## Disclaimer
ALL THE CODES, PROGRAM AND INFORMATION ARE FOR EDUCATIONAL PURPOSES ONLY. USE IT AT YOUR OWN RISK. THE DEVELOPER WILL NOT BE RESPONSIBLE FOR ANY LOSS, DAMAGE OR CLAIM ARISING FROM USING THIS PROGRAM.

