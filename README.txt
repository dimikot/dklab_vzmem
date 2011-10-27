vzmem: visual noncontradictory memory distribution tool for OpenVZ
(C) dkLab, http://en.dklab.ru/lib/dklab_vzmem/


Vzmem is a pseudo-graphical tool which allows you to distribute physical 
memory among all VEs consistently. It shows all physical memory blocks 
graphically in /etc/vz/conf/MEM-MAP  text file and lets you to move these 
blocks from one VE to another to redistribute the memory. Also you may 
specify "additional" memory personally for each VE: such memory will be 
obtained from system's free memory or swap (it is reflected as modifying 
of privvmpages parameter). 


INSTALLATION
------------

cd /usr/sbin
wget https://raw.github.com/DmitryKoterov/dklab_vzmem/master/vzmem
chmod +x vzmem


SYNOPSIS
--------

1. Initialize a new /etc/vz/conf/MEM-MAP file based on your 
   existed OpenVZ configs:
   
   vzmem -i 300

2. Edit this file with any text editor to re-distribute the memory
   available to containers:
   
   300
   10003 vps1.example.com      ========== 109552K
   10004 vps2.example.com      ============================== 335503K
   20004 vps3.example.com      ==========+++++++++++++++ 109552K + 221324K swap
   FREE                        ====================== 513525K   

   You see, all the RAM is divided into 300 blocks, each block is displayed 
   as "=" character. You may move these "=" characters among virtual machines
   to redistribute the memory (but you MUST keep the total number of "="'s
   equals to 300). You may also add "+" characters to specify that this block 
   may be used not as a RAM-block only, but as SWAP too.
   
3. To apply changes you made in /etc/vz/conf/MEM-MAP, run:

   vzmem -a

   After you run this, vzmem will also recalculate memory kilobytes displayed
   at the right side of each bar.
