# 1. default, smbd will start 3 processes:
```
root          39       2  0 Jun07 ?        00:00:14 smbd -F --no-process-group
root          55      39  0 Jun07 ?        00:00:14 smbd -F --no-process-group
root          56      39  0 Jun07 ?        00:00:15 smbd -F --no-process-group
```

1. main process
```
#0  0x00007fb79e033357 in epoll_wait (epfd=4, events=0x7ffe6fc13aec, maxevents=1, timeout=564032) at ../sysdeps/unix/sysv/linux/epoll_wait.c:30
#1  0x00007fb79e396f52 in epoll_event_loop (epoll_ev=0x5612bb592df0, tvalp=0x7ffe6fc13b30) at ../../lib/tevent/tevent_epoll.c:651
#2  0x00007fb79e39790c in epoll_event_loop_once (ev=0x5612bb580610, location=0x5612b9581790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent_epoll.c:938
#3  0x00007fb79e3940a2 in std_event_loop_once (ev=0x5612bb580610, location=0x5612b9581790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent_standard.c:110
#4  0x00007fb79e38b1ac in _tevent_loop_once (ev=0x5612bb580610, location=0x5612b9581790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent.c:825
#5  0x00007fb79e38b4fe in tevent_common_loop_wait (ev=0x5612bb580610, location=0x5612b9581790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent.c:948
#6  0x00007fb79e394144 in std_event_loop_wait (ev=0x5612bb580610, location=0x5612b9581790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent_standard.c:141
#7  0x00007fb79e38b5a1 in _tevent_loop_wait (ev=0x5612bb580610, location=0x5612b9581790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent.c:967
#8  0x00005612b957cdc2 in smbd_parent_loop (ev_ctx=0x5612bb580610, parent=0x5612bb58e930) at ../../source3/smbd/server.c:1381
#9  0x00005612b957eebb in main (argc=3, argv=0x7ffe6fc140c8) at ../../source3/smbd/server.c:2125
```

2. notifyd process
```
Thread 2 (Thread 0x7fb79bc49700 (LWP 57)):
#0  0x00007fb79e0005c0 in __GI___nanosleep (requested_time=requested_time@entry=0x7fb79bc48bf0, remaining=remaining@entry=0x0) at ../sysdeps/unix/sysv/linux/nanosleep.c:28
#1  0x00007fb79e02b414 in usleep (useconds=<optimized out>) at ../sysdeps/posix/usleep.c:32
#2  0x00007fb79e69a86f in metrics_loop (arg=0x0) at ../../source3/smbd/metrics.c:187
#3  0x00007fb79e10ffa3 in start_thread (arg=<optimized out>) at pthread_create.c:486
#4  0x00007fb79e03306f in clone () at ../sysdeps/unix/sysv/linux/x86_64/clone.S:95
Thread 1 (Thread 0x7fb79c37de00 (LWP 55)):
#0  0x00007fb79e03338f in epoll_wait (epfd=4, events=0x7ffe6fc13adc, maxevents=1, timeout=30000) at ../sysdeps/unix/sysv/linux/epoll_wait.c:30
#1  0x00007fb79e396f52 in epoll_event_loop (epoll_ev=0x5612bb592df0, tvalp=0x7ffe6fc13b20) at ../../lib/tevent/tevent_epoll.c:651
#2  0x00007fb79e39790c in epoll_event_loop_once (ev=0x5612bb580610, location=0x7fb79e3989a0 "../../lib/tevent/tevent_req.c:300") at ../../lib/tevent/tevent_epoll.c:938
#3  0x00007fb79e3940a2 in std_event_loop_once (ev=0x5612bb580610, location=0x7fb79e3989a0 "../../lib/tevent/tevent_req.c:300") at ../../lib/tevent/tevent_standard.c:110
#4  0x00007fb79e38b1ac in _tevent_loop_once (ev=0x5612bb580610, location=0x7fb79e3989a0 "../../lib/tevent/tevent_req.c:300") at ../../lib/tevent/tevent.c:825
#5  0x00007fb79e38e3da in tevent_req_poll (req=0x5612bb59cbf0, ev=0x5612bb580610) at ../../lib/tevent/tevent_req.c:300
#6  0x00005612b9579ef5 in smbd_notifyd_init (msg=0x5612bb57a4b0, interactive=false, ppid=0x5612bb58e978) at ../../source3/smbd/server.c:463
#7  0x00005612b957e67e in main (argc=3, argv=0x7ffe6fc140c8) at ../../source3/smbd/server.c:1970
```

