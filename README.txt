vzmem: visual noncontradictory memory distribution tool for OpenVZ
(C) dkLab, http://en.dklab.ru/lib/dklab_vzmem/


SYNOPSYS
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
