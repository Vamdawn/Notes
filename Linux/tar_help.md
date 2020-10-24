# tar

## Usage

tar -- manipulate tape archives

```shell
tar [bundled-flags <args>] [<file> | <pattern> ...]
tar {-c} [options] [files | directories]
tar {-r | -u} -f archive-file [options] [files | directories]
tar {-t | -x} [options] [patterns]
```

## Options

```shell
-c | --create   
创建包含指定项目的归档文件

-r | --append   
新的内容被添加到归档文件的尾部(不能用于压缩)

-t | --list     
将归档文件的内容输出到stdout

-u | --update   
当新的内容修改日期比归档文件对应内容新时, 才添加新的内容

-x | --extract  
将归档文件的内容提取到磁盘(如果归档文件中有重复名称的文件, 后者将覆盖前者)

-f | --file     
Read the archive from or write the archive to the specified file.  The filename can be - for standard input or standard output.  The default varies by system; on FreeBSD, the default is /dev/sa0; on Linux, the default is /dev/st0.

-v | --verbose  
Produce verbose output.  In create and extract modes, tar will list each file name as it is read from or written to the archive.  In list mode, tar will produce output similar to that of ls(1).  An additional -v option will also provide ls-like details in create and extract mode.

-z | --gzip | --gnuzip
-c模式下, 使用gzip压缩生成的归档文件. 在提取模式和列举模式下, 该选项将被忽略. tar在读取归档文件时将自动识别出gzip压缩格式
```

## Example

```shell

tar -czf file.tar.gz source.c source.h

tar -tvf file.tar.gz

tar -x

tar -tf image.iso
```
