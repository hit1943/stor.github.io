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
