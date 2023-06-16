```
root@node11.tjmp02:~# ls -li /mnt/
total 16
      1314036 drwxr-xr-x 2 root root 4096 Mar 14 19:56 lltest
**1099511628813 drwxr-xr-x 2 root root    0 Jun 13 21:55 myshare**
       524289 drwxr-xr-x 2 root root 4096 Nov 11  2022 nas
       524290 drwxr-xr-x 2 root root 4096 Nov 14  2022 nas1
       527213 drwxr-xr-x 2 root root 4096 Feb 23 11:53 nfs     

root@node11.tjmp02:~/fuse# ls -li
total 2
1099511629309 drwxr-xr-x 2 root root 137438953472 Jun 12 20:43 bench
**1099511628813 drwxr-xr-x 2 root root            0 Jun 13 21:55 nas-00920221097402520097**
1099511627782 drwxr-xr-x 3 root root 171798691840 Jun  8 14:49 nas-20704072200243132250
1099511628796 drwxr-xr-x 3 root root  11811160623 Jun 13 19:24 nas-62242350433942034230
```  

delete root dir in cephfs by fuse, and create the root dir again

```
root@node11.tjmp02:~/fuse# rm -rf nas-00920221097402520097
root@node11.tjmp02:~/fuse# mkdir nas-00920221097402520097
root@node11.tjmp02:~/fuse# ls -li
total 2
1099511629309 drwxr-xr-x 2 root root 137438953472 Jun 12 20:43 bench
**1099511628814 drwxr-xr-x 2 root root            0 Jun 13 22:30 nas-00920221097402520097**
1099511627782 drwxr-xr-x 3 root root 171798691840 Jun  8 14:49 nas-20704072200243132250
1099511628796 drwxr-xr-x 3 root root  11811160623 Jun 13 19:24 nas-62242350433942034230

```

then ls the cifs client mount dir can see "Stale file handle"
