## Adicionar um novo disco no Linux 

Neste artigo, vou demonstrar como adicionar um novo disco ao sistema operacional Linux.<br>
Nesse ambiente, usamos a seguinte versão:

> **Sistema Operacional:** Oracle Linux 8.10<br>
> **Disco:** 4 TiB

## Introdução:
Em um dos ambientes que operamos, um dos servidores não possui acesso externo(internet) e precisamos instalar um pacote que depende de algumas bibliotecas. Para isso, utilizamos a imagem ISO como fonte local para a instalação dos pacotes via YUM, eliminando a necessidade de acessar a internet.

### Criar novo diretório:
mkdir -p backup

### Lista via comando fdisk os discos:
# fdisk -l
Disk /dev/sdb: 4 TiB, 4398046511104 bytes, 8589934592 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 4664AF5D-13F5-4E2F-8AB2-AF51A27542B5


### Criar a partição e alterar tipo:  
gdisk /dev/sdb
GPT fdisk (gdisk) version 1.0.3

Warning: Partition table header claims that the size of partition table
entries is 0 bytes, but this program  supports only 128-byte entries.
Adjusting accordingly, but partition table may be garbage.
Warning: Partition table header claims that the size of partition table
entries is 0 bytes, but this program  supports only 128-byte entries.
Adjusting accordingly, but partition table may be garbage.
Partition table scan:
  MBR: MBR only
  BSD: not present
  APM: not present
  GPT: not present


*********************
Found invalid GPT and valid MBR; converting MBR to GPT format
in memory. THIS OPERATION IS POTENTIALLY DESTRUCTIVE! Exit by
typing 'q' if you don't want to convert your MBR partitions
to GPT format!
*********************


Command (? for help): m
b       back up GPT data to a file
c       change a partition's name
d       delete a partition
i       show detailed information on a partition
l       list known partition types
n       add a new partition
o       create a new empty GUID partition table (GPT)
p       print the partition table
q       quit without saving changes
r       recovery and transformation options (experts only)
s       sort partitions
t       change a partition's type code
v       verify disk
w       write table to disk and exit
x       extra functionality (experts only)
?       print this menu

Command (? for help): p
Disk /dev/sdb: 8589934592 sectors, 4.0 TiB
Model: Virtual disk
Sector size (logical/physical): 512/512 bytes
Disk identifier (GUID): 4664AF5D-13F5-4E2F-8AB2-AF51A27542B5
Partition table holds up to 128 entries
Main partition table begins at sector 2 and ends at sector 33
First usable sector is 34, last usable sector is 8589934558
Partitions will be aligned on 2048-sector boundaries
Total free space is 8589934525 sectors (4.0 TiB)

Number  Start (sector)    End (sector)  Size       Code  Name

Command (? for help): n
Partition number (1-128, default 1):
First sector (34-8589934558, default = 2048) or {+-}size{KMGTP}:
Last sector (2048-8589934558, default = 8589934558) or {+-}size{KMGTP}:
Current type is 'Linux filesystem'
Hex code or GUID (L to show codes, Enter = 8300): 8e00
Changed type of partition to 'Linux LVM'

Command (? for help): p
Disk /dev/sdb: 8589934592 sectors, 4.0 TiB
Model: Virtual disk
Sector size (logical/physical): 512/512 bytes
Disk identifier (GUID): 4664AF5D-13F5-4E2F-8AB2-AF51A27542B5
Partition table holds up to 128 entries
Main partition table begins at sector 2 and ends at sector 33
First usable sector is 34, last usable sector is 8589934558
Partitions will be aligned on 2048-sector boundaries
Total free space is 2014 sectors (1007.0 KiB)

Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048      8589934558   4.0 TiB     8E00  Linux LVM

Command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): y
OK; writing new GUID partition table (GPT) to /dev/sdb.
The operation has completed successfully.

### formatar disco
mkfs -t xfs /dev/sdb1

### Obter o uid:
blkid

### Ajustar o fstab:
# vi /etc/fstab
UUID=f99db564-7fb1-43b1-a169-db4cc03ce624 /backup xfs   defaults        0 0

### Montar o novo disco:
 mount -a

