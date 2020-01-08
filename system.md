# System

## File System

### EROFS: A Compression-friendly Readonly File System for Resource-scarce Devices (ATC 2019) (2020-01-03)

Existing compression file system is I/O and memory inefficiency. This work designs and implements a compression-friendly readonly file system. It uses fix-sized output compression method, and uses several optimization methods, including using cache, using per-cpu buffer, using rolling-decompression.

The basic point of this paper is that compression-friendly readonly file system is usfule for low-level smartphonse. Its main contribution is the design and implementation of the file system in android. The idea is valuable, and the implementation needs complicated technical knowledge.