3. cleanupd process
```
Thread 2 (Thread 0x7fb79bc49700 (LWP 58)):
#0  0x00007fb79e0005c0 in __GI___nanosleep (requested_time=requested_time@entry=0x7fb79bc48bf0, remaining=remaining@entry=0x0) at ../sysdeps/unix/sysv/linux/nanosleep.c:28
#1  0x00007fb79e02b414 in usleep (useconds=<optimized out>) at ../sysdeps/posix/usleep.c:32
#2  0x00007fb79e69a86f in metrics_loop (arg=0x0) at ../../source3/smbd/metrics.c:187
#3  0x00007fb79e10ffa3 in start_thread (arg=<optimized out>) at pthread_create.c:486
#4  0x00007fb79e03306f in clone () at ../sysdeps/unix/sysv/linux/x86_64/clone.S:95
Thread 1 (Thread 0x7fb79c37de00 (LWP 56)):
#0  0x00007fb79e03338f in epoll_wait (epfd=4, events=0x7ffe6fc13acc, maxevents=1, timeout=30000) at ../sysdeps/unix/sysv/linux/epoll_wait.c:30
#1  0x00007fb79e396f52 in epoll_event_loop (epoll_ev=0x5612bb592df0, tvalp=0x7ffe6fc13b10) at ../../lib/tevent/tevent_epoll.c:651
#2  0x00007fb79e39790c in epoll_event_loop_once (ev=0x5612bb580610, location=0x7fb79e3989a0 "../../lib/tevent/tevent_req.c:300") at ../../lib/tevent/tevent_epoll.c:938
#3  0x00007fb79e3940a2 in std_event_loop_once (ev=0x5612bb580610, location=0x7fb79e3989a0 "../../lib/tevent/tevent_req.c:300") at ../../lib/tevent/tevent_standard.c:110
#4  0x00007fb79e38b1ac in _tevent_loop_once (ev=0x5612bb580610, location=0x7fb79e3989a0 "../../lib/tevent/tevent_req.c:300") at ../../lib/tevent/tevent.c:825
#5  0x00007fb79e38e3da in tevent_req_poll (req=0x5612bb59cb70, ev=0x5612bb580610) at ../../lib/tevent/tevent_req.c:300
#6  0x00005612b957adac in cleanupd_init (msg=0x5612bb57a4b0, interactive=false, ppid=0x5612bb58e960) at ../../source3/smbd/server.c:690
#7  0x00005612b957e6c0 in main (argc=3, argv=0x7ffe6fc140c8) at ../../source3/smbd/server.c:1977
```


# 2. when a new connection arrives, a new process will be created for processing the new connection 
```
root          39       2  0 Jun07 ?        00:00:14 smbd -F --no-process-group
root          55      39  0 Jun07 ?        00:00:14 smbd -F --no-process-group
root          56      39  0 Jun07 ?        00:00:15 smbd -F --no-process-group
root         208      39  0 Jun07 ?        00:15:33 smbd -F --no-process-group
```

