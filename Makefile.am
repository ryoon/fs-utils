AUTOMAKE_OPTIONS= foreign
ACLOCAL_AMFLAGS= -I m4

AM_CPPFLAGS= -DUSE_RUMP -I${srcdir}/lib -D'__COPYRIGHT(x)=' -D'__RCSID(x)='
AM_CPPFLAGS+=-D_FILE_OFFSET_BITS=64 -D_XOPEN_SOURCE=500 -D_BSD_SOURCE
AM_CPPFLAGS+=-DMOUNT_NOMAIN

#
# XXX: how do you avoid having to add foo/src.c a billion times?

#
# lib/
#

lib_LTLIBRARIES= libfsu.la

noinst_HEADERS= lib/filesystems.h lib/fs_args.h lib/fsu_alias.h		\
	lib/fsu_compat.h lib/fsu_fts.h lib/fsu_mount.h lib/fsu_utils.h	\
	lib/fts2fsufts.h lib/iodesc.h lib/mntopts.h lib/mount_cd9660.h	\
	lib/mount_efs.h lib/mount_ext2fs.h lib/mount_ffs.h		\
	lib/mount_hfs.h lib/mount_kernfs.h lib/mount_lfs.h		\
	lib/mount_msdos.h lib/mount_nfs.h lib/mount_ntfs.h		\
	lib/mountprog.h lib/mount_smbfs.h lib/mount_sysvbfs.h		\
	lib/mount_tmpfs.h lib/mount_udf.h lib/mount_v7fs.h lib/nb_fs.h	\
	lib/nbstdlib.h lib/nbsysstat.h lib/net.h lib/pathnames.h	\
	lib/rpc.h lib/rpcv2.h lib/rump_syspuffs.h

libfsu_la_SOURCES= lib/fsu_mount.c lib/fsu_alias.c			\
	lib/mount_cd9660.c lib/mount_ext2fs.c lib/mount_hfs.c		\
	lib/mount_msdos.c lib/mount_tmpfs.c lib/mount_efs.c		\
	lib/mount_ffs.c lib/mount_lfs.c lib/mount_ntfs.c		\
	lib/mount_udf.c lib/mount_sysvbfs.c lib/mount_v7fs.c		\
	lib/mount_kernfs.c						\
	lib/pathadj.c lib/fattr.c lib/getmntopts.c lib/fsu_fts.c	\
	lib/fsu_dir.c lib/fsu_file.c lib/fsu_str2arg.c lib/getbsize.c	\
	lib/stat_flags.c

#libfsu_la_AM_CPPFLAGS=	-DMOUNT_NOMAIN

if ENABLE_NFS
AM_CPPFLAGS+=-Ilib/external -Ilib -DNFS -DWITH_NFS -DNO_PMAP_CACHE
libfsu_la_SOURCES+= lib/mount_nfs.c lib/snprintb.c lib/udp_xfer.c \
		    lib/rpc.c lib/net.c lib/getnfsargs_small.c
endif


#
# src/
#

bin_PROGRAMS= fsu_cat fsu_chmod fsu_cp fsu_diff fsu_dir fsu_ecp		\
	fsu_exec fsu_find fsu_ln fsu_ls fsu_mkdir fsu_mv fsu_rm		\
	fsu_rmdir fsu_stat fsu_write fsu_mknod fsu_chflags fsu_du	\
	fsu_mkfifo fsu_touch fsu_chown

#LDFLAGS=-L${TOP}/lib -Wl,-R${TOP}/lib -L${RUMPBASE}/lib -Wl,-R${RUMPBASE}/lib
#OSNAME=	$(shell uname -s)
#ifeq ($(OSNAME),Linux)
#LIBS= -lrumpnet_sockin -lrumpnet_net -lrumpnet -lrumpkern_sys_linux
#endif

binlibs = libfsu.la -lrumpvfs -lrumpdev_disk -lrumpdev -lrump -lrumpuser

# XXX only for Linux, but unconditional now
binlibs+= -lrumpnet_sockin -lrumpnet_net -lrumpnet -lrumpkern_sys_linux


noinst_HEADERS+= src/extern_cp.h src/extern_ls.h src/fsu_flist.h	\
	src/ls.h src/pack_dev.h

fsu_cat_SOURCES= src/fsu_cat.c
fsu_cat_LDADD= $(binlibs)

fsu_chflags_SOURCES= src/chflags.c
fsu_chflags_LDADD= $(binlibs)

fsu_chmod_SOURCES= src/chmod.c
fsu_chmod_LDFLAGS= -Wl,--wrap=chmod,--wrap=lchmod
fsu_chmod_LDADD= $(binlibs)

fsu_chown_SOURCES= src/chown.c
fsu_chown_LDFLAGS= -Wl,--wrap=chown,--wrap=lchown
fsu_chown_LDADD= $(binlibs)

fsu_cp_SOURCES= src/cp.c src/utils_cp.c
fsu_cp_LDADD= $(binlibs)

fsu_diff_SOURCES= src/fsu_diff.c
fsu_diff_LDADD= $(binlibs)

fsu_dir_SOURCES= src/fsu_dir.c
fsu_dir_LDADD= $(binlibs)

fsu_du_SOURCES= src/du.c
fsu_du_LDADD= $(binlibs)

fsu_ecp_SOURCES= src/fsu_ecp.c src/fsu_flist.c
fsu_ecp_LDADD= $(binlibs)

fsu_exec_SOURCES= src/fsu_exec.c
fsu_exec_LDADD= $(binlibs)

fsu_find_SOURCES= src/fsu_find.c
fsu_find_LDADD= $(binlibs)

fsu_ln_SOURCES= src/ln.c
fsu_ln_LDADD= $(binlibs)

fsu_ls_SOURCES= src/cmp.c src/ls.c src/main.c src/print.c src/utils_ls.c
fsu_ls_LDADD= $(binlibs)

fsu_mkdir_SOURCES= src/mkdir.c
fsu_mkdir_LDADD= $(binlibs)

fsu_mkfifo_SOURCES= src/mkfifo.c
fsu_mkfifo_LDADD= $(binlibs)

fsu_mknod_SOURCES= src/mknod.c src/pack_dev.c
fsu_mknod_LDADD= $(binlibs)

fsu_mv_SOURCES= src/fsu_mv.c
fsu_mv_LDADD= $(binlibs)

fsu_rm_SOURCES= src/rm.c
fsu_rm_LDADD= $(binlibs)

fsu_rmdir_SOURCES= src/rmdir.c
fsu_rmdir_LDADD= $(binlibs)

fsu_stat_SOURCES= src/fsu_stat.c
fsu_stat_LDADD= $(binlibs)

fsu_touch_SOURCES= src/fsu_touch.c
fsu_touch_LDADD= $(binlibs)

fsu_write_SOURCES= src/fsu_write.c
fsu_write_LDADD= $(binlibs)