无请求正在处理时：
```
Thread 1 (Thread 0x7f034a32be00 (LWP 208)):
#0  0x00007f034bfe138f in epoll_wait (epfd=4, events=0x7ffeab168bfc, maxevents=1, timeout=59999) at ../sysdeps/unix/sysv/linux/epoll_wait.c:30
#1  0x00007f034c344f52 in epoll_event_loop (epoll_ev=0x5559ee59a240, tvalp=0x7ffeab168c40) at ../../lib/tevent/tevent_epoll.c:651
#2  0x00007f034c34590c in epoll_event_loop_once (ev=0x5559ee576610, location=0x7f034c6e5ef8 "../../source3/smbd/smb2_process.c:2015") at ../../lib/tevent/tevent_epoll.c:938
#3  0x00007f034c3420a2 in std_event_loop_once (ev=0x5559ee576610, location=0x7f034c6e5ef8 "../../source3/smbd/smb2_process.c:2015") at ../../lib/tevent/tevent_standard.c:110
#4  0x00007f034c3391ac in _tevent_loop_once (ev=0x5559ee576610, location=0x7f034c6e5ef8 "../../source3/smbd/smb2_process.c:2015") at ../../lib/tevent/tevent.c:825
#5  0x00007f034c3394fe in tevent_common_loop_wait (ev=0x5559ee576610, location=0x7f034c6e5ef8 "../../source3/smbd/smb2_process.c:2015") at ../../lib/tevent/tevent.c:948
#6  0x00007f034c342144 in std_event_loop_wait (ev=0x5559ee576610, location=0x7f034c6e5ef8 "../../source3/smbd/smb2_process.c:2015") at ../../lib/tevent/tevent_standard.c:141
#7  0x00007f034c3395a1 in _tevent_loop_wait (ev=0x5559ee576610, location=0x7f034c6e5ef8 "../../source3/smbd/smb2_process.c:2015") at ../../lib/tevent/tevent.c:967
#8  0x00007f034c5eebaa in smbd_process (ev_ctx=0x5559ee576610, msg_ctx=0x5559ee5704b0, sock_fd=30, interactive=false) at ../../source3/smbd/smb2_process.c:2015
#9  0x00005559ecb9509a in smbd_accept_connection (ev=0x5559ee576610, fde=0x5559ee593270, flags=1, private_data=0x5559ee59a240) at ../../source3/smbd/server.c:1037
#10 0x00007f034c33a469 in tevent_common_invoke_fd_handler (fde=0x5559ee593270, flags=1, removed=0x0) at ../../lib/tevent/tevent_fd.c:142
#11 0x00007f034c345229 in epoll_event_loop (epoll_ev=0x5559ee588df0, tvalp=0x7ffeab168fe0) at ../../lib/tevent/tevent_epoll.c:737
#12 0x00007f034c34590c in epoll_event_loop_once (ev=0x5559ee576610, location=0x5559ecb9a790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent_epoll.c:938
#13 0x00007f034c3420a2 in std_event_loop_once (ev=0x5559ee576610, location=0x5559ecb9a790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent_standard.c:110
#14 0x00007f034c3391ac in _tevent_loop_once (ev=0x5559ee576610, location=0x5559ecb9a790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent.c:825
#15 0x00007f034c3394fe in tevent_common_loop_wait (ev=0x5559ee576610, location=0x5559ecb9a790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent.c:948
#16 0x00007f034c342144 in std_event_loop_wait (ev=0x5559ee576610, location=0x5559ecb9a790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent_standard.c:141
#17 0x00007f034c3395a1 in _tevent_loop_wait (ev=0x5559ee576610, location=0x5559ecb9a790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent.c:967
#18 0x00005559ecb95dc2 in smbd_parent_loop (ev_ctx=0x5559ee576610, parent=0x5559ee584930) at ../../source3/smbd/server.c:1381
#19 0x00005559ecb97ebb in main (argc=3, argv=0x7ffeab169578) at ../../source3/smbd/server.c:2125
```

有请求正在处理时：
```
#0  Client::write (this=0x5559ee70d570, fd=188, buf=0x5559f268a5a0 "", size=1048576, offset=0) at ./src/client/Client.cc:9558
#1  0x00007f03491b9346 in cephwrap_pwrite_send (handle=0x5559ee627580, mem_ctx=0x5559ee73af00, ev=0x5559ee576610, fsp=0x5559ee72f6f0, data=0x5559f268a5a0, n=1048576, offset=0) at ../../source3/modules/vfs_ceph.c:573
#2  0x00007f034c5d7342 in smb_vfs_call_pwrite_send (handle=0x5559ee627580, mem_ctx=0x5559eeb6ff10, ev=0x5559ee576610, fsp=0x5559ee72f6f0, data=0x5559f268a5a0, n=1048576, offset=0) at ../../source3/smbd/vfs.c:1873
#3  0x00007f034c5fc419 in pwrite_fsync_send (mem_ctx=0x5559eeb6fc50, ev=0x5559ee576610, fsp=0x5559ee72f6f0, data=0x5559f268a5a0, n=1048576, offset=0, write_through=false) at ../../source3/smbd/smb2_aio.c:178
#4  0x00007f034c5fd257 in schedule_aio_smb2_write (conn=0x5559ee5b6610, smbreq=0x5559eeb6fb20, fsp=0x5559ee72f6f0, in_offset=0, in_data=..., write_through=false) at ../../source3/smbd/smb2_aio.c:491
#5  0x00007f034c62105c in smbd_smb2_write_send (mem_ctx=0x5559eeb6f4e0, ev=0x5559ee576610, smb2req=0x5559eeb6f4e0, fsp=0x5559ee72f6f0, in_data=..., in_offset=0, in_flags=0) at ../../source3/smbd/smb2_write.c:335
#6  0x00007f034c62059e in smbd_smb2_request_process_write (req=0x5559eeb6f4e0) at ../../source3/smbd/smb2_write.c:112
#7  0x00007f034c6081a3 in smbd_smb2_request_dispatch (req=0x5559eeb6f4e0) at ../../source3/smbd/smb2_server.c:3423
#8  0x00007f034c60d285 in smbd_smb2_io_handler (xconn=0x5559ee59ef10, fde_flags=1) at ../../source3/smbd/smb2_server.c:5025
#9  0x00007f034c60d3b4 in smbd_smb2_connection_handler (ev=0x5559ee576610, fde=0x5559ee59fe90, flags=1, private_data=0x5559ee59ef10) at ../../source3/smbd/smb2_server.c:5063
#10 0x00007f034c33a469 in tevent_common_invoke_fd_handler (fde=0x5559ee59fe90, flags=1, removed=0x0) at ../../lib/tevent/tevent_fd.c:142
#11 0x00007f034c345229 in epoll_event_loop (epoll_ev=0x5559ee59a240, tvalp=0x7ffeab168c40) at ../../lib/tevent/tevent_epoll.c:737
#12 0x00007f034c34590c in epoll_event_loop_once (ev=0x5559ee576610, location=0x7f034c6e5ef8 "../../source3/smbd/smb2_process.c:2015") at ../../lib/tevent/tevent_epoll.c:938
#13 0x00007f034c3420a2 in std_event_loop_once (ev=0x5559ee576610, location=0x7f034c6e5ef8 "../../source3/smbd/smb2_process.c:2015") at ../../lib/tevent/tevent_standard.c:110
#14 0x00007f034c3391ac in _tevent_loop_once (ev=0x5559ee576610, location=0x7f034c6e5ef8 "../../source3/smbd/smb2_process.c:2015") at ../../lib/tevent/tevent.c:825
#15 0x00007f034c3394fe in tevent_common_loop_wait (ev=0x5559ee576610, location=0x7f034c6e5ef8 "../../source3/smbd/smb2_process.c:2015") at ../../lib/tevent/tevent.c:948
#16 0x00007f034c342144 in std_event_loop_wait (ev=0x5559ee576610, location=0x7f034c6e5ef8 "../../source3/smbd/smb2_process.c:2015") at ../../lib/tevent/tevent_standard.c:141
#17 0x00007f034c3395a1 in _tevent_loop_wait (ev=0x5559ee576610, location=0x7f034c6e5ef8 "../../source3/smbd/smb2_process.c:2015") at ../../lib/tevent/tevent.c:967
#18 0x00007f034c5eebaa in smbd_process (ev_ctx=0x5559ee576610, msg_ctx=0x5559ee5704b0, sock_fd=30, interactive=false) at ../../source3/smbd/smb2_process.c:2015
#19 0x00005559ecb9509a in smbd_accept_connection (ev=0x5559ee576610, fde=0x5559ee593270, flags=1, private_data=0x5559ee59a240) at ../../source3/smbd/server.c:1037
#20 0x00007f034c33a469 in tevent_common_invoke_fd_handler (fde=0x5559ee593270, flags=1, removed=0x0) at ../../lib/tevent/tevent_fd.c:142
#21 0x00007f034c345229 in epoll_event_loop (epoll_ev=0x5559ee588df0, tvalp=0x7ffeab168fe0) at ../../lib/tevent/tevent_epoll.c:737
#22 0x00007f034c34590c in epoll_event_loop_once (ev=0x5559ee576610, location=0x5559ecb9a790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent_epoll.c:938
#23 0x00007f034c3420a2 in std_event_loop_once (ev=0x5559ee576610, location=0x5559ecb9a790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent_standard.c:110
#24 0x00007f034c3391ac in _tevent_loop_once (ev=0x5559ee576610, location=0x5559ecb9a790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent.c:825
#25 0x00007f034c3394fe in tevent_common_loop_wait (ev=0x5559ee576610, location=0x5559ecb9a790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent.c:948
#26 0x00007f034c342144 in std_event_loop_wait (ev=0x5559ee576610, location=0x5559ecb9a790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent_standard.c:141
#27 0x00007f034c3395a1 in _tevent_loop_wait (ev=0x5559ee576610, location=0x5559ecb9a790 "../../source3/smbd/server.c:1381") at ../../lib/tevent/tevent.c:967
#28 0x00005559ecb95dc2 in smbd_parent_loop (ev_ctx=0x5559ee576610, parent=0x5559ee584930) at ../../source3/smbd/server.c:1381
#29 0x00005559ecb97ebb in main (argc=3, argv=0x7ffeab169578) at ../../source3/smbd/server.c:2125
```
