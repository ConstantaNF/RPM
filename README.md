# ****Размещаем свой RPM в своем репозитории**** #

### Описание домашннего задания ###

1. Создать свой RPM пакет (можно взять свое приложение, либо собрать, например,
апач с определенными опциями)
2. Создать свой репозиторий и разместить там ранее собранный RPM

Реализовать это все либо в Vagrant, либо развернуть у себя через NGINX и дать ссылку на репозиторий.

### **Выполнение** ###

Задание выполняется на рабочей станции с ОС Ubuntu 22.04.4 LTS с заранее установленными Vagrant 2.4.1 и VirtualBox 7.0. 
Перед выполнением предварительно подготовлен репозиторий <https://github.com/ConstantaNF/RPM.git>

### **Подготовка окружения** ###

Для развёртывания управляемой ВМ посредством Vagrant создаю Vagrantfile и скрипт для установки необходимых пакетов через `provision`. Cоздаю их в заранее подготовленном каталоге 
`/home/adminkonstantin/RPM`.

Стартую ВМ:

```
adminkonstantin@2OSUbuntu:~/RPM$ vagrant up
Bringing machine 'rpm' up with 'virtualbox' provider...
==> rpm: Importing base box 'generic/centos8s'...
==> rpm: Matching MAC address for NAT networking...
==> rpm: Checking if box 'generic/centos8s' version '4.3.12' is up to date...
==> rpm: Setting the name of the VM: RPM_rpm_1713168504807_13471
==> rpm: Fixed port collision for 22 => 2222. Now on port 2200.
==> rpm: Clearing any previously set network interfaces...
==> rpm: Preparing network interfaces based on configuration...
    rpm: Adapter 1: nat
==> rpm: Forwarding ports...
    rpm: 22 (guest) => 2200 (host) (adapter 1)
==> rpm: Running 'pre-boot' VM customizations...
==> rpm: Booting VM...
==> rpm: Waiting for machine to boot. This may take a few minutes...
    rpm: SSH address: 127.0.0.1:2200
    rpm: SSH username: vagrant
    rpm: SSH auth method: private key
    rpm: 
    rpm: Vagrant insecure key detected. Vagrant will automatically replace
    rpm: this with a newly generated keypair for better security.
    rpm: 
    rpm: Inserting generated public key within guest...
    rpm: Removing insecure key from the guest if it's present...
    rpm: Key inserted! Disconnecting and reconnecting using new SSH key...
==> rpm: Machine booted and ready!
==> rpm: Checking for guest additions in VM...
    rpm: The guest additions on this VM do not match the installed version of
    rpm: VirtualBox! In most cases this is fine, but in rare cases it can
    rpm: prevent things such as shared folders from working properly. If you see
    rpm: shared folder errors, please make sure the guest additions within the
    rpm: virtual machine match the version of VirtualBox you have installed on
    rpm: your host and reload your VM.
    rpm: 
    rpm: Guest Additions Version: 6.1.30 r148432
    rpm: VirtualBox Version: 7.0
==> rpm: Setting hostname...
==> rpm: Running provisioner: shell...
    rpm: Running: /tmp/vagrant-shell20240415-10237-cbs8d9.sh
    rpm: CentOS Stream 8 - AppStream                     5.7 MB/s |  28 MB     00:04
    rpm: CentOS Stream 8 - BaseOS                        4.4 MB/s |  10 MB     00:02
    rpm: CentOS Stream 8 - Extras                         18 kB/s |  18 kB     00:00
    rpm: CentOS Stream 8 - Extras common packages         12 kB/s | 7.7 kB     00:00
    rpm: Extra Packages for Enterprise Linux 8 - x86_64  3.7 MB/s |  16 MB     00:04
    rpm: Extra Packages for Enterprise Linux 8 - Next -  217 kB/s | 368 kB     00:01
    rpm: Package wget-1.19.5-11.el8.x86_64 is already installed.
    rpm: Package yum-utils-4.0.21-24.el8.noarch is already installed.
    rpm: Package gcc-8.5.0-21.el8.x86_64 is already installed.
    rpm: Dependencies resolved.
    rpm: ================================================================================
    rpm:  Package                      Arch     Version                Repository   Size
    rpm: ================================================================================
    rpm: Installing:
    rpm:  createrepo_c                 x86_64   0.17.7-6.el8           appstream    89 k
    rpm:  redhat-lsb-core              x86_64   4.1-47.el8             appstream    46 k
    rpm:  rpm-build                    x86_64   4.14.3-31.el8          appstream   185 k
    rpm:  rpmdevtools                  noarch   8.10-8.el8             appstream    87 k
    rpm: Upgrading:
    rpm:  dnf-plugins-core             noarch   4.0.21-25.el8          baseos       77 k
    rpm:  python3-dnf-plugins-core     noarch   4.0.21-25.el8          baseos      280 k
    rpm:  yum-utils                    noarch   4.0.21-25.el8          baseos       80 k
    rpm: Installing dependencies:
    rpm:  annobin                      x86_64   11.13-2.el8            baseos      972 k
    rpm:  at                           x86_64   3.1.20-12.el8          baseos       81 k
    rpm:  avahi-libs                   x86_64   0.7-27.el8             baseos       62 k
    rpm:  bc                           x86_64   1.07.1-5.el8           baseos      129 k
    rpm:  createrepo_c-libs            x86_64   0.17.7-6.el8           appstream   116 k
    rpm:  cups-client                  x86_64   1:2.2.6-57.el8         appstream   175 k
    rpm:  cups-libs                    x86_64   1:2.2.6-57.el8         baseos      436 k
    rpm:  drpm                         x86_64   0.4.1-3.el8            appstream    68 k
    rpm:  dwz                          x86_64   0.12-10.el8            appstream   109 k
    rpm:  ed                           x86_64   1.14.2-4.el8           baseos       82 k
    rpm:  efi-srpm-macros              noarch   3-3.el8                appstream    22 k
    rpm:  elfutils                     x86_64   0.190-2.el8            baseos      581 k
    rpm:  esmtp                        x86_64   1.2-15.el8             epel         57 k
    rpm:  gc                           x86_64   7.6.4-3.el8            appstream   109 k
    rpm:  gcc-plugin-annobin           x86_64   8.5.0-21.el8           baseos       36 k
    rpm:  gdb-headless                 x86_64   8.2-20.el8             appstream   3.7 M
    rpm:  ghc-srpm-macros              noarch   1.4.2-7.el8            appstream   9.3 k
    rpm:  go-srpm-macros               noarch   2-17.el8               appstream    13 k
    rpm:  guile                        x86_64   5:2.0.14-7.el8         appstream   3.5 M
    rpm:  libatomic_ops                x86_64   7.6.2-3.el8            appstream    38 k
    rpm:  libbabeltrace                x86_64   1.5.4-4.el8            baseos      200 k
    rpm:  libesmtp                     x86_64   1.0.6-18.el8           epel         70 k
    rpm:  libipt                       x86_64   1.6.1-8.el8            appstream    50 k
    rpm:  liblockfile                  x86_64   1.14-2.el8             appstream    32 k
    rpm:  libtool-ltdl                 x86_64   2.4.6-25.el8           baseos       58 k
    rpm:  mailx                        x86_64   12.5-29.el8            baseos      257 k
    rpm:  ncurses-compat-libs          x86_64   6.1-10.20180224.el8    baseos      335 k
    rpm:  nspr                         x86_64   4.35.0-1.el8           appstream   143 k
    rpm:  nss                          x86_64   3.90.0-6.el8           appstream   753 k
    rpm:  nss-softokn                  x86_64   3.90.0-6.el8           appstream   1.2 M
    rpm:  nss-softokn-freebl           x86_64   3.90.0-6.el8           appstream   376 k
    rpm:  nss-sysinit                  x86_64   3.90.0-6.el8           appstream    75 k
    rpm:  nss-util                     x86_64   3.90.0-6.el8           appstream   140 k
    rpm:  ocaml-srpm-macros            noarch   5-4.el8                appstream   9.4 k
    rpm:  openblas-srpm-macros         noarch   2-2.el8                appstream   7.9 k
    rpm:  perl-srpm-macros             noarch   1-25.el8               appstream    11 k
    rpm:  python-rpm-macros            noarch   3-45.el8               baseos       16 k
    rpm:  python-srpm-macros           noarch   3-45.el8               baseos       16 k
    rpm:  python3-rpm-macros           noarch   3-45.el8               baseos       15 k
    rpm:  qt5-srpm-macros              noarch   5.15.3-1.el8           appstream    11 k
    rpm:  redhat-lsb-submod-security   x86_64   4.1-47.el8             appstream    22 k
    rpm:  redhat-rpm-config            noarch   131-1.el8              baseos       94 k
    rpm:  rust-srpm-macros             noarch   5-2.el8                appstream   9.2 k
    rpm:  spax                         x86_64   1.5.3-13.el8           baseos      217 k
    rpm:  time                         x86_64   1.9-3.el8              baseos       54 k
    rpm:  unzip                        x86_64   6.0-46.el8             baseos      196 k
    rpm:  util-linux-user              x86_64   2.32.1-43.el8          baseos      103 k
    rpm:  zip                          x86_64   3.0-23.el8             baseos      270 k
    rpm:  zstd                         x86_64   1.4.4-1.el8            appstream   393 k
    rpm: 
    rpm: Transaction Summary
    rpm: ================================================================================
    rpm: Install  53 Packages
    rpm: Upgrade   3 Packages
    rpm: 
    rpm: Total download size: 16 M
    rpm: Downloading Packages:
    rpm: (1/56): createrepo_c-0.17.7-6.el8.x86_64.rpm    298 kB/s |  89 kB     00:00
    rpm: (2/56): createrepo_c-libs-0.17.7-6.el8.x86_64.r 339 kB/s | 116 kB     00:00
    rpm: (3/56): drpm-0.4.1-3.el8.x86_64.rpm             1.1 MB/s |  68 kB     00:00
    rpm: (4/56): cups-client-2.2.6-57.el8.x86_64.rpm     473 kB/s | 175 kB     00:00
    rpm: (5/56): dwz-0.12-10.el8.x86_64.rpm              1.4 MB/s | 109 kB     00:00
    rpm: (6/56): efi-srpm-macros-3-3.el8.noarch.rpm      325 kB/s |  22 kB     00:00
    rpm: (7/56): gc-7.6.4-3.el8.x86_64.rpm               1.7 MB/s | 109 kB     00:00
    rpm: (8/56): ghc-srpm-macros-1.4.2-7.el8.noarch.rpm  169 kB/s | 9.3 kB     00:00
    rpm: (9/56): go-srpm-macros-2-17.el8.noarch.rpm      238 kB/s |  13 kB     00:00
    rpm: (10/56): libatomic_ops-7.6.2-3.el8.x86_64.rpm   520 kB/s |  38 kB     00:00
    rpm: (11/56): gdb-headless-8.2-20.el8.x86_64.rpm     5.2 MB/s | 3.7 MB     00:00
    rpm: (12/56): libipt-1.6.1-8.el8.x86_64.rpm           85 kB/s |  50 kB     00:00
    rpm: (13/56): liblockfile-1.14-2.el8.x86_64.rpm      552 kB/s |  32 kB     00:00
    rpm: (14/56): nspr-4.35.0-1.el8.x86_64.rpm           1.3 MB/s | 143 kB     00:00
    rpm: (15/56): guile-2.0.14-7.el8.x86_64.rpm          3.7 MB/s | 3.5 MB     00:00
    rpm: (16/56): nss-3.90.0-6.el8.x86_64.rpm            2.6 MB/s | 753 kB     00:00
    rpm: (17/56): nss-sysinit-3.90.0-6.el8.x86_64.rpm    1.2 MB/s |  75 kB     00:00
    rpm: (18/56): nss-softokn-freebl-3.90.0-6.el8.x86_64 2.6 MB/s | 376 kB     00:00
    rpm: (19/56): nss-util-3.90.0-6.el8.x86_64.rpm       2.1 MB/s | 140 kB     00:00
    rpm: (20/56): ocaml-srpm-macros-5-4.el8.noarch.rpm   187 kB/s | 9.4 kB     00:00
    rpm: (21/56): openblas-srpm-macros-2-2.el8.noarch.rp 159 kB/s | 7.9 kB     00:00
    rpm: (22/56): perl-srpm-macros-1-25.el8.noarch.rpm   210 kB/s |  11 kB     00:00
    rpm: (23/56): qt5-srpm-macros-5.15.3-1.el8.noarch.rp 106 kB/s |  11 kB     00:00
    rpm: (24/56): redhat-lsb-core-4.1-47.el8.x86_64.rpm  455 kB/s |  46 kB     00:00
    rpm: (25/56): nss-softokn-3.90.0-6.el8.x86_64.rpm    2.1 MB/s | 1.2 MB     00:00
    rpm: (26/56): redhat-lsb-submod-security-4.1-47.el8. 357 kB/s |  22 kB     00:00
    rpm: (27/56): rpm-build-4.14.3-31.el8.x86_64.rpm     2.5 MB/s | 185 kB     00:00
    rpm: (28/56): rpmdevtools-8.10-8.el8.noarch.rpm      1.2 MB/s |  87 kB     00:00
    rpm: (29/56): rust-srpm-macros-5-2.el8.noarch.rpm    136 kB/s | 9.2 kB     00:00
    rpm: (30/56): zstd-1.4.4-1.el8.x86_64.rpm            3.4 MB/s | 393 kB     00:00
    rpm: (31/56): at-3.1.20-12.el8.x86_64.rpm            286 kB/s |  81 kB     00:00
    rpm: (32/56): avahi-libs-0.7-27.el8.x86_64.rpm       266 kB/s |  62 kB     00:00
    rpm: (33/56): bc-1.07.1-5.el8.x86_64.rpm             1.3 MB/s | 129 kB     00:00
    rpm: (34/56): cups-libs-2.2.6-57.el8.x86_64.rpm      2.5 MB/s | 436 kB     00:00
    rpm: (35/56): ed-1.14.2-4.el8.x86_64.rpm             996 kB/s |  82 kB     00:00
    rpm: (36/56): annobin-11.13-2.el8.x86_64.rpm         1.9 MB/s | 972 kB     00:00
    rpm: (37/56): gcc-plugin-annobin-8.5.0-21.el8.x86_64 489 kB/s |  36 kB     00:00
    rpm: (38/56): elfutils-0.190-2.el8.x86_64.rpm        4.6 MB/s | 581 kB     00:00
    rpm: (39/56): libtool-ltdl-2.4.6-25.el8.x86_64.rpm   1.0 MB/s |  58 kB     00:00
    rpm: (40/56): mailx-12.5-29.el8.x86_64.rpm           3.2 MB/s | 257 kB     00:00
    rpm: (41/56): ncurses-compat-libs-6.1-10.20180224.el 2.7 MB/s | 335 kB     00:00
    rpm: (42/56): python-rpm-macros-3-45.el8.noarch.rpm  193 kB/s |  16 kB     00:00
    rpm: (43/56): python-srpm-macros-3-45.el8.noarch.rpm 324 kB/s |  16 kB     00:00
    rpm: (44/56): python3-rpm-macros-3-45.el8.noarch.rpm 319 kB/s |  15 kB     00:00
    rpm: (45/56): redhat-rpm-config-131-1.el8.noarch.rpm 1.5 MB/s |  94 kB     00:00
    rpm: (46/56): spax-1.5.3-13.el8.x86_64.rpm           2.9 MB/s | 217 kB     00:00
    rpm: (47/56): libbabeltrace-1.5.4-4.el8.x86_64.rpm   471 kB/s | 200 kB     00:00
    rpm: (48/56): time-1.9-3.el8.x86_64.rpm              933 kB/s |  54 kB     00:00
    rpm: (49/56): unzip-6.0-46.el8.x86_64.rpm            2.6 MB/s | 196 kB     00:00
    rpm: (50/56): util-linux-user-2.32.1-43.el8.x86_64.r 1.2 MB/s | 103 kB     00:00
    rpm: (51/56): zip-3.0-23.el8.x86_64.rpm              2.7 MB/s | 270 kB     00:00
    rpm: (52/56): dnf-plugins-core-4.0.21-25.el8.noarch. 1.3 MB/s |  77 kB     00:00
    rpm: (53/56): python3-dnf-plugins-core-4.0.21-25.el8 2.1 MB/s | 280 kB     00:00
    rpm: (54/56): yum-utils-4.0.21-25.el8.noarch.rpm     1.3 MB/s |  80 kB     00:00
    rpm: (55/56): esmtp-1.2-15.el8.x86_64.rpm             89 kB/s |  57 kB     00:00
    rpm: (56/56): libesmtp-1.0.6-18.el8.x86_64.rpm       110 kB/s |  70 kB     00:00
    rpm: --------------------------------------------------------------------------------
    rpm: Total                                           3.4 MB/s |  16 MB     00:04
    rpm: Running transaction check
    rpm: Transaction check succeeded.
    rpm: Running transaction test
    rpm: Transaction test succeeded.
    rpm: Running transaction
    rpm:   Preparing        :                                                        1/1
    rpm:   Running scriptlet: nspr-4.35.0-1.el8.x86_64                               1/1
    rpm:   Installing       : nspr-4.35.0-1.el8.x86_64                              1/59
    rpm:   Running scriptlet: nspr-4.35.0-1.el8.x86_64                              1/59
    rpm:   Installing       : nss-util-3.90.0-6.el8.x86_64                          2/59
    rpm:   Installing       : python-srpm-macros-3-45.el8.noarch                    3/59
    rpm:   Installing       : unzip-6.0-46.el8.x86_64                               4/59
    rpm:   Installing       : avahi-libs-0.7-27.el8.x86_64                          5/59
    rpm:   Installing       : drpm-0.4.1-3.el8.x86_64                               6/59
    rpm:   Installing       : createrepo_c-libs-0.17.7-6.el8.x86_64                 7/59
    rpm:   Installing       : cups-libs-1:2.2.6-57.el8.x86_64                       8/59
    rpm:   Installing       : cups-client-1:2.2.6-57.el8.x86_64                     9/59
    rpm:   Running scriptlet: cups-client-1:2.2.6-57.el8.x86_64                     9/59
    rpm:   Installing       : zip-3.0-23.el8.x86_64                                10/59
    rpm:   Installing       : python-rpm-macros-3-45.el8.noarch                    11/59
    rpm:   Installing       : python3-rpm-macros-3-45.el8.noarch                   12/59
    rpm:   Installing       : nss-softokn-freebl-3.90.0-6.el8.x86_64               13/59
    rpm:   Installing       : nss-softokn-3.90.0-6.el8.x86_64                      14/59
    rpm:   Installing       : nss-3.90.0-6.el8.x86_64                              15/59
    rpm:   Installing       : nss-sysinit-3.90.0-6.el8.x86_64                      16/59
    rpm:   Installing       : redhat-lsb-submod-security-4.1-47.el8.x86_64         17/59
    rpm:   Upgrading        : python3-dnf-plugins-core-4.0.21-25.el8.noarch        18/59
    rpm:   Upgrading        : dnf-plugins-core-4.0.21-25.el8.noarch                19/59
    rpm:   Installing       : libesmtp-1.0.6-18.el8.x86_64                         20/59
    rpm:   Installing       : util-linux-user-2.32.1-43.el8.x86_64                 21/59
    rpm:   Installing       : time-1.9-3.el8.x86_64                                22/59
    rpm:   Running scriptlet: time-1.9-3.el8.x86_64                                22/59
    rpm:   Installing       : spax-1.5.3-13.el8.x86_64                             23/59
    rpm:   Running scriptlet: spax-1.5.3-13.el8.x86_64                             23/59
    rpm:   Installing       : ncurses-compat-libs-6.1-10.20180224.el8.x86_64       24/59
    rpm:   Installing       : mailx-12.5-29.el8.x86_64                             25/59
    rpm:   Installing       : libtool-ltdl-2.4.6-25.el8.x86_64                     26/59
    rpm:   Running scriptlet: libtool-ltdl-2.4.6-25.el8.x86_64                     26/59
    rpm:   Installing       : libbabeltrace-1.5.4-4.el8.x86_64                     27/59
    rpm:   Running scriptlet: libbabeltrace-1.5.4-4.el8.x86_64                     27/59
    rpm:   Installing       : gcc-plugin-annobin-8.5.0-21.el8.x86_64               28/59
    rpm:   Installing       : elfutils-0.190-2.el8.x86_64                          29/59
    rpm:   Installing       : ed-1.14.2-4.el8.x86_64                               30/59
    rpm:   Running scriptlet: ed-1.14.2-4.el8.x86_64                               30/59
    rpm:   Installing       : bc-1.07.1-5.el8.x86_64                               31/59
    rpm:   Running scriptlet: bc-1.07.1-5.el8.x86_64                               31/59
    rpm:   Installing       : at-3.1.20-12.el8.x86_64                              32/59
    rpm:   Running scriptlet: at-3.1.20-12.el8.x86_64                              32/59
    rpm:   Installing       : annobin-11.13-2.el8.x86_64                           33/59
    rpm:   Installing       : zstd-1.4.4-1.el8.x86_64                              34/59
    rpm:   Installing       : rust-srpm-macros-5-2.el8.noarch                      35/59
    rpm:   Installing       : qt5-srpm-macros-5.15.3-1.el8.noarch                  36/59
    rpm:   Installing       : perl-srpm-macros-1-25.el8.noarch                     37/59
    rpm:   Installing       : openblas-srpm-macros-2-2.el8.noarch                  38/59
    rpm:   Installing       : ocaml-srpm-macros-5-4.el8.noarch                     39/59
    rpm:   Installing       : liblockfile-1.14-2.el8.x86_64                        40/59
    rpm:   Running scriptlet: liblockfile-1.14-2.el8.x86_64                        40/59
    rpm:   Installing       : esmtp-1.2-15.el8.x86_64                              41/59
    rpm:   Running scriptlet: esmtp-1.2-15.el8.x86_64                              41/59
    rpm:   Installing       : libipt-1.6.1-8.el8.x86_64                            42/59
    rpm:   Installing       : libatomic_ops-7.6.2-3.el8.x86_64                     43/59
    rpm:   Installing       : gc-7.6.4-3.el8.x86_64                                44/59
    rpm:   Installing       : guile-5:2.0.14-7.el8.x86_64                          45/59
    rpm:   Running scriptlet: guile-5:2.0.14-7.el8.x86_64                          45/59
    rpm:   Installing       : gdb-headless-8.2-20.el8.x86_64                       46/59
    rpm:   Installing       : go-srpm-macros-2-17.el8.noarch                       47/59
    rpm:   Installing       : ghc-srpm-macros-1.4.2-7.el8.noarch                   48/59
    rpm:   Installing       : efi-srpm-macros-3-3.el8.noarch                       49/59
    rpm:   Installing       : dwz-0.12-10.el8.x86_64                               50/59
    rpm:   Installing       : redhat-rpm-config-131-1.el8.noarch                   51/59
    rpm:   Running scriptlet: redhat-rpm-config-131-1.el8.noarch                   51/59
    rpm:   Installing       : rpm-build-4.14.3-31.el8.x86_64                       52/59
    rpm:   Installing       : rpmdevtools-8.10-8.el8.noarch                        53/59
    rpm:   Installing       : redhat-lsb-core-4.1-47.el8.x86_64                    54/59
    rpm:   Upgrading        : yum-utils-4.0.21-25.el8.noarch                       55/59
    rpm:   Installing       : createrepo_c-0.17.7-6.el8.x86_64                     56/59
    rpm:   Cleanup          : yum-utils-4.0.21-24.el8.noarch                       57/59
    rpm:   Cleanup          : dnf-plugins-core-4.0.21-24.el8.noarch                58/59
    rpm:   Cleanup          : python3-dnf-plugins-core-4.0.21-24.el8.noarch        59/59
    rpm:   Running scriptlet: nss-3.90.0-6.el8.x86_64                              59/59
    rpm:   Running scriptlet: guile-5:2.0.14-7.el8.x86_64                          59/59
    rpm:   Running scriptlet: python3-dnf-plugins-core-4.0.21-24.el8.noarch        59/59
    rpm:   Verifying        : createrepo_c-0.17.7-6.el8.x86_64                      1/59
    rpm:   Verifying        : createrepo_c-libs-0.17.7-6.el8.x86_64                 2/59
    rpm:   Verifying        : cups-client-1:2.2.6-57.el8.x86_64                     3/59
    rpm:   Verifying        : drpm-0.4.1-3.el8.x86_64                               4/59
    rpm:   Verifying        : dwz-0.12-10.el8.x86_64                                5/59
    rpm:   Verifying        : efi-srpm-macros-3-3.el8.noarch                        6/59
    rpm:   Verifying        : gc-7.6.4-3.el8.x86_64                                 7/59
    rpm:   Verifying        : gdb-headless-8.2-20.el8.x86_64                        8/59
    rpm:   Verifying        : ghc-srpm-macros-1.4.2-7.el8.noarch                    9/59
    rpm:   Verifying        : go-srpm-macros-2-17.el8.noarch                       10/59
    rpm:   Verifying        : guile-5:2.0.14-7.el8.x86_64                          11/59
    rpm:   Verifying        : libatomic_ops-7.6.2-3.el8.x86_64                     12/59
    rpm:   Verifying        : libipt-1.6.1-8.el8.x86_64                            13/59
    rpm:   Verifying        : liblockfile-1.14-2.el8.x86_64                        14/59
    rpm:   Verifying        : nspr-4.35.0-1.el8.x86_64                             15/59
    rpm:   Verifying        : nss-3.90.0-6.el8.x86_64                              16/59
    rpm:   Verifying        : nss-softokn-3.90.0-6.el8.x86_64                      17/59
    rpm:   Verifying        : nss-softokn-freebl-3.90.0-6.el8.x86_64               18/59
    rpm:   Verifying        : nss-sysinit-3.90.0-6.el8.x86_64                      19/59
    rpm:   Verifying        : nss-util-3.90.0-6.el8.x86_64                         20/59
    rpm:   Verifying        : ocaml-srpm-macros-5-4.el8.noarch                     21/59
    rpm:   Verifying        : openblas-srpm-macros-2-2.el8.noarch                  22/59
    rpm:   Verifying        : perl-srpm-macros-1-25.el8.noarch                     23/59
    rpm:   Verifying        : qt5-srpm-macros-5.15.3-1.el8.noarch                  24/59
    rpm:   Verifying        : redhat-lsb-core-4.1-47.el8.x86_64                    25/59
    rpm:   Verifying        : redhat-lsb-submod-security-4.1-47.el8.x86_64         26/59
    rpm:   Verifying        : rpm-build-4.14.3-31.el8.x86_64                       27/59
    rpm:   Verifying        : rpmdevtools-8.10-8.el8.noarch                        28/59
    rpm:   Verifying        : rust-srpm-macros-5-2.el8.noarch                      29/59
    rpm:   Verifying        : zstd-1.4.4-1.el8.x86_64                              30/59
    rpm:   Verifying        : annobin-11.13-2.el8.x86_64                           31/59
    rpm:   Verifying        : at-3.1.20-12.el8.x86_64                              32/59
    rpm:   Verifying        : avahi-libs-0.7-27.el8.x86_64                         33/59
    rpm:   Verifying        : bc-1.07.1-5.el8.x86_64                               34/59
    rpm:   Verifying        : cups-libs-1:2.2.6-57.el8.x86_64                      35/59
    rpm:   Verifying        : ed-1.14.2-4.el8.x86_64                               36/59
    rpm:   Verifying        : elfutils-0.190-2.el8.x86_64                          37/59
    rpm:   Verifying        : gcc-plugin-annobin-8.5.0-21.el8.x86_64               38/59
    rpm:   Verifying        : libbabeltrace-1.5.4-4.el8.x86_64                     39/59
    rpm:   Verifying        : libtool-ltdl-2.4.6-25.el8.x86_64                     40/59
    rpm:   Verifying        : mailx-12.5-29.el8.x86_64                             41/59
    rpm:   Verifying        : ncurses-compat-libs-6.1-10.20180224.el8.x86_64       42/59
    rpm:   Verifying        : python-rpm-macros-3-45.el8.noarch                    43/59
    rpm:   Verifying        : python-srpm-macros-3-45.el8.noarch                   44/59
    rpm:   Verifying        : python3-rpm-macros-3-45.el8.noarch                   45/59
    rpm:   Verifying        : redhat-rpm-config-131-1.el8.noarch                   46/59
    rpm:   Verifying        : spax-1.5.3-13.el8.x86_64                             47/59
    rpm:   Verifying        : time-1.9-3.el8.x86_64                                48/59
    rpm:   Verifying        : unzip-6.0-46.el8.x86_64                              49/59
    rpm:   Verifying        : util-linux-user-2.32.1-43.el8.x86_64                 50/59
    rpm:   Verifying        : zip-3.0-23.el8.x86_64                                51/59
    rpm:   Verifying        : esmtp-1.2-15.el8.x86_64                              52/59
    rpm:   Verifying        : libesmtp-1.0.6-18.el8.x86_64                         53/59
    rpm:   Verifying        : dnf-plugins-core-4.0.21-25.el8.noarch                54/59
    rpm:   Verifying        : dnf-plugins-core-4.0.21-24.el8.noarch                55/59
    rpm:   Verifying        : python3-dnf-plugins-core-4.0.21-25.el8.noarch        56/59
    rpm:   Verifying        : python3-dnf-plugins-core-4.0.21-24.el8.noarch        57/59
    rpm:   Verifying        : yum-utils-4.0.21-25.el8.noarch                       58/59
    rpm:   Verifying        : yum-utils-4.0.21-24.el8.noarch                       59/59
    rpm: 
    rpm: Upgraded:
    rpm:   dnf-plugins-core-4.0.21-25.el8.noarch
    rpm:   python3-dnf-plugins-core-4.0.21-25.el8.noarch
    rpm:   yum-utils-4.0.21-25.el8.noarch
    rpm: Installed:
    rpm:   annobin-11.13-2.el8.x86_64
    rpm:   at-3.1.20-12.el8.x86_64
    rpm:   avahi-libs-0.7-27.el8.x86_64
    rpm:   bc-1.07.1-5.el8.x86_64
    rpm:   createrepo_c-0.17.7-6.el8.x86_64
    rpm:   createrepo_c-libs-0.17.7-6.el8.x86_64
    rpm:   cups-client-1:2.2.6-57.el8.x86_64
    rpm:   cups-libs-1:2.2.6-57.el8.x86_64
    rpm:   drpm-0.4.1-3.el8.x86_64
    rpm:   dwz-0.12-10.el8.x86_64
    rpm:   ed-1.14.2-4.el8.x86_64
    rpm:   efi-srpm-macros-3-3.el8.noarch
    rpm:   elfutils-0.190-2.el8.x86_64
    rpm:   esmtp-1.2-15.el8.x86_64
    rpm:   gc-7.6.4-3.el8.x86_64
    rpm:   gcc-plugin-annobin-8.5.0-21.el8.x86_64
    rpm:   gdb-headless-8.2-20.el8.x86_64
    rpm:   ghc-srpm-macros-1.4.2-7.el8.noarch
    rpm:   go-srpm-macros-2-17.el8.noarch
    rpm:   guile-5:2.0.14-7.el8.x86_64
    rpm:   libatomic_ops-7.6.2-3.el8.x86_64
    rpm:   libbabeltrace-1.5.4-4.el8.x86_64
    rpm:   libesmtp-1.0.6-18.el8.x86_64
    rpm:   libipt-1.6.1-8.el8.x86_64
    rpm:   liblockfile-1.14-2.el8.x86_64
    rpm:   libtool-ltdl-2.4.6-25.el8.x86_64
    rpm:   mailx-12.5-29.el8.x86_64
    rpm:   ncurses-compat-libs-6.1-10.20180224.el8.x86_64
    rpm:   nspr-4.35.0-1.el8.x86_64
    rpm:   nss-3.90.0-6.el8.x86_64
    rpm:   nss-softokn-3.90.0-6.el8.x86_64
    rpm:   nss-softokn-freebl-3.90.0-6.el8.x86_64
    rpm:   nss-sysinit-3.90.0-6.el8.x86_64
    rpm:   nss-util-3.90.0-6.el8.x86_64
    rpm:   ocaml-srpm-macros-5-4.el8.noarch
    rpm:   openblas-srpm-macros-2-2.el8.noarch
    rpm:   perl-srpm-macros-1-25.el8.noarch
    rpm:   python-rpm-macros-3-45.el8.noarch
    rpm:   python-srpm-macros-3-45.el8.noarch
    rpm:   python3-rpm-macros-3-45.el8.noarch
    rpm:   qt5-srpm-macros-5.15.3-1.el8.noarch
    rpm:   redhat-lsb-core-4.1-47.el8.x86_64
    rpm:   redhat-lsb-submod-security-4.1-47.el8.x86_64
    rpm:   redhat-rpm-config-131-1.el8.noarch
    rpm:   rpm-build-4.14.3-31.el8.x86_64
    rpm:   rpmdevtools-8.10-8.el8.noarch
    rpm:   rust-srpm-macros-5-2.el8.noarch
    rpm:   spax-1.5.3-13.el8.x86_64
    rpm:   time-1.9-3.el8.x86_64
    rpm:   unzip-6.0-46.el8.x86_64
    rpm:   util-linux-user-2.32.1-43.el8.x86_64
    rpm:   zip-3.0-23.el8.x86_64
    rpm:   zstd-1.4.4-1.el8.x86_64
    rpm: 
    rpm: Complete!
```

Подключаюсь к созданной ВМ по ssh:

```
adminkonstantin@2OSUbuntu:~/RPM$ vagrant ssh
[vagrant@rpm ~]$ 
```

Использую УЗ root:

```
[vagrant@rpm ~]$ sudo -i
[root@rpm ~]# 
```

### **Создать свой RPM пакет** ###

Для примера возьмем пакет NGINX и соберем его с поддержкой openssl.
Загрузим SRPM пакет NGINX для дальнейшей работы над ним:

```
[root@rpm ~]# wget https://nginx.org/packages/centos/8/SRPMS/nginx-1.20.2-1.el8.ngx.src.rpm
--2024-04-15 08:45:52--  https://nginx.org/packages/centos/8/SRPMS/nginx-1.20.2-1.el8.ngx.src.rpm
Resolving nginx.org (nginx.org)... 3.125.197.172, 52.58.199.22, 2a05:d014:5c0:2600::6, ...
Connecting to nginx.org (nginx.org)|3.125.197.172|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 1086865 (1.0M) [application/x-redhat-package-manager]
Saving to: 'nginx-1.20.2-1.el8.ngx.src.rpm'

nginx-1.20.2-1.el8.ngx.src.rpm                   100%[==========================================================================================================>]   1.04M  3.88MB/s    in 0.3s    

2024-04-15 08:45:53 (3.88 MB/s) - 'nginx-1.20.2-1.el8.ngx.src.rpm' saved [1086865/1086865]
```

Устанавливаем скачаный пакет:

```
[root@rpm ~]# rpm -i nginx-1.*
```

При установке этого пакета в домашней директории создается древо каталогов для сборки:

```
[root@rpm ~]# ls -l
total 1064
-rw-r--r--. 1 root root 1086865 Nov 16  2021 nginx-1.20.2-1.el8.ngx.src.rpm
drwxr-xr-x. 4 root root      34 Apr 15 09:00 rpmbuild
```

Также нужно скачать и разархивировать последний исходник для openssl - он потребуется при сборке:

```
[root@rpm ~]# wget https://www.openssl.org/source/openssl-1.1.1w.tar.gz
--2024-04-15 09:57:43--  https://www.openssl.org/source/openssl-1.1.1w.tar.gz
Resolving www.openssl.org (www.openssl.org)... 34.36.58.177, 2600:1901:0:1812::
Connecting to www.openssl.org (www.openssl.org)|34.36.58.177|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 9893384 (9.4M) [application/x-tar]
Saving to: 'openssl-1.1.1w.tar.gz'

openssl-1.1.1w.tar.gz                          100%[===================================================================================================>]   9.43M  6.79MB/s    in 1.4s    

2024-04-15 09:57:45 (6.79 MB/s) - 'openssl-1.1.1w.tar.gz' saved [9893384/9893384]
```

```
[root@rpm ~]# tar -xvf openssl-1.1.1w.tar.gz
openssl-1.1.1w/
openssl-1.1.1w/ACKNOWLEDGEMENTS
openssl-1.1.1w/AUTHORS
openssl-1.1.1w/CHANGES
openssl-1.1.1w/CONTRIBUTING
openssl-1.1.1w/Configurations/
openssl-1.1.1w/Configurations/00-base-templates.conf
openssl-1.1.1w/Configurations/10-main.conf
openssl-1.1.1w/Configurations/15-android.conf
openssl-1.1.1w/Configurations/15-ios.conf
openssl-1.1.1w/Configurations/50-djgpp.conf
openssl-1.1.1w/Configurations/50-haiku.conf
openssl-1.1.1w/Configurations/50-masm.conf
openssl-1.1.1w/Configurations/50-win-onecore.conf
openssl-1.1.1w/Configurations/INTERNALS.Configure
openssl-1.1.1w/Configurations/README
openssl-1.1.1w/Configurations/README.design
openssl-1.1.1w/Configurations/common.tmpl
openssl-1.1.1w/Configurations/common0.tmpl
openssl-1.1.1w/Configurations/descrip.mms.tmpl
openssl-1.1.1w/Configurations/shared-info.pl
openssl-1.1.1w/Configurations/unix-Makefile.tmpl
openssl-1.1.1w/Configurations/unix-checker.pm
openssl-1.1.1w/Configurations/windows-checker.pm
openssl-1.1.1w/Configurations/windows-makefile.tmpl
openssl-1.1.1w/Configure
openssl-1.1.1w/FAQ
openssl-1.1.1w/INSTALL
openssl-1.1.1w/LICENSE
openssl-1.1.1w/NEWS
openssl-1.1.1w/NOTES.ANDROID
openssl-1.1.1w/NOTES.DJGPP
openssl-1.1.1w/NOTES.PERL
openssl-1.1.1w/NOTES.UNIX
openssl-1.1.1w/NOTES.VMS
openssl-1.1.1w/NOTES.WIN
openssl-1.1.1w/README
openssl-1.1.1w/README.ENGINE
openssl-1.1.1w/README.FIPS
openssl-1.1.1w/VMS/
openssl-1.1.1w/VMS/VMSify-conf.pl
openssl-1.1.1w/VMS/engine.opt
openssl-1.1.1w/VMS/msg_install.com
openssl-1.1.1w/VMS/msg_staging.com
openssl-1.1.1w/VMS/openssl_ivp.com.in
openssl-1.1.1w/VMS/openssl_shutdown.com.in
openssl-1.1.1w/VMS/openssl_startup.com.in
openssl-1.1.1w/VMS/openssl_utils.com.in
openssl-1.1.1w/VMS/test-includes.com
openssl-1.1.1w/VMS/translatesyms.pl
openssl-1.1.1w/apps/
openssl-1.1.1w/apps/CA.pl.in
openssl-1.1.1w/apps/app_rand.c
openssl-1.1.1w/apps/apps.c
openssl-1.1.1w/apps/apps.h
openssl-1.1.1w/apps/asn1pars.c
openssl-1.1.1w/apps/bf_prefix.c
openssl-1.1.1w/apps/build.info
openssl-1.1.1w/apps/ca-cert.srl
openssl-1.1.1w/apps/ca-key.pem
openssl-1.1.1w/apps/ca-req.pem
openssl-1.1.1w/apps/ca.c
openssl-1.1.1w/apps/cert.pem
openssl-1.1.1w/apps/ciphers.c
openssl-1.1.1w/apps/client.pem
openssl-1.1.1w/apps/cms.c
openssl-1.1.1w/apps/crl.c
openssl-1.1.1w/apps/crl2p7.c
openssl-1.1.1w/apps/ct_log_list.cnf
openssl-1.1.1w/apps/demoSRP/
openssl-1.1.1w/apps/demoSRP/srp_verifier.txt
openssl-1.1.1w/apps/demoSRP/srp_verifier.txt.attr
openssl-1.1.1w/apps/dgst.c
openssl-1.1.1w/apps/dh1024.pem
openssl-1.1.1w/apps/dh2048.pem
openssl-1.1.1w/apps/dh4096.pem
openssl-1.1.1w/apps/dhparam.c
openssl-1.1.1w/apps/dsa-ca.pem
openssl-1.1.1w/apps/dsa-pca.pem
openssl-1.1.1w/apps/dsa.c
openssl-1.1.1w/apps/dsa1024.pem
openssl-1.1.1w/apps/dsa512.pem
openssl-1.1.1w/apps/dsap.pem
openssl-1.1.1w/apps/dsaparam.c
openssl-1.1.1w/apps/ec.c
openssl-1.1.1w/apps/ecparam.c
openssl-1.1.1w/apps/enc.c
openssl-1.1.1w/apps/engine.c
openssl-1.1.1w/apps/errstr.c
openssl-1.1.1w/apps/gendsa.c
openssl-1.1.1w/apps/genpkey.c
openssl-1.1.1w/apps/genrsa.c
openssl-1.1.1w/apps/nseq.c
openssl-1.1.1w/apps/ocsp.c
openssl-1.1.1w/apps/openssl-vms.cnf
openssl-1.1.1w/apps/openssl.c
openssl-1.1.1w/apps/openssl.cnf
openssl-1.1.1w/apps/opt.c
openssl-1.1.1w/apps/passwd.c
openssl-1.1.1w/apps/pca-cert.srl
openssl-1.1.1w/apps/pca-key.pem
openssl-1.1.1w/apps/pca-req.pem
openssl-1.1.1w/apps/pkcs12.c
openssl-1.1.1w/apps/pkcs7.c
openssl-1.1.1w/apps/pkcs8.c
openssl-1.1.1w/apps/pkey.c
openssl-1.1.1w/apps/pkeyparam.c
openssl-1.1.1w/apps/pkeyutl.c
openssl-1.1.1w/apps/prime.c
openssl-1.1.1w/apps/privkey.pem
openssl-1.1.1w/apps/progs.pl
openssl-1.1.1w/apps/rand.c
openssl-1.1.1w/apps/rehash.c
openssl-1.1.1w/apps/req.c
openssl-1.1.1w/apps/req.pem
openssl-1.1.1w/apps/rsa.c
openssl-1.1.1w/apps/rsa8192.pem
openssl-1.1.1w/apps/rsautl.c
openssl-1.1.1w/apps/s1024key.pem
openssl-1.1.1w/apps/s1024req.pem
openssl-1.1.1w/apps/s512-key.pem
openssl-1.1.1w/apps/s512-req.pem
openssl-1.1.1w/apps/s_apps.h
openssl-1.1.1w/apps/s_cb.c
openssl-1.1.1w/apps/s_client.c
openssl-1.1.1w/apps/s_server.c
openssl-1.1.1w/apps/s_socket.c
openssl-1.1.1w/apps/s_time.c
openssl-1.1.1w/apps/server.pem
openssl-1.1.1w/apps/server.srl
openssl-1.1.1w/apps/server2.pem
openssl-1.1.1w/apps/sess_id.c
openssl-1.1.1w/apps/smime.c
openssl-1.1.1w/apps/speed.c
openssl-1.1.1w/apps/spkac.c
openssl-1.1.1w/apps/srp.c
openssl-1.1.1w/apps/storeutl.c
openssl-1.1.1w/apps/testCA.pem
openssl-1.1.1w/apps/testdsa.h
openssl-1.1.1w/apps/testrsa.h
openssl-1.1.1w/apps/timeouts.h
openssl-1.1.1w/apps/ts.c
openssl-1.1.1w/apps/tsget.in
openssl-1.1.1w/apps/verify.c
openssl-1.1.1w/apps/version.c
openssl-1.1.1w/apps/vms_decc_argv.c
openssl-1.1.1w/apps/vms_decc_init.c
openssl-1.1.1w/apps/vms_term_sock.c
openssl-1.1.1w/apps/vms_term_sock.h
openssl-1.1.1w/apps/win32_init.c
openssl-1.1.1w/apps/x509.c
openssl-1.1.1w/build.info
openssl-1.1.1w/config
openssl-1.1.1w/config.com
openssl-1.1.1w/crypto/
openssl-1.1.1w/crypto/LPdir_nyi.c
openssl-1.1.1w/crypto/LPdir_unix.c
openssl-1.1.1w/crypto/LPdir_vms.c
openssl-1.1.1w/crypto/LPdir_win.c
openssl-1.1.1w/crypto/LPdir_win32.c
openssl-1.1.1w/crypto/LPdir_wince.c
openssl-1.1.1w/crypto/aes/
openssl-1.1.1w/crypto/aes/aes_cbc.c
openssl-1.1.1w/crypto/aes/aes_cfb.c
openssl-1.1.1w/crypto/aes/aes_core.c
openssl-1.1.1w/crypto/aes/aes_ecb.c
openssl-1.1.1w/crypto/aes/aes_ige.c
openssl-1.1.1w/crypto/aes/aes_local.h
openssl-1.1.1w/crypto/aes/aes_misc.c
openssl-1.1.1w/crypto/aes/aes_ofb.c
openssl-1.1.1w/crypto/aes/aes_wrap.c
openssl-1.1.1w/crypto/aes/aes_x86core.c
openssl-1.1.1w/crypto/aes/asm/
openssl-1.1.1w/crypto/aes/asm/aes-armv4.pl
openssl-1.1.1w/crypto/aes/asm/aes-c64xplus.pl
openssl-1.1.1w/crypto/aes/asm/aes-ia64.S
openssl-1.1.1w/crypto/aes/asm/aes-mips.pl
openssl-1.1.1w/crypto/aes/asm/aes-parisc.pl
openssl-1.1.1w/crypto/aes/asm/aes-ppc.pl
openssl-1.1.1w/crypto/aes/asm/aes-s390x.pl
openssl-1.1.1w/crypto/aes/asm/aes-sparcv9.pl
openssl-1.1.1w/crypto/aes/asm/aesfx-sparcv9.pl
openssl-1.1.1w/crypto/aes/asm/aesni-mb-x86_64.pl
openssl-1.1.1w/crypto/aes/asm/aesni-sha1-x86_64.pl
openssl-1.1.1w/crypto/aes/asm/aesni-sha256-x86_64.pl
openssl-1.1.1w/crypto/aes/asm/aesni-x86.pl
openssl-1.1.1w/crypto/aes/asm/aesni-x86_64.pl
openssl-1.1.1w/crypto/aes/asm/aesp8-ppc.pl
openssl-1.1.1w/crypto/aes/asm/aest4-sparcv9.pl
openssl-1.1.1w/crypto/aes/asm/aesv8-armx.pl
openssl-1.1.1w/crypto/aes/asm/bsaes-armv7.pl
openssl-1.1.1w/crypto/aes/asm/vpaes-armv8.pl
openssl-1.1.1w/crypto/aes/asm/vpaes-ppc.pl
openssl-1.1.1w/crypto/aes/asm/vpaes-x86.pl
openssl-1.1.1w/crypto/aes/asm/vpaes-x86_64.pl
openssl-1.1.1w/crypto/aes/build.info
openssl-1.1.1w/crypto/alphacpuid.pl
openssl-1.1.1w/crypto/aria/
openssl-1.1.1w/crypto/aria/aria.c
openssl-1.1.1w/crypto/aria/build.info
openssl-1.1.1w/crypto/arm64cpuid.pl
openssl-1.1.1w/crypto/arm_arch.h
openssl-1.1.1w/crypto/armcap.c
openssl-1.1.1w/crypto/armv4cpuid.pl
openssl-1.1.1w/crypto/asn1/
openssl-1.1.1w/crypto/asn1/a_bitstr.c
openssl-1.1.1w/crypto/asn1/a_d2i_fp.c
openssl-1.1.1w/crypto/asn1/a_digest.c
openssl-1.1.1w/crypto/asn1/a_dup.c
openssl-1.1.1w/crypto/asn1/a_gentm.c
openssl-1.1.1w/crypto/asn1/a_i2d_fp.c
openssl-1.1.1w/crypto/asn1/a_int.c
openssl-1.1.1w/crypto/asn1/a_mbstr.c
openssl-1.1.1w/crypto/asn1/a_object.c
openssl-1.1.1w/crypto/asn1/a_octet.c
openssl-1.1.1w/crypto/asn1/a_print.c
openssl-1.1.1w/crypto/asn1/a_sign.c
openssl-1.1.1w/crypto/asn1/a_strex.c
openssl-1.1.1w/crypto/asn1/a_strnid.c
openssl-1.1.1w/crypto/asn1/a_time.c
openssl-1.1.1w/crypto/asn1/a_type.c
openssl-1.1.1w/crypto/asn1/a_utctm.c
openssl-1.1.1w/crypto/asn1/a_utf8.c
openssl-1.1.1w/crypto/asn1/a_verify.c
openssl-1.1.1w/crypto/asn1/ameth_lib.c
openssl-1.1.1w/crypto/asn1/asn1_err.c
openssl-1.1.1w/crypto/asn1/asn1_gen.c
openssl-1.1.1w/crypto/asn1/asn1_item_list.c
openssl-1.1.1w/crypto/asn1/asn1_item_list.h
openssl-1.1.1w/crypto/asn1/asn1_lib.c
openssl-1.1.1w/crypto/asn1/asn1_local.h
openssl-1.1.1w/crypto/asn1/asn1_par.c
openssl-1.1.1w/crypto/asn1/asn_mime.c
openssl-1.1.1w/crypto/asn1/asn_moid.c
openssl-1.1.1w/crypto/asn1/asn_mstbl.c
openssl-1.1.1w/crypto/asn1/asn_pack.c
openssl-1.1.1w/crypto/asn1/bio_asn1.c
openssl-1.1.1w/crypto/asn1/bio_ndef.c
openssl-1.1.1w/crypto/asn1/build.info
openssl-1.1.1w/crypto/asn1/charmap.h
openssl-1.1.1w/crypto/asn1/charmap.pl
openssl-1.1.1w/crypto/asn1/d2i_pr.c
openssl-1.1.1w/crypto/asn1/d2i_pu.c
openssl-1.1.1w/crypto/asn1/evp_asn1.c
openssl-1.1.1w/crypto/asn1/f_int.c
openssl-1.1.1w/crypto/asn1/f_string.c
openssl-1.1.1w/crypto/asn1/i2d_pr.c
openssl-1.1.1w/crypto/asn1/i2d_pu.c
openssl-1.1.1w/crypto/asn1/n_pkey.c
openssl-1.1.1w/crypto/asn1/nsseq.c
openssl-1.1.1w/crypto/asn1/p5_pbe.c
openssl-1.1.1w/crypto/asn1/p5_pbev2.c
openssl-1.1.1w/crypto/asn1/p5_scrypt.c
openssl-1.1.1w/crypto/asn1/p8_pkey.c
openssl-1.1.1w/crypto/asn1/standard_methods.h
openssl-1.1.1w/crypto/asn1/t_bitst.c
openssl-1.1.1w/crypto/asn1/t_pkey.c
openssl-1.1.1w/crypto/asn1/t_spki.c
openssl-1.1.1w/crypto/asn1/tasn_dec.c
openssl-1.1.1w/crypto/asn1/tasn_enc.c
openssl-1.1.1w/crypto/asn1/tasn_fre.c
openssl-1.1.1w/crypto/asn1/tasn_new.c
openssl-1.1.1w/crypto/asn1/tasn_prn.c
openssl-1.1.1w/crypto/asn1/tasn_scn.c
openssl-1.1.1w/crypto/asn1/tasn_typ.c
openssl-1.1.1w/crypto/asn1/tasn_utl.c
openssl-1.1.1w/crypto/asn1/tbl_standard.h
openssl-1.1.1w/crypto/asn1/x_algor.c
openssl-1.1.1w/crypto/asn1/x_bignum.c
openssl-1.1.1w/crypto/asn1/x_info.c
openssl-1.1.1w/crypto/asn1/x_int64.c
openssl-1.1.1w/crypto/asn1/x_long.c
openssl-1.1.1w/crypto/asn1/x_pkey.c
openssl-1.1.1w/crypto/asn1/x_sig.c
openssl-1.1.1w/crypto/asn1/x_spki.c
openssl-1.1.1w/crypto/asn1/x_val.c
openssl-1.1.1w/crypto/async/
openssl-1.1.1w/crypto/async/arch/
openssl-1.1.1w/crypto/async/arch/async_null.c
openssl-1.1.1w/crypto/async/arch/async_null.h
openssl-1.1.1w/crypto/async/arch/async_posix.c
openssl-1.1.1w/crypto/async/arch/async_posix.h
openssl-1.1.1w/crypto/async/arch/async_win.c
openssl-1.1.1w/crypto/async/arch/async_win.h
openssl-1.1.1w/crypto/async/async.c
openssl-1.1.1w/crypto/async/async_err.c
openssl-1.1.1w/crypto/async/async_local.h
openssl-1.1.1w/crypto/async/async_wait.c
openssl-1.1.1w/crypto/async/build.info
openssl-1.1.1w/crypto/bf/
openssl-1.1.1w/crypto/bf/asm/
openssl-1.1.1w/crypto/bf/asm/bf-586.pl
openssl-1.1.1w/crypto/bf/bf_cfb64.c
openssl-1.1.1w/crypto/bf/bf_ecb.c
openssl-1.1.1w/crypto/bf/bf_enc.c
openssl-1.1.1w/crypto/bf/bf_local.h
openssl-1.1.1w/crypto/bf/bf_ofb64.c
openssl-1.1.1w/crypto/bf/bf_pi.h
openssl-1.1.1w/crypto/bf/bf_skey.c
openssl-1.1.1w/crypto/bf/build.info
openssl-1.1.1w/crypto/bio/
openssl-1.1.1w/crypto/bio/b_addr.c
openssl-1.1.1w/crypto/bio/b_dump.c
openssl-1.1.1w/crypto/bio/b_print.c
openssl-1.1.1w/crypto/bio/b_sock.c
openssl-1.1.1w/crypto/bio/b_sock2.c
openssl-1.1.1w/crypto/bio/bf_buff.c
openssl-1.1.1w/crypto/bio/bf_lbuf.c
openssl-1.1.1w/crypto/bio/bf_nbio.c
openssl-1.1.1w/crypto/bio/bf_null.c
openssl-1.1.1w/crypto/bio/bio_cb.c
openssl-1.1.1w/crypto/bio/bio_err.c
openssl-1.1.1w/crypto/bio/bio_lib.c
openssl-1.1.1w/crypto/bio/bio_local.h
openssl-1.1.1w/crypto/bio/bio_meth.c
openssl-1.1.1w/crypto/bio/bss_acpt.c
openssl-1.1.1w/crypto/bio/bss_bio.c
openssl-1.1.1w/crypto/bio/bss_conn.c
openssl-1.1.1w/crypto/bio/bss_dgram.c
openssl-1.1.1w/crypto/bio/bss_fd.c
openssl-1.1.1w/crypto/bio/bss_file.c
openssl-1.1.1w/crypto/bio/bss_log.c
openssl-1.1.1w/crypto/bio/bss_mem.c
openssl-1.1.1w/crypto/bio/bss_null.c
openssl-1.1.1w/crypto/bio/bss_sock.c
openssl-1.1.1w/crypto/bio/build.info
openssl-1.1.1w/crypto/blake2/
openssl-1.1.1w/crypto/blake2/blake2_impl.h
openssl-1.1.1w/crypto/blake2/blake2_local.h
openssl-1.1.1w/crypto/blake2/blake2b.c
openssl-1.1.1w/crypto/blake2/blake2s.c
openssl-1.1.1w/crypto/blake2/build.info
openssl-1.1.1w/crypto/blake2/m_blake2b.c
openssl-1.1.1w/crypto/blake2/m_blake2s.c
openssl-1.1.1w/crypto/bn/
openssl-1.1.1w/crypto/bn/README.pod
openssl-1.1.1w/crypto/bn/asm/
openssl-1.1.1w/crypto/bn/asm/alpha-mont.pl
openssl-1.1.1w/crypto/bn/asm/armv4-gf2m.pl
openssl-1.1.1w/crypto/bn/asm/armv4-mont.pl
openssl-1.1.1w/crypto/bn/asm/armv8-mont.pl
openssl-1.1.1w/crypto/bn/asm/bn-586.pl
openssl-1.1.1w/crypto/bn/asm/bn-c64xplus.asm
openssl-1.1.1w/crypto/bn/asm/c64xplus-gf2m.pl
openssl-1.1.1w/crypto/bn/asm/co-586.pl
openssl-1.1.1w/crypto/bn/asm/ia64-mont.pl
openssl-1.1.1w/crypto/bn/asm/ia64.S
openssl-1.1.1w/crypto/bn/asm/mips-mont.pl
openssl-1.1.1w/crypto/bn/asm/mips.pl
openssl-1.1.1w/crypto/bn/asm/parisc-mont.pl
openssl-1.1.1w/crypto/bn/asm/ppc-mont.pl
openssl-1.1.1w/crypto/bn/asm/ppc.pl
openssl-1.1.1w/crypto/bn/asm/ppc64-mont.pl
openssl-1.1.1w/crypto/bn/asm/rsaz-avx2.pl
openssl-1.1.1w/crypto/bn/asm/rsaz-x86_64.pl
openssl-1.1.1w/crypto/bn/asm/s390x-gf2m.pl
openssl-1.1.1w/crypto/bn/asm/s390x-mont.pl
openssl-1.1.1w/crypto/bn/asm/s390x.S
openssl-1.1.1w/crypto/bn/asm/sparct4-mont.pl
openssl-1.1.1w/crypto/bn/asm/sparcv8.S
openssl-1.1.1w/crypto/bn/asm/sparcv8plus.S
openssl-1.1.1w/crypto/bn/asm/sparcv9-gf2m.pl
openssl-1.1.1w/crypto/bn/asm/sparcv9-mont.pl
openssl-1.1.1w/crypto/bn/asm/sparcv9a-mont.pl
openssl-1.1.1w/crypto/bn/asm/via-mont.pl
openssl-1.1.1w/crypto/bn/asm/vis3-mont.pl
openssl-1.1.1w/crypto/bn/asm/x86-gf2m.pl
openssl-1.1.1w/crypto/bn/asm/x86-mont.pl
openssl-1.1.1w/crypto/bn/asm/x86_64-gcc.c
openssl-1.1.1w/crypto/bn/asm/x86_64-gf2m.pl
openssl-1.1.1w/crypto/bn/asm/x86_64-mont.pl
openssl-1.1.1w/crypto/bn/asm/x86_64-mont5.pl
openssl-1.1.1w/crypto/bn/bn_add.c
openssl-1.1.1w/crypto/bn/bn_asm.c
openssl-1.1.1w/crypto/bn/bn_blind.c
openssl-1.1.1w/crypto/bn/bn_const.c
openssl-1.1.1w/crypto/bn/bn_ctx.c
openssl-1.1.1w/crypto/bn/bn_depr.c
openssl-1.1.1w/crypto/bn/bn_dh.c
openssl-1.1.1w/crypto/bn/bn_div.c
openssl-1.1.1w/crypto/bn/bn_err.c
openssl-1.1.1w/crypto/bn/bn_exp.c
openssl-1.1.1w/crypto/bn/bn_exp2.c
openssl-1.1.1w/crypto/bn/bn_gcd.c
openssl-1.1.1w/crypto/bn/bn_gf2m.c
openssl-1.1.1w/crypto/bn/bn_intern.c
openssl-1.1.1w/crypto/bn/bn_kron.c
openssl-1.1.1w/crypto/bn/bn_lib.c
openssl-1.1.1w/crypto/bn/bn_local.h
openssl-1.1.1w/crypto/bn/bn_mod.c
openssl-1.1.1w/crypto/bn/bn_mont.c
openssl-1.1.1w/crypto/bn/bn_mpi.c
openssl-1.1.1w/crypto/bn/bn_mul.c
openssl-1.1.1w/crypto/bn/bn_nist.c
openssl-1.1.1w/crypto/bn/bn_prime.c
openssl-1.1.1w/crypto/bn/bn_prime.h
openssl-1.1.1w/crypto/bn/bn_prime.pl
openssl-1.1.1w/crypto/bn/bn_print.c
openssl-1.1.1w/crypto/bn/bn_rand.c
openssl-1.1.1w/crypto/bn/bn_recp.c
openssl-1.1.1w/crypto/bn/bn_shift.c
openssl-1.1.1w/crypto/bn/bn_sqr.c
openssl-1.1.1w/crypto/bn/bn_sqrt.c
openssl-1.1.1w/crypto/bn/bn_srp.c
openssl-1.1.1w/crypto/bn/bn_word.c
openssl-1.1.1w/crypto/bn/bn_x931p.c
openssl-1.1.1w/crypto/bn/build.info
openssl-1.1.1w/crypto/bn/rsaz_exp.c
openssl-1.1.1w/crypto/bn/rsaz_exp.h
openssl-1.1.1w/crypto/buffer/
openssl-1.1.1w/crypto/buffer/buf_err.c
openssl-1.1.1w/crypto/buffer/buffer.c
openssl-1.1.1w/crypto/buffer/build.info
openssl-1.1.1w/crypto/build.info
openssl-1.1.1w/crypto/c64xpluscpuid.pl
openssl-1.1.1w/crypto/camellia/
openssl-1.1.1w/crypto/camellia/asm/
openssl-1.1.1w/crypto/camellia/asm/cmll-x86.pl
openssl-1.1.1w/crypto/camellia/asm/cmll-x86_64.pl
openssl-1.1.1w/crypto/camellia/asm/cmllt4-sparcv9.pl
openssl-1.1.1w/crypto/camellia/build.info
openssl-1.1.1w/crypto/camellia/camellia.c
openssl-1.1.1w/crypto/camellia/cmll_cbc.c
openssl-1.1.1w/crypto/camellia/cmll_cfb.c
openssl-1.1.1w/crypto/camellia/cmll_ctr.c
openssl-1.1.1w/crypto/camellia/cmll_ecb.c
openssl-1.1.1w/crypto/camellia/cmll_local.h
openssl-1.1.1w/crypto/camellia/cmll_misc.c
openssl-1.1.1w/crypto/camellia/cmll_ofb.c
openssl-1.1.1w/crypto/cast/
openssl-1.1.1w/crypto/cast/asm/
openssl-1.1.1w/crypto/cast/asm/cast-586.pl
openssl-1.1.1w/crypto/cast/build.info
openssl-1.1.1w/crypto/cast/c_cfb64.c
openssl-1.1.1w/crypto/cast/c_ecb.c
openssl-1.1.1w/crypto/cast/c_enc.c
openssl-1.1.1w/crypto/cast/c_ofb64.c
openssl-1.1.1w/crypto/cast/c_skey.c
openssl-1.1.1w/crypto/cast/cast_local.h
openssl-1.1.1w/crypto/cast/cast_s.h
openssl-1.1.1w/crypto/chacha/
openssl-1.1.1w/crypto/chacha/asm/
openssl-1.1.1w/crypto/chacha/asm/chacha-armv4.pl
openssl-1.1.1w/crypto/chacha/asm/chacha-armv8.pl
openssl-1.1.1w/crypto/chacha/asm/chacha-c64xplus.pl
openssl-1.1.1w/crypto/chacha/asm/chacha-ppc.pl
openssl-1.1.1w/crypto/chacha/asm/chacha-s390x.pl
openssl-1.1.1w/crypto/chacha/asm/chacha-x86.pl
openssl-1.1.1w/crypto/chacha/asm/chacha-x86_64.pl
openssl-1.1.1w/crypto/chacha/build.info
openssl-1.1.1w/crypto/chacha/chacha_enc.c
openssl-1.1.1w/crypto/cmac/
openssl-1.1.1w/crypto/cmac/build.info
openssl-1.1.1w/crypto/cmac/cm_ameth.c
openssl-1.1.1w/crypto/cmac/cm_pmeth.c
openssl-1.1.1w/crypto/cmac/cmac.c
openssl-1.1.1w/crypto/cms/
openssl-1.1.1w/crypto/cms/build.info
openssl-1.1.1w/crypto/cms/cms_asn1.c
openssl-1.1.1w/crypto/cms/cms_att.c
openssl-1.1.1w/crypto/cms/cms_cd.c
openssl-1.1.1w/crypto/cms/cms_dd.c
openssl-1.1.1w/crypto/cms/cms_enc.c
openssl-1.1.1w/crypto/cms/cms_env.c
openssl-1.1.1w/crypto/cms/cms_err.c
openssl-1.1.1w/crypto/cms/cms_ess.c
openssl-1.1.1w/crypto/cms/cms_io.c
openssl-1.1.1w/crypto/cms/cms_kari.c
openssl-1.1.1w/crypto/cms/cms_lib.c
openssl-1.1.1w/crypto/cms/cms_local.h
openssl-1.1.1w/crypto/cms/cms_pwri.c
openssl-1.1.1w/crypto/cms/cms_sd.c
openssl-1.1.1w/crypto/cms/cms_smime.c
openssl-1.1.1w/crypto/comp/
openssl-1.1.1w/crypto/comp/build.info
openssl-1.1.1w/crypto/comp/c_zlib.c
openssl-1.1.1w/crypto/comp/comp_err.c
openssl-1.1.1w/crypto/comp/comp_lib.c
openssl-1.1.1w/crypto/comp/comp_local.h
openssl-1.1.1w/crypto/conf/
openssl-1.1.1w/crypto/conf/build.info
openssl-1.1.1w/crypto/conf/conf_api.c
openssl-1.1.1w/crypto/conf/conf_def.c
openssl-1.1.1w/crypto/conf/conf_def.h
openssl-1.1.1w/crypto/conf/conf_err.c
openssl-1.1.1w/crypto/conf/conf_lib.c
openssl-1.1.1w/crypto/conf/conf_local.h
openssl-1.1.1w/crypto/conf/conf_mall.c
openssl-1.1.1w/crypto/conf/conf_mod.c
openssl-1.1.1w/crypto/conf/conf_sap.c
openssl-1.1.1w/crypto/conf/conf_ssl.c
openssl-1.1.1w/crypto/conf/keysets.pl
openssl-1.1.1w/crypto/cpt_err.c
openssl-1.1.1w/crypto/cryptlib.c
openssl-1.1.1w/crypto/ct/
openssl-1.1.1w/crypto/ct/build.info
openssl-1.1.1w/crypto/ct/ct_b64.c
openssl-1.1.1w/crypto/ct/ct_err.c
openssl-1.1.1w/crypto/ct/ct_local.h
openssl-1.1.1w/crypto/ct/ct_log.c
openssl-1.1.1w/crypto/ct/ct_oct.c
openssl-1.1.1w/crypto/ct/ct_policy.c
openssl-1.1.1w/crypto/ct/ct_prn.c
openssl-1.1.1w/crypto/ct/ct_sct.c
openssl-1.1.1w/crypto/ct/ct_sct_ctx.c
openssl-1.1.1w/crypto/ct/ct_vfy.c
openssl-1.1.1w/crypto/ct/ct_x509v3.c
openssl-1.1.1w/crypto/ctype.c
openssl-1.1.1w/crypto/cversion.c
openssl-1.1.1w/crypto/des/
openssl-1.1.1w/crypto/des/asm/
openssl-1.1.1w/crypto/des/asm/crypt586.pl
openssl-1.1.1w/crypto/des/asm/des-586.pl
openssl-1.1.1w/crypto/des/asm/des_enc.m4
openssl-1.1.1w/crypto/des/asm/desboth.pl
openssl-1.1.1w/crypto/des/asm/dest4-sparcv9.pl
openssl-1.1.1w/crypto/des/build.info
openssl-1.1.1w/crypto/des/cbc_cksm.c
openssl-1.1.1w/crypto/des/cbc_enc.c
openssl-1.1.1w/crypto/des/cfb64ede.c
openssl-1.1.1w/crypto/des/cfb64enc.c
openssl-1.1.1w/crypto/des/cfb_enc.c
openssl-1.1.1w/crypto/des/des_enc.c
openssl-1.1.1w/crypto/des/des_local.h
openssl-1.1.1w/crypto/des/ecb3_enc.c
openssl-1.1.1w/crypto/des/ecb_enc.c
openssl-1.1.1w/crypto/des/fcrypt.c
openssl-1.1.1w/crypto/des/fcrypt_b.c
openssl-1.1.1w/crypto/des/ncbc_enc.c
openssl-1.1.1w/crypto/des/ofb64ede.c
openssl-1.1.1w/crypto/des/ofb64enc.c
openssl-1.1.1w/crypto/des/ofb_enc.c
openssl-1.1.1w/crypto/des/pcbc_enc.c
openssl-1.1.1w/crypto/des/qud_cksm.c
openssl-1.1.1w/crypto/des/rand_key.c
openssl-1.1.1w/crypto/des/set_key.c
openssl-1.1.1w/crypto/des/spr.h
openssl-1.1.1w/crypto/des/str2key.c
openssl-1.1.1w/crypto/des/xcbc_enc.c
openssl-1.1.1w/crypto/dh/
openssl-1.1.1w/crypto/dh/build.info
openssl-1.1.1w/crypto/dh/dh1024.pem
openssl-1.1.1w/crypto/dh/dh192.pem
openssl-1.1.1w/crypto/dh/dh2048.pem
openssl-1.1.1w/crypto/dh/dh4096.pem
openssl-1.1.1w/crypto/dh/dh512.pem
openssl-1.1.1w/crypto/dh/dh_ameth.c
openssl-1.1.1w/crypto/dh/dh_asn1.c
openssl-1.1.1w/crypto/dh/dh_check.c
openssl-1.1.1w/crypto/dh/dh_depr.c
openssl-1.1.1w/crypto/dh/dh_err.c
openssl-1.1.1w/crypto/dh/dh_gen.c
openssl-1.1.1w/crypto/dh/dh_kdf.c
openssl-1.1.1w/crypto/dh/dh_key.c
openssl-1.1.1w/crypto/dh/dh_lib.c
openssl-1.1.1w/crypto/dh/dh_local.h
openssl-1.1.1w/crypto/dh/dh_meth.c
openssl-1.1.1w/crypto/dh/dh_pmeth.c
openssl-1.1.1w/crypto/dh/dh_prn.c
openssl-1.1.1w/crypto/dh/dh_rfc5114.c
openssl-1.1.1w/crypto/dh/dh_rfc7919.c
openssl-1.1.1w/crypto/dllmain.c
openssl-1.1.1w/crypto/dsa/
openssl-1.1.1w/crypto/dsa/build.info
openssl-1.1.1w/crypto/dsa/dsa_ameth.c
openssl-1.1.1w/crypto/dsa/dsa_asn1.c
openssl-1.1.1w/crypto/dsa/dsa_depr.c
openssl-1.1.1w/crypto/dsa/dsa_err.c
openssl-1.1.1w/crypto/dsa/dsa_gen.c
openssl-1.1.1w/crypto/dsa/dsa_key.c
openssl-1.1.1w/crypto/dsa/dsa_lib.c
openssl-1.1.1w/crypto/dsa/dsa_local.h
openssl-1.1.1w/crypto/dsa/dsa_meth.c
openssl-1.1.1w/crypto/dsa/dsa_ossl.c
openssl-1.1.1w/crypto/dsa/dsa_pmeth.c
openssl-1.1.1w/crypto/dsa/dsa_prn.c
openssl-1.1.1w/crypto/dsa/dsa_sign.c
openssl-1.1.1w/crypto/dsa/dsa_vrf.c
openssl-1.1.1w/crypto/dso/
openssl-1.1.1w/crypto/dso/build.info
openssl-1.1.1w/crypto/dso/dso_dl.c
openssl-1.1.1w/crypto/dso/dso_dlfcn.c
openssl-1.1.1w/crypto/dso/dso_err.c
openssl-1.1.1w/crypto/dso/dso_lib.c
openssl-1.1.1w/crypto/dso/dso_local.h
openssl-1.1.1w/crypto/dso/dso_openssl.c
openssl-1.1.1w/crypto/dso/dso_vms.c
openssl-1.1.1w/crypto/dso/dso_win32.c
openssl-1.1.1w/crypto/ebcdic.c
openssl-1.1.1w/crypto/ec/
openssl-1.1.1w/crypto/ec/asm/
openssl-1.1.1w/crypto/ec/asm/ecp_nistz256-armv4.pl
openssl-1.1.1w/crypto/ec/asm/ecp_nistz256-armv8.pl
openssl-1.1.1w/crypto/ec/asm/ecp_nistz256-ppc64.pl
openssl-1.1.1w/crypto/ec/asm/ecp_nistz256-sparcv9.pl
openssl-1.1.1w/crypto/ec/asm/ecp_nistz256-x86.pl
openssl-1.1.1w/crypto/ec/asm/ecp_nistz256-x86_64.pl
openssl-1.1.1w/crypto/ec/asm/x25519-ppc64.pl
openssl-1.1.1w/crypto/ec/asm/x25519-x86_64.pl
openssl-1.1.1w/crypto/ec/build.info
openssl-1.1.1w/crypto/ec/curve25519.c
openssl-1.1.1w/crypto/ec/curve448/
openssl-1.1.1w/crypto/ec/curve448/arch_32/
openssl-1.1.1w/crypto/ec/curve448/arch_32/arch_intrinsics.h
openssl-1.1.1w/crypto/ec/curve448/arch_32/f_impl.c
openssl-1.1.1w/crypto/ec/curve448/arch_32/f_impl.h
openssl-1.1.1w/crypto/ec/curve448/curve448.c
openssl-1.1.1w/crypto/ec/curve448/curve448_local.h
openssl-1.1.1w/crypto/ec/curve448/curve448_tables.c
openssl-1.1.1w/crypto/ec/curve448/curve448utils.h
openssl-1.1.1w/crypto/ec/curve448/ed448.h
openssl-1.1.1w/crypto/ec/curve448/eddsa.c
openssl-1.1.1w/crypto/ec/curve448/f_generic.c
openssl-1.1.1w/crypto/ec/curve448/field.h
openssl-1.1.1w/crypto/ec/curve448/point_448.h
openssl-1.1.1w/crypto/ec/curve448/scalar.c
openssl-1.1.1w/crypto/ec/curve448/word.h
openssl-1.1.1w/crypto/ec/ec2_oct.c
openssl-1.1.1w/crypto/ec/ec2_smpl.c
openssl-1.1.1w/crypto/ec/ec_ameth.c
openssl-1.1.1w/crypto/ec/ec_asn1.c
openssl-1.1.1w/crypto/ec/ec_check.c
openssl-1.1.1w/crypto/ec/ec_curve.c
openssl-1.1.1w/crypto/ec/ec_cvt.c
openssl-1.1.1w/crypto/ec/ec_err.c
openssl-1.1.1w/crypto/ec/ec_key.c
openssl-1.1.1w/crypto/ec/ec_kmeth.c
openssl-1.1.1w/crypto/ec/ec_lib.c
openssl-1.1.1w/crypto/ec/ec_local.h
openssl-1.1.1w/crypto/ec/ec_mult.c
openssl-1.1.1w/crypto/ec/ec_oct.c
openssl-1.1.1w/crypto/ec/ec_pmeth.c
openssl-1.1.1w/crypto/ec/ec_print.c
openssl-1.1.1w/crypto/ec/ecdh_kdf.c
openssl-1.1.1w/crypto/ec/ecdh_ossl.c
openssl-1.1.1w/crypto/ec/ecdsa_ossl.c
openssl-1.1.1w/crypto/ec/ecdsa_sign.c
openssl-1.1.1w/crypto/ec/ecdsa_vrf.c
openssl-1.1.1w/crypto/ec/eck_prn.c
openssl-1.1.1w/crypto/ec/ecp_mont.c
openssl-1.1.1w/crypto/ec/ecp_nist.c
openssl-1.1.1w/crypto/ec/ecp_nistp224.c
openssl-1.1.1w/crypto/ec/ecp_nistp256.c
openssl-1.1.1w/crypto/ec/ecp_nistp521.c
openssl-1.1.1w/crypto/ec/ecp_nistputil.c
openssl-1.1.1w/crypto/ec/ecp_nistz256.c
openssl-1.1.1w/crypto/ec/ecp_nistz256_table.c
openssl-1.1.1w/crypto/ec/ecp_oct.c
openssl-1.1.1w/crypto/ec/ecp_smpl.c
openssl-1.1.1w/crypto/ec/ecx_meth.c
openssl-1.1.1w/crypto/engine/
openssl-1.1.1w/crypto/engine/README
openssl-1.1.1w/crypto/engine/build.info
openssl-1.1.1w/crypto/engine/eng_all.c
openssl-1.1.1w/crypto/engine/eng_cnf.c
openssl-1.1.1w/crypto/engine/eng_ctrl.c
openssl-1.1.1w/crypto/engine/eng_devcrypto.c
openssl-1.1.1w/crypto/engine/eng_dyn.c
openssl-1.1.1w/crypto/engine/eng_err.c
openssl-1.1.1w/crypto/engine/eng_fat.c
openssl-1.1.1w/crypto/engine/eng_init.c
openssl-1.1.1w/crypto/engine/eng_lib.c
openssl-1.1.1w/crypto/engine/eng_list.c
openssl-1.1.1w/crypto/engine/eng_local.h
openssl-1.1.1w/crypto/engine/eng_openssl.c
openssl-1.1.1w/crypto/engine/eng_pkey.c
openssl-1.1.1w/crypto/engine/eng_rdrand.c
openssl-1.1.1w/crypto/engine/eng_table.c
openssl-1.1.1w/crypto/engine/tb_asnmth.c
openssl-1.1.1w/crypto/engine/tb_cipher.c
openssl-1.1.1w/crypto/engine/tb_dh.c
openssl-1.1.1w/crypto/engine/tb_digest.c
openssl-1.1.1w/crypto/engine/tb_dsa.c
openssl-1.1.1w/crypto/engine/tb_eckey.c
openssl-1.1.1w/crypto/engine/tb_pkmeth.c
openssl-1.1.1w/crypto/engine/tb_rand.c
openssl-1.1.1w/crypto/engine/tb_rsa.c
openssl-1.1.1w/crypto/err/
openssl-1.1.1w/crypto/err/README
openssl-1.1.1w/crypto/err/build.info
openssl-1.1.1w/crypto/err/err.c
openssl-1.1.1w/crypto/err/err_all.c
openssl-1.1.1w/crypto/err/err_prn.c
openssl-1.1.1w/crypto/err/openssl.ec
openssl-1.1.1w/crypto/err/openssl.txt
openssl-1.1.1w/crypto/evp/
openssl-1.1.1w/crypto/evp/bio_b64.c
openssl-1.1.1w/crypto/evp/bio_enc.c
openssl-1.1.1w/crypto/evp/bio_md.c
openssl-1.1.1w/crypto/evp/bio_ok.c
openssl-1.1.1w/crypto/evp/build.info
openssl-1.1.1w/crypto/evp/c_allc.c
openssl-1.1.1w/crypto/evp/c_alld.c
openssl-1.1.1w/crypto/evp/cmeth_lib.c
openssl-1.1.1w/crypto/evp/digest.c
openssl-1.1.1w/crypto/evp/e_aes.c
openssl-1.1.1w/crypto/evp/e_aes_cbc_hmac_sha1.c
openssl-1.1.1w/crypto/evp/e_aes_cbc_hmac_sha256.c
openssl-1.1.1w/crypto/evp/e_aria.c
openssl-1.1.1w/crypto/evp/e_bf.c
openssl-1.1.1w/crypto/evp/e_camellia.c
openssl-1.1.1w/crypto/evp/e_cast.c
openssl-1.1.1w/crypto/evp/e_chacha20_poly1305.c
openssl-1.1.1w/crypto/evp/e_des.c
openssl-1.1.1w/crypto/evp/e_des3.c
openssl-1.1.1w/crypto/evp/e_idea.c
openssl-1.1.1w/crypto/evp/e_null.c
openssl-1.1.1w/crypto/evp/e_old.c
openssl-1.1.1w/crypto/evp/e_rc2.c
openssl-1.1.1w/crypto/evp/e_rc4.c
openssl-1.1.1w/crypto/evp/e_rc4_hmac_md5.c
openssl-1.1.1w/crypto/evp/e_rc5.c
openssl-1.1.1w/crypto/evp/e_seed.c
openssl-1.1.1w/crypto/evp/e_sm4.c
openssl-1.1.1w/crypto/evp/e_xcbc_d.c
openssl-1.1.1w/crypto/evp/encode.c
openssl-1.1.1w/crypto/evp/evp_cnf.c
openssl-1.1.1w/crypto/evp/evp_enc.c
openssl-1.1.1w/crypto/evp/evp_err.c
openssl-1.1.1w/crypto/evp/evp_key.c
openssl-1.1.1w/crypto/evp/evp_lib.c
openssl-1.1.1w/crypto/evp/evp_local.h
openssl-1.1.1w/crypto/evp/evp_pbe.c
openssl-1.1.1w/crypto/evp/evp_pkey.c
openssl-1.1.1w/crypto/evp/m_md2.c
openssl-1.1.1w/crypto/evp/m_md4.c
openssl-1.1.1w/crypto/evp/m_md5.c
openssl-1.1.1w/crypto/evp/m_md5_sha1.c
openssl-1.1.1w/crypto/evp/m_mdc2.c
openssl-1.1.1w/crypto/evp/m_null.c
openssl-1.1.1w/crypto/evp/m_ripemd.c
openssl-1.1.1w/crypto/evp/m_sha1.c
openssl-1.1.1w/crypto/evp/m_sha3.c
openssl-1.1.1w/crypto/evp/m_sigver.c
openssl-1.1.1w/crypto/evp/m_wp.c
openssl-1.1.1w/crypto/evp/names.c
openssl-1.1.1w/crypto/evp/p5_crpt.c
openssl-1.1.1w/crypto/evp/p5_crpt2.c
openssl-1.1.1w/crypto/evp/p_dec.c
openssl-1.1.1w/crypto/evp/p_enc.c
openssl-1.1.1w/crypto/evp/p_lib.c
openssl-1.1.1w/crypto/evp/p_open.c
openssl-1.1.1w/crypto/evp/p_seal.c
openssl-1.1.1w/crypto/evp/p_sign.c
openssl-1.1.1w/crypto/evp/p_verify.c
openssl-1.1.1w/crypto/evp/pbe_scrypt.c
openssl-1.1.1w/crypto/evp/pmeth_fn.c
openssl-1.1.1w/crypto/evp/pmeth_gn.c
openssl-1.1.1w/crypto/evp/pmeth_lib.c
openssl-1.1.1w/crypto/ex_data.c
openssl-1.1.1w/crypto/getenv.c
openssl-1.1.1w/crypto/hmac/
openssl-1.1.1w/crypto/hmac/build.info
openssl-1.1.1w/crypto/hmac/hm_ameth.c
openssl-1.1.1w/crypto/hmac/hm_pmeth.c
openssl-1.1.1w/crypto/hmac/hmac.c
openssl-1.1.1w/crypto/hmac/hmac_local.h
openssl-1.1.1w/crypto/ia64cpuid.S
openssl-1.1.1w/crypto/idea/
openssl-1.1.1w/crypto/idea/build.info
openssl-1.1.1w/crypto/idea/i_cbc.c
openssl-1.1.1w/crypto/idea/i_cfb64.c
openssl-1.1.1w/crypto/idea/i_ecb.c
openssl-1.1.1w/crypto/idea/i_ofb64.c
openssl-1.1.1w/crypto/idea/i_skey.c
openssl-1.1.1w/crypto/idea/idea_local.h
openssl-1.1.1w/crypto/init.c
openssl-1.1.1w/crypto/kdf/
openssl-1.1.1w/crypto/kdf/build.info
openssl-1.1.1w/crypto/kdf/hkdf.c
openssl-1.1.1w/crypto/kdf/kdf_err.c
openssl-1.1.1w/crypto/kdf/scrypt.c
openssl-1.1.1w/crypto/kdf/tls1_prf.c
openssl-1.1.1w/crypto/lhash/
openssl-1.1.1w/crypto/lhash/build.info
openssl-1.1.1w/crypto/lhash/lh_stats.c
openssl-1.1.1w/crypto/lhash/lhash.c
openssl-1.1.1w/crypto/lhash/lhash_local.h
openssl-1.1.1w/crypto/md2/
openssl-1.1.1w/crypto/md2/build.info
openssl-1.1.1w/crypto/md2/md2_dgst.c
openssl-1.1.1w/crypto/md2/md2_one.c
openssl-1.1.1w/crypto/md4/
openssl-1.1.1w/crypto/md4/build.info
openssl-1.1.1w/crypto/md4/md4_dgst.c
openssl-1.1.1w/crypto/md4/md4_local.h
openssl-1.1.1w/crypto/md4/md4_one.c
openssl-1.1.1w/crypto/md5/
openssl-1.1.1w/crypto/md5/asm/
openssl-1.1.1w/crypto/md5/asm/md5-586.pl
openssl-1.1.1w/crypto/md5/asm/md5-sparcv9.pl
openssl-1.1.1w/crypto/md5/asm/md5-x86_64.pl
openssl-1.1.1w/crypto/md5/build.info
openssl-1.1.1w/crypto/md5/md5_dgst.c
openssl-1.1.1w/crypto/md5/md5_local.h
openssl-1.1.1w/crypto/md5/md5_one.c
openssl-1.1.1w/crypto/mdc2/
openssl-1.1.1w/crypto/mdc2/build.info
openssl-1.1.1w/crypto/mdc2/mdc2_one.c
openssl-1.1.1w/crypto/mdc2/mdc2dgst.c
openssl-1.1.1w/crypto/mem.c
openssl-1.1.1w/crypto/mem_clr.c
openssl-1.1.1w/crypto/mem_dbg.c
openssl-1.1.1w/crypto/mem_sec.c
openssl-1.1.1w/crypto/mips_arch.h
openssl-1.1.1w/crypto/modes/
openssl-1.1.1w/crypto/modes/asm/
openssl-1.1.1w/crypto/modes/asm/aesni-gcm-x86_64.pl
openssl-1.1.1w/crypto/modes/asm/ghash-alpha.pl
openssl-1.1.1w/crypto/modes/asm/ghash-armv4.pl
openssl-1.1.1w/crypto/modes/asm/ghash-c64xplus.pl
openssl-1.1.1w/crypto/modes/asm/ghash-ia64.pl
openssl-1.1.1w/crypto/modes/asm/ghash-parisc.pl
openssl-1.1.1w/crypto/modes/asm/ghash-s390x.pl
openssl-1.1.1w/crypto/modes/asm/ghash-sparcv9.pl
openssl-1.1.1w/crypto/modes/asm/ghash-x86.pl
openssl-1.1.1w/crypto/modes/asm/ghash-x86_64.pl
openssl-1.1.1w/crypto/modes/asm/ghashp8-ppc.pl
openssl-1.1.1w/crypto/modes/asm/ghashv8-armx.pl
openssl-1.1.1w/crypto/modes/build.info
openssl-1.1.1w/crypto/modes/cbc128.c
openssl-1.1.1w/crypto/modes/ccm128.c
openssl-1.1.1w/crypto/modes/cfb128.c
openssl-1.1.1w/crypto/modes/ctr128.c
openssl-1.1.1w/crypto/modes/cts128.c
openssl-1.1.1w/crypto/modes/gcm128.c
openssl-1.1.1w/crypto/modes/modes_local.h
openssl-1.1.1w/crypto/modes/ocb128.c
openssl-1.1.1w/crypto/modes/ofb128.c
openssl-1.1.1w/crypto/modes/wrap128.c
openssl-1.1.1w/crypto/modes/xts128.c
openssl-1.1.1w/crypto/o_dir.c
openssl-1.1.1w/crypto/o_fips.c
openssl-1.1.1w/crypto/o_fopen.c
openssl-1.1.1w/crypto/o_init.c
openssl-1.1.1w/crypto/o_str.c
openssl-1.1.1w/crypto/o_time.c
openssl-1.1.1w/crypto/objects/
openssl-1.1.1w/crypto/objects/README
openssl-1.1.1w/crypto/objects/build.info
openssl-1.1.1w/crypto/objects/o_names.c
openssl-1.1.1w/crypto/objects/obj_dat.c
openssl-1.1.1w/crypto/objects/obj_dat.h
openssl-1.1.1w/crypto/objects/obj_dat.pl
openssl-1.1.1w/crypto/objects/obj_err.c
openssl-1.1.1w/crypto/objects/obj_lib.c
openssl-1.1.1w/crypto/objects/obj_local.h
openssl-1.1.1w/crypto/objects/obj_mac.num
openssl-1.1.1w/crypto/objects/obj_xref.c
openssl-1.1.1w/crypto/objects/obj_xref.h
openssl-1.1.1w/crypto/objects/obj_xref.txt
openssl-1.1.1w/crypto/objects/objects.pl
openssl-1.1.1w/crypto/objects/objects.txt
openssl-1.1.1w/crypto/objects/objxref.pl
openssl-1.1.1w/crypto/ocsp/
openssl-1.1.1w/crypto/ocsp/build.info
openssl-1.1.1w/crypto/ocsp/ocsp_asn.c
openssl-1.1.1w/crypto/ocsp/ocsp_cl.c
openssl-1.1.1w/crypto/ocsp/ocsp_err.c
openssl-1.1.1w/crypto/ocsp/ocsp_ext.c
openssl-1.1.1w/crypto/ocsp/ocsp_ht.c
openssl-1.1.1w/crypto/ocsp/ocsp_lib.c
openssl-1.1.1w/crypto/ocsp/ocsp_local.h
openssl-1.1.1w/crypto/ocsp/ocsp_prn.c
openssl-1.1.1w/crypto/ocsp/ocsp_srv.c
openssl-1.1.1w/crypto/ocsp/ocsp_vfy.c
openssl-1.1.1w/crypto/ocsp/v3_ocsp.c
openssl-1.1.1w/crypto/pariscid.pl
openssl-1.1.1w/crypto/pem/
openssl-1.1.1w/crypto/pem/build.info
openssl-1.1.1w/crypto/pem/pem_all.c
openssl-1.1.1w/crypto/pem/pem_err.c
openssl-1.1.1w/crypto/pem/pem_info.c
openssl-1.1.1w/crypto/pem/pem_lib.c
openssl-1.1.1w/crypto/pem/pem_oth.c
openssl-1.1.1w/crypto/pem/pem_pk8.c
openssl-1.1.1w/crypto/pem/pem_pkey.c
openssl-1.1.1w/crypto/pem/pem_sign.c
openssl-1.1.1w/crypto/pem/pem_x509.c
openssl-1.1.1w/crypto/pem/pem_xaux.c
openssl-1.1.1w/crypto/pem/pvkfmt.c
openssl-1.1.1w/crypto/perlasm/
openssl-1.1.1w/crypto/perlasm/README
openssl-1.1.1w/crypto/perlasm/arm-xlate.pl
openssl-1.1.1w/crypto/perlasm/cbc.pl
openssl-1.1.1w/crypto/perlasm/ppc-xlate.pl
openssl-1.1.1w/crypto/perlasm/sparcv9_modes.pl
openssl-1.1.1w/crypto/perlasm/x86_64-xlate.pl
openssl-1.1.1w/crypto/perlasm/x86asm.pl
openssl-1.1.1w/crypto/perlasm/x86gas.pl
openssl-1.1.1w/crypto/perlasm/x86masm.pl
openssl-1.1.1w/crypto/perlasm/x86nasm.pl
openssl-1.1.1w/crypto/pkcs12/
openssl-1.1.1w/crypto/pkcs12/build.info
openssl-1.1.1w/crypto/pkcs12/p12_add.c
openssl-1.1.1w/crypto/pkcs12/p12_asn.c
openssl-1.1.1w/crypto/pkcs12/p12_attr.c
openssl-1.1.1w/crypto/pkcs12/p12_crpt.c
openssl-1.1.1w/crypto/pkcs12/p12_crt.c
openssl-1.1.1w/crypto/pkcs12/p12_decr.c
openssl-1.1.1w/crypto/pkcs12/p12_init.c
openssl-1.1.1w/crypto/pkcs12/p12_key.c
openssl-1.1.1w/crypto/pkcs12/p12_kiss.c
openssl-1.1.1w/crypto/pkcs12/p12_local.h
openssl-1.1.1w/crypto/pkcs12/p12_mutl.c
openssl-1.1.1w/crypto/pkcs12/p12_npas.c
openssl-1.1.1w/crypto/pkcs12/p12_p8d.c
openssl-1.1.1w/crypto/pkcs12/p12_p8e.c
openssl-1.1.1w/crypto/pkcs12/p12_sbag.c
openssl-1.1.1w/crypto/pkcs12/p12_utl.c
openssl-1.1.1w/crypto/pkcs12/pk12err.c
openssl-1.1.1w/crypto/pkcs7/
openssl-1.1.1w/crypto/pkcs7/bio_pk7.c
openssl-1.1.1w/crypto/pkcs7/build.info
openssl-1.1.1w/crypto/pkcs7/pk7_asn1.c
openssl-1.1.1w/crypto/pkcs7/pk7_attr.c
openssl-1.1.1w/crypto/pkcs7/pk7_doit.c
openssl-1.1.1w/crypto/pkcs7/pk7_lib.c
openssl-1.1.1w/crypto/pkcs7/pk7_mime.c
openssl-1.1.1w/crypto/pkcs7/pk7_smime.c
openssl-1.1.1w/crypto/pkcs7/pkcs7err.c
openssl-1.1.1w/crypto/poly1305/
openssl-1.1.1w/crypto/poly1305/asm/
openssl-1.1.1w/crypto/poly1305/asm/poly1305-armv4.pl
openssl-1.1.1w/crypto/poly1305/asm/poly1305-armv8.pl
openssl-1.1.1w/crypto/poly1305/asm/poly1305-c64xplus.pl
openssl-1.1.1w/crypto/poly1305/asm/poly1305-mips.pl
openssl-1.1.1w/crypto/poly1305/asm/poly1305-ppc.pl
openssl-1.1.1w/crypto/poly1305/asm/poly1305-ppcfp.pl
openssl-1.1.1w/crypto/poly1305/asm/poly1305-s390x.pl
openssl-1.1.1w/crypto/poly1305/asm/poly1305-sparcv9.pl
openssl-1.1.1w/crypto/poly1305/asm/poly1305-x86.pl
openssl-1.1.1w/crypto/poly1305/asm/poly1305-x86_64.pl
openssl-1.1.1w/crypto/poly1305/build.info
openssl-1.1.1w/crypto/poly1305/poly1305.c
openssl-1.1.1w/crypto/poly1305/poly1305_ameth.c
openssl-1.1.1w/crypto/poly1305/poly1305_base2_44.c
openssl-1.1.1w/crypto/poly1305/poly1305_ieee754.c
openssl-1.1.1w/crypto/poly1305/poly1305_local.h
openssl-1.1.1w/crypto/poly1305/poly1305_pmeth.c
openssl-1.1.1w/crypto/ppc_arch.h
openssl-1.1.1w/crypto/ppccap.c
openssl-1.1.1w/crypto/ppccpuid.pl
openssl-1.1.1w/crypto/rand/
openssl-1.1.1w/crypto/rand/build.info
openssl-1.1.1w/crypto/rand/drbg_ctr.c
openssl-1.1.1w/crypto/rand/drbg_lib.c
openssl-1.1.1w/crypto/rand/rand_egd.c
openssl-1.1.1w/crypto/rand/rand_err.c
openssl-1.1.1w/crypto/rand/rand_lib.c
openssl-1.1.1w/crypto/rand/rand_local.h
openssl-1.1.1w/crypto/rand/rand_unix.c
openssl-1.1.1w/crypto/rand/rand_vms.c
openssl-1.1.1w/crypto/rand/rand_win.c
openssl-1.1.1w/crypto/rand/randfile.c
openssl-1.1.1w/crypto/rc2/
openssl-1.1.1w/crypto/rc2/build.info
openssl-1.1.1w/crypto/rc2/rc2_cbc.c
openssl-1.1.1w/crypto/rc2/rc2_ecb.c
openssl-1.1.1w/crypto/rc2/rc2_local.h
openssl-1.1.1w/crypto/rc2/rc2_skey.c
openssl-1.1.1w/crypto/rc2/rc2cfb64.c
openssl-1.1.1w/crypto/rc2/rc2ofb64.c
openssl-1.1.1w/crypto/rc4/
openssl-1.1.1w/crypto/rc4/asm/
openssl-1.1.1w/crypto/rc4/asm/rc4-586.pl
openssl-1.1.1w/crypto/rc4/asm/rc4-c64xplus.pl
openssl-1.1.1w/crypto/rc4/asm/rc4-md5-x86_64.pl
openssl-1.1.1w/crypto/rc4/asm/rc4-parisc.pl
openssl-1.1.1w/crypto/rc4/asm/rc4-s390x.pl
openssl-1.1.1w/crypto/rc4/asm/rc4-x86_64.pl
openssl-1.1.1w/crypto/rc4/build.info
openssl-1.1.1w/crypto/rc4/rc4_enc.c
openssl-1.1.1w/crypto/rc4/rc4_local.h
openssl-1.1.1w/crypto/rc4/rc4_skey.c
openssl-1.1.1w/crypto/rc5/
openssl-1.1.1w/crypto/rc5/asm/
openssl-1.1.1w/crypto/rc5/asm/rc5-586.pl
openssl-1.1.1w/crypto/rc5/build.info
openssl-1.1.1w/crypto/rc5/rc5_ecb.c
openssl-1.1.1w/crypto/rc5/rc5_enc.c
openssl-1.1.1w/crypto/rc5/rc5_local.h
openssl-1.1.1w/crypto/rc5/rc5_skey.c
openssl-1.1.1w/crypto/rc5/rc5cfb64.c
openssl-1.1.1w/crypto/rc5/rc5ofb64.c
openssl-1.1.1w/crypto/ripemd/
openssl-1.1.1w/crypto/ripemd/asm/
openssl-1.1.1w/crypto/ripemd/asm/rmd-586.pl
openssl-1.1.1w/crypto/ripemd/build.info
openssl-1.1.1w/crypto/ripemd/rmd_dgst.c
openssl-1.1.1w/crypto/ripemd/rmd_local.h
openssl-1.1.1w/crypto/ripemd/rmd_one.c
openssl-1.1.1w/crypto/ripemd/rmdconst.h
openssl-1.1.1w/crypto/rsa/
openssl-1.1.1w/crypto/rsa/build.info
openssl-1.1.1w/crypto/rsa/rsa_ameth.c
openssl-1.1.1w/crypto/rsa/rsa_asn1.c
openssl-1.1.1w/crypto/rsa/rsa_chk.c
openssl-1.1.1w/crypto/rsa/rsa_crpt.c
openssl-1.1.1w/crypto/rsa/rsa_depr.c
openssl-1.1.1w/crypto/rsa/rsa_err.c
openssl-1.1.1w/crypto/rsa/rsa_gen.c
openssl-1.1.1w/crypto/rsa/rsa_lib.c
openssl-1.1.1w/crypto/rsa/rsa_local.h
openssl-1.1.1w/crypto/rsa/rsa_meth.c
openssl-1.1.1w/crypto/rsa/rsa_mp.c
openssl-1.1.1w/crypto/rsa/rsa_none.c
openssl-1.1.1w/crypto/rsa/rsa_oaep.c
openssl-1.1.1w/crypto/rsa/rsa_ossl.c
openssl-1.1.1w/crypto/rsa/rsa_pk1.c
openssl-1.1.1w/crypto/rsa/rsa_pmeth.c
openssl-1.1.1w/crypto/rsa/rsa_prn.c
openssl-1.1.1w/crypto/rsa/rsa_pss.c
openssl-1.1.1w/crypto/rsa/rsa_saos.c
openssl-1.1.1w/crypto/rsa/rsa_sign.c
openssl-1.1.1w/crypto/rsa/rsa_ssl.c
openssl-1.1.1w/crypto/rsa/rsa_x931.c
openssl-1.1.1w/crypto/rsa/rsa_x931g.c
openssl-1.1.1w/crypto/s390x_arch.h
openssl-1.1.1w/crypto/s390xcap.c
openssl-1.1.1w/crypto/s390xcpuid.pl
openssl-1.1.1w/crypto/seed/
openssl-1.1.1w/crypto/seed/build.info
openssl-1.1.1w/crypto/seed/seed.c
openssl-1.1.1w/crypto/seed/seed_cbc.c
openssl-1.1.1w/crypto/seed/seed_cfb.c
openssl-1.1.1w/crypto/seed/seed_ecb.c
openssl-1.1.1w/crypto/seed/seed_local.h
openssl-1.1.1w/crypto/seed/seed_ofb.c
openssl-1.1.1w/crypto/sha/
openssl-1.1.1w/crypto/sha/asm/
openssl-1.1.1w/crypto/sha/asm/keccak1600-armv4.pl
openssl-1.1.1w/crypto/sha/asm/keccak1600-armv8.pl
openssl-1.1.1w/crypto/sha/asm/keccak1600-avx2.pl
openssl-1.1.1w/crypto/sha/asm/keccak1600-avx512.pl
openssl-1.1.1w/crypto/sha/asm/keccak1600-avx512vl.pl
openssl-1.1.1w/crypto/sha/asm/keccak1600-c64x.pl
openssl-1.1.1w/crypto/sha/asm/keccak1600-mmx.pl
openssl-1.1.1w/crypto/sha/asm/keccak1600-ppc64.pl
openssl-1.1.1w/crypto/sha/asm/keccak1600-s390x.pl
openssl-1.1.1w/crypto/sha/asm/keccak1600-x86_64.pl
openssl-1.1.1w/crypto/sha/asm/keccak1600p8-ppc.pl
openssl-1.1.1w/crypto/sha/asm/sha1-586.pl
openssl-1.1.1w/crypto/sha/asm/sha1-alpha.pl
openssl-1.1.1w/crypto/sha/asm/sha1-armv4-large.pl
openssl-1.1.1w/crypto/sha/asm/sha1-armv8.pl
openssl-1.1.1w/crypto/sha/asm/sha1-c64xplus.pl
openssl-1.1.1w/crypto/sha/asm/sha1-ia64.pl
openssl-1.1.1w/crypto/sha/asm/sha1-mb-x86_64.pl
openssl-1.1.1w/crypto/sha/asm/sha1-mips.pl
openssl-1.1.1w/crypto/sha/asm/sha1-parisc.pl
openssl-1.1.1w/crypto/sha/asm/sha1-ppc.pl
openssl-1.1.1w/crypto/sha/asm/sha1-s390x.pl
openssl-1.1.1w/crypto/sha/asm/sha1-sparcv9.pl
openssl-1.1.1w/crypto/sha/asm/sha1-sparcv9a.pl
openssl-1.1.1w/crypto/sha/asm/sha1-thumb.pl
openssl-1.1.1w/crypto/sha/asm/sha1-x86_64.pl
openssl-1.1.1w/crypto/sha/asm/sha256-586.pl
openssl-1.1.1w/crypto/sha/asm/sha256-armv4.pl
openssl-1.1.1w/crypto/sha/asm/sha256-c64xplus.pl
openssl-1.1.1w/crypto/sha/asm/sha256-mb-x86_64.pl
openssl-1.1.1w/crypto/sha/asm/sha512-586.pl
openssl-1.1.1w/crypto/sha/asm/sha512-armv4.pl
openssl-1.1.1w/crypto/sha/asm/sha512-armv8.pl
openssl-1.1.1w/crypto/sha/asm/sha512-c64xplus.pl
openssl-1.1.1w/crypto/sha/asm/sha512-ia64.pl
openssl-1.1.1w/crypto/sha/asm/sha512-mips.pl
openssl-1.1.1w/crypto/sha/asm/sha512-parisc.pl
openssl-1.1.1w/crypto/sha/asm/sha512-ppc.pl
openssl-1.1.1w/crypto/sha/asm/sha512-s390x.pl
openssl-1.1.1w/crypto/sha/asm/sha512-sparcv9.pl
openssl-1.1.1w/crypto/sha/asm/sha512-x86_64.pl
openssl-1.1.1w/crypto/sha/asm/sha512p8-ppc.pl
openssl-1.1.1w/crypto/sha/build.info
openssl-1.1.1w/crypto/sha/keccak1600.c
openssl-1.1.1w/crypto/sha/sha1_one.c
openssl-1.1.1w/crypto/sha/sha1dgst.c
openssl-1.1.1w/crypto/sha/sha256.c
openssl-1.1.1w/crypto/sha/sha512.c
openssl-1.1.1w/crypto/sha/sha_local.h
openssl-1.1.1w/crypto/siphash/
openssl-1.1.1w/crypto/siphash/build.info
openssl-1.1.1w/crypto/siphash/siphash.c
openssl-1.1.1w/crypto/siphash/siphash_ameth.c
openssl-1.1.1w/crypto/siphash/siphash_local.h
openssl-1.1.1w/crypto/siphash/siphash_pmeth.c
openssl-1.1.1w/crypto/sm2/
openssl-1.1.1w/crypto/sm2/build.info
openssl-1.1.1w/crypto/sm2/sm2_crypt.c
openssl-1.1.1w/crypto/sm2/sm2_err.c
openssl-1.1.1w/crypto/sm2/sm2_pmeth.c
openssl-1.1.1w/crypto/sm2/sm2_sign.c
openssl-1.1.1w/crypto/sm3/
openssl-1.1.1w/crypto/sm3/build.info
openssl-1.1.1w/crypto/sm3/m_sm3.c
openssl-1.1.1w/crypto/sm3/sm3.c
openssl-1.1.1w/crypto/sm3/sm3_local.h
openssl-1.1.1w/crypto/sm4/
openssl-1.1.1w/crypto/sm4/build.info
openssl-1.1.1w/crypto/sm4/sm4.c
openssl-1.1.1w/crypto/sparc_arch.h
openssl-1.1.1w/crypto/sparccpuid.S
openssl-1.1.1w/crypto/sparcv9cap.c
openssl-1.1.1w/crypto/srp/
openssl-1.1.1w/crypto/srp/build.info
openssl-1.1.1w/crypto/srp/srp_lib.c
openssl-1.1.1w/crypto/srp/srp_vfy.c
openssl-1.1.1w/crypto/stack/
openssl-1.1.1w/crypto/stack/build.info
openssl-1.1.1w/crypto/stack/stack.c
openssl-1.1.1w/crypto/store/
openssl-1.1.1w/crypto/store/build.info
openssl-1.1.1w/crypto/store/loader_file.c
openssl-1.1.1w/crypto/store/store_err.c
openssl-1.1.1w/crypto/store/store_init.c
openssl-1.1.1w/crypto/store/store_lib.c
openssl-1.1.1w/crypto/store/store_local.h
openssl-1.1.1w/crypto/store/store_register.c
openssl-1.1.1w/crypto/store/store_strings.c
openssl-1.1.1w/crypto/threads_none.c
openssl-1.1.1w/crypto/threads_pthread.c
openssl-1.1.1w/crypto/threads_win.c
openssl-1.1.1w/crypto/ts/
openssl-1.1.1w/crypto/ts/build.info
openssl-1.1.1w/crypto/ts/ts_asn1.c
openssl-1.1.1w/crypto/ts/ts_conf.c
openssl-1.1.1w/crypto/ts/ts_err.c
openssl-1.1.1w/crypto/ts/ts_lib.c
openssl-1.1.1w/crypto/ts/ts_local.h
openssl-1.1.1w/crypto/ts/ts_req_print.c
openssl-1.1.1w/crypto/ts/ts_req_utils.c
openssl-1.1.1w/crypto/ts/ts_rsp_print.c
openssl-1.1.1w/crypto/ts/ts_rsp_sign.c
openssl-1.1.1w/crypto/ts/ts_rsp_utils.c
openssl-1.1.1w/crypto/ts/ts_rsp_verify.c
openssl-1.1.1w/crypto/ts/ts_verify_ctx.c
openssl-1.1.1w/crypto/txt_db/
openssl-1.1.1w/crypto/txt_db/build.info
openssl-1.1.1w/crypto/txt_db/txt_db.c
openssl-1.1.1w/crypto/ui/
openssl-1.1.1w/crypto/ui/build.info
openssl-1.1.1w/crypto/ui/ui_err.c
openssl-1.1.1w/crypto/ui/ui_lib.c
openssl-1.1.1w/crypto/ui/ui_local.h
openssl-1.1.1w/crypto/ui/ui_null.c
openssl-1.1.1w/crypto/ui/ui_openssl.c
openssl-1.1.1w/crypto/ui/ui_util.c
openssl-1.1.1w/crypto/uid.c
openssl-1.1.1w/crypto/vms_rms.h
openssl-1.1.1w/crypto/whrlpool/
openssl-1.1.1w/crypto/whrlpool/asm/
openssl-1.1.1w/crypto/whrlpool/asm/wp-mmx.pl
openssl-1.1.1w/crypto/whrlpool/asm/wp-x86_64.pl
openssl-1.1.1w/crypto/whrlpool/build.info
openssl-1.1.1w/crypto/whrlpool/wp_block.c
openssl-1.1.1w/crypto/whrlpool/wp_dgst.c
openssl-1.1.1w/crypto/whrlpool/wp_local.h
openssl-1.1.1w/crypto/x509/
openssl-1.1.1w/crypto/x509/build.info
openssl-1.1.1w/crypto/x509/by_dir.c
openssl-1.1.1w/crypto/x509/by_file.c
openssl-1.1.1w/crypto/x509/t_crl.c
openssl-1.1.1w/crypto/x509/t_req.c
openssl-1.1.1w/crypto/x509/t_x509.c
openssl-1.1.1w/crypto/x509/x509_att.c
openssl-1.1.1w/crypto/x509/x509_cmp.c
openssl-1.1.1w/crypto/x509/x509_d2.c
openssl-1.1.1w/crypto/x509/x509_def.c
openssl-1.1.1w/crypto/x509/x509_err.c
openssl-1.1.1w/crypto/x509/x509_ext.c
openssl-1.1.1w/crypto/x509/x509_local.h
openssl-1.1.1w/crypto/x509/x509_lu.c
openssl-1.1.1w/crypto/x509/x509_meth.c
openssl-1.1.1w/crypto/x509/x509_obj.c
openssl-1.1.1w/crypto/x509/x509_r2x.c
openssl-1.1.1w/crypto/x509/x509_req.c
openssl-1.1.1w/crypto/x509/x509_set.c
openssl-1.1.1w/crypto/x509/x509_trs.c
openssl-1.1.1w/crypto/x509/x509_txt.c
openssl-1.1.1w/crypto/x509/x509_v3.c
openssl-1.1.1w/crypto/x509/x509_vfy.c
openssl-1.1.1w/crypto/x509/x509_vpm.c
openssl-1.1.1w/crypto/x509/x509cset.c
openssl-1.1.1w/crypto/x509/x509name.c
openssl-1.1.1w/crypto/x509/x509rset.c
openssl-1.1.1w/crypto/x509/x509spki.c
openssl-1.1.1w/crypto/x509/x509type.c
openssl-1.1.1w/crypto/x509/x_all.c
openssl-1.1.1w/crypto/x509/x_attrib.c
openssl-1.1.1w/crypto/x509/x_crl.c
openssl-1.1.1w/crypto/x509/x_exten.c
openssl-1.1.1w/crypto/x509/x_name.c
openssl-1.1.1w/crypto/x509/x_pubkey.c
openssl-1.1.1w/crypto/x509/x_req.c
openssl-1.1.1w/crypto/x509/x_x509.c
openssl-1.1.1w/crypto/x509/x_x509a.c
openssl-1.1.1w/crypto/x509v3/
openssl-1.1.1w/crypto/x509v3/build.info
openssl-1.1.1w/crypto/x509v3/ext_dat.h
openssl-1.1.1w/crypto/x509v3/pcy_cache.c
openssl-1.1.1w/crypto/x509v3/pcy_data.c
openssl-1.1.1w/crypto/x509v3/pcy_lib.c
openssl-1.1.1w/crypto/x509v3/pcy_local.h
openssl-1.1.1w/crypto/x509v3/pcy_map.c
openssl-1.1.1w/crypto/x509v3/pcy_node.c
openssl-1.1.1w/crypto/x509v3/pcy_tree.c
openssl-1.1.1w/crypto/x509v3/standard_exts.h
openssl-1.1.1w/crypto/x509v3/v3_addr.c
openssl-1.1.1w/crypto/x509v3/v3_admis.c
openssl-1.1.1w/crypto/x509v3/v3_admis.h
openssl-1.1.1w/crypto/x509v3/v3_akey.c
openssl-1.1.1w/crypto/x509v3/v3_akeya.c
openssl-1.1.1w/crypto/x509v3/v3_alt.c
openssl-1.1.1w/crypto/x509v3/v3_asid.c
openssl-1.1.1w/crypto/x509v3/v3_bcons.c
openssl-1.1.1w/crypto/x509v3/v3_bitst.c
openssl-1.1.1w/crypto/x509v3/v3_conf.c
openssl-1.1.1w/crypto/x509v3/v3_cpols.c
openssl-1.1.1w/crypto/x509v3/v3_crld.c
openssl-1.1.1w/crypto/x509v3/v3_enum.c
openssl-1.1.1w/crypto/x509v3/v3_extku.c
openssl-1.1.1w/crypto/x509v3/v3_genn.c
openssl-1.1.1w/crypto/x509v3/v3_ia5.c
openssl-1.1.1w/crypto/x509v3/v3_info.c
openssl-1.1.1w/crypto/x509v3/v3_int.c
openssl-1.1.1w/crypto/x509v3/v3_lib.c
openssl-1.1.1w/crypto/x509v3/v3_ncons.c
openssl-1.1.1w/crypto/x509v3/v3_pci.c
openssl-1.1.1w/crypto/x509v3/v3_pcia.c
openssl-1.1.1w/crypto/x509v3/v3_pcons.c
openssl-1.1.1w/crypto/x509v3/v3_pku.c
openssl-1.1.1w/crypto/x509v3/v3_pmaps.c
openssl-1.1.1w/crypto/x509v3/v3_prn.c
openssl-1.1.1w/crypto/x509v3/v3_purp.c
openssl-1.1.1w/crypto/x509v3/v3_skey.c
openssl-1.1.1w/crypto/x509v3/v3_sxnet.c
openssl-1.1.1w/crypto/x509v3/v3_tlsf.c
openssl-1.1.1w/crypto/x509v3/v3_utl.c
openssl-1.1.1w/crypto/x509v3/v3err.c
openssl-1.1.1w/crypto/x86_64cpuid.pl
openssl-1.1.1w/crypto/x86cpuid.pl
openssl-1.1.1w/demos/
openssl-1.1.1w/demos/README
openssl-1.1.1w/demos/bio/
openssl-1.1.1w/demos/bio/Makefile
openssl-1.1.1w/demos/bio/README
openssl-1.1.1w/demos/bio/accept.cnf
openssl-1.1.1w/demos/bio/client-arg.c
openssl-1.1.1w/demos/bio/client-conf.c
openssl-1.1.1w/demos/bio/cmod.cnf
openssl-1.1.1w/demos/bio/connect.cnf
openssl-1.1.1w/demos/bio/descrip.mms
openssl-1.1.1w/demos/bio/intca.pem
openssl-1.1.1w/demos/bio/root.pem
openssl-1.1.1w/demos/bio/saccept.c
openssl-1.1.1w/demos/bio/sconnect.c
openssl-1.1.1w/demos/bio/server-arg.c
openssl-1.1.1w/demos/bio/server-cmod.c
openssl-1.1.1w/demos/bio/server-conf.c
openssl-1.1.1w/demos/bio/server-ec.pem
openssl-1.1.1w/demos/bio/server.pem
openssl-1.1.1w/demos/bio/shared.opt
openssl-1.1.1w/demos/bio/static.opt
openssl-1.1.1w/demos/certs/
openssl-1.1.1w/demos/certs/README
openssl-1.1.1w/demos/certs/apps/
openssl-1.1.1w/demos/certs/apps/apps.cnf
openssl-1.1.1w/demos/certs/apps/ckey.pem
openssl-1.1.1w/demos/certs/apps/intkey.pem
openssl-1.1.1w/demos/certs/apps/mkacerts.sh
openssl-1.1.1w/demos/certs/apps/mkxcerts.sh
openssl-1.1.1w/demos/certs/apps/rootkey.pem
openssl-1.1.1w/demos/certs/apps/skey.pem
openssl-1.1.1w/demos/certs/apps/skey2.pem
openssl-1.1.1w/demos/certs/ca.cnf
openssl-1.1.1w/demos/certs/mkcerts.sh
openssl-1.1.1w/demos/certs/ocspquery.sh
openssl-1.1.1w/demos/certs/ocsprun.sh
openssl-1.1.1w/demos/cms/
openssl-1.1.1w/demos/cms/cacert.pem
openssl-1.1.1w/demos/cms/cakey.pem
openssl-1.1.1w/demos/cms/cms_comp.c
openssl-1.1.1w/demos/cms/cms_ddec.c
openssl-1.1.1w/demos/cms/cms_dec.c
openssl-1.1.1w/demos/cms/cms_denc.c
openssl-1.1.1w/demos/cms/cms_enc.c
openssl-1.1.1w/demos/cms/cms_sign.c
openssl-1.1.1w/demos/cms/cms_sign2.c
openssl-1.1.1w/demos/cms/cms_uncomp.c
openssl-1.1.1w/demos/cms/cms_ver.c
openssl-1.1.1w/demos/cms/comp.txt
openssl-1.1.1w/demos/cms/encr.txt
openssl-1.1.1w/demos/cms/sign.txt
openssl-1.1.1w/demos/cms/signer.pem
openssl-1.1.1w/demos/cms/signer2.pem
openssl-1.1.1w/demos/engines/
openssl-1.1.1w/demos/engines/e_chil.txt
openssl-1.1.1w/demos/evp/
openssl-1.1.1w/demos/evp/Makefile
openssl-1.1.1w/demos/evp/aesccm.c
openssl-1.1.1w/demos/evp/aesgcm.c
openssl-1.1.1w/demos/pkcs12/
openssl-1.1.1w/demos/pkcs12/pkread.c
openssl-1.1.1w/demos/pkcs12/pkwrite.c
openssl-1.1.1w/demos/smime/
openssl-1.1.1w/demos/smime/cacert.pem
openssl-1.1.1w/demos/smime/cakey.pem
openssl-1.1.1w/demos/smime/encr.txt
openssl-1.1.1w/demos/smime/sign.txt
openssl-1.1.1w/demos/smime/signer.pem
openssl-1.1.1w/demos/smime/signer2.pem
openssl-1.1.1w/demos/smime/smdec.c
openssl-1.1.1w/demos/smime/smenc.c
openssl-1.1.1w/demos/smime/smsign.c
openssl-1.1.1w/demos/smime/smsign2.c
openssl-1.1.1w/demos/smime/smver.c
openssl-1.1.1w/doc/
openssl-1.1.1w/doc/HOWTO/
openssl-1.1.1w/doc/HOWTO/certificates.txt
openssl-1.1.1w/doc/HOWTO/keys.txt
openssl-1.1.1w/doc/README
openssl-1.1.1w/doc/dir-locals.example.el
openssl-1.1.1w/doc/fingerprints.txt
openssl-1.1.1w/doc/man1/
openssl-1.1.1w/doc/man1/CA.pl.pod
openssl-1.1.1w/doc/man1/asn1parse.pod
openssl-1.1.1w/doc/man1/ca.pod
openssl-1.1.1w/doc/man1/ciphers.pod
openssl-1.1.1w/doc/man1/cms.pod
openssl-1.1.1w/doc/man1/crl.pod
openssl-1.1.1w/doc/man1/crl2pkcs7.pod
openssl-1.1.1w/doc/man1/dgst.pod
openssl-1.1.1w/doc/man1/dhparam.pod
openssl-1.1.1w/doc/man1/dsa.pod
openssl-1.1.1w/doc/man1/dsaparam.pod
openssl-1.1.1w/doc/man1/ec.pod
openssl-1.1.1w/doc/man1/ecparam.pod
openssl-1.1.1w/doc/man1/enc.pod
openssl-1.1.1w/doc/man1/engine.pod
openssl-1.1.1w/doc/man1/errstr.pod
openssl-1.1.1w/doc/man1/gendsa.pod
openssl-1.1.1w/doc/man1/genpkey.pod
openssl-1.1.1w/doc/man1/genrsa.pod
openssl-1.1.1w/doc/man1/list.pod
openssl-1.1.1w/doc/man1/nseq.pod
openssl-1.1.1w/doc/man1/ocsp.pod
openssl-1.1.1w/doc/man1/openssl.pod
openssl-1.1.1w/doc/man1/passwd.pod
openssl-1.1.1w/doc/man1/pkcs12.pod
openssl-1.1.1w/doc/man1/pkcs7.pod
openssl-1.1.1w/doc/man1/pkcs8.pod
openssl-1.1.1w/doc/man1/pkey.pod
openssl-1.1.1w/doc/man1/pkeyparam.pod
openssl-1.1.1w/doc/man1/pkeyutl.pod
openssl-1.1.1w/doc/man1/prime.pod
openssl-1.1.1w/doc/man1/rand.pod
openssl-1.1.1w/doc/man1/rehash.pod
openssl-1.1.1w/doc/man1/req.pod
openssl-1.1.1w/doc/man1/rsa.pod
openssl-1.1.1w/doc/man1/rsautl.pod
openssl-1.1.1w/doc/man1/s_client.pod
openssl-1.1.1w/doc/man1/s_server.pod
openssl-1.1.1w/doc/man1/s_time.pod
openssl-1.1.1w/doc/man1/sess_id.pod
openssl-1.1.1w/doc/man1/smime.pod
openssl-1.1.1w/doc/man1/speed.pod
openssl-1.1.1w/doc/man1/spkac.pod
openssl-1.1.1w/doc/man1/srp.pod
openssl-1.1.1w/doc/man1/storeutl.pod
openssl-1.1.1w/doc/man1/ts.pod
openssl-1.1.1w/doc/man1/tsget.pod
openssl-1.1.1w/doc/man1/verify.pod
openssl-1.1.1w/doc/man1/version.pod
openssl-1.1.1w/doc/man1/x509.pod
openssl-1.1.1w/doc/man3/
openssl-1.1.1w/doc/man3/ADMISSIONS.pod
openssl-1.1.1w/doc/man3/ASN1_INTEGER_get_int64.pod
openssl-1.1.1w/doc/man3/ASN1_ITEM_lookup.pod
openssl-1.1.1w/doc/man3/ASN1_OBJECT_new.pod
openssl-1.1.1w/doc/man3/ASN1_STRING_TABLE_add.pod
openssl-1.1.1w/doc/man3/ASN1_STRING_length.pod
openssl-1.1.1w/doc/man3/ASN1_STRING_new.pod
openssl-1.1.1w/doc/man3/ASN1_STRING_print_ex.pod
openssl-1.1.1w/doc/man3/ASN1_TIME_set.pod
openssl-1.1.1w/doc/man3/ASN1_TYPE_get.pod
openssl-1.1.1w/doc/man3/ASN1_generate_nconf.pod
openssl-1.1.1w/doc/man3/ASYNC_WAIT_CTX_new.pod
openssl-1.1.1w/doc/man3/ASYNC_start_job.pod
openssl-1.1.1w/doc/man3/BF_encrypt.pod
openssl-1.1.1w/doc/man3/BIO_ADDR.pod
openssl-1.1.1w/doc/man3/BIO_ADDRINFO.pod
openssl-1.1.1w/doc/man3/BIO_connect.pod
openssl-1.1.1w/doc/man3/BIO_ctrl.pod
openssl-1.1.1w/doc/man3/BIO_f_base64.pod
openssl-1.1.1w/doc/man3/BIO_f_buffer.pod
openssl-1.1.1w/doc/man3/BIO_f_cipher.pod
openssl-1.1.1w/doc/man3/BIO_f_md.pod
openssl-1.1.1w/doc/man3/BIO_f_null.pod
openssl-1.1.1w/doc/man3/BIO_f_ssl.pod
openssl-1.1.1w/doc/man3/BIO_find_type.pod
openssl-1.1.1w/doc/man3/BIO_get_data.pod
openssl-1.1.1w/doc/man3/BIO_get_ex_new_index.pod
openssl-1.1.1w/doc/man3/BIO_meth_new.pod
openssl-1.1.1w/doc/man3/BIO_new.pod
openssl-1.1.1w/doc/man3/BIO_new_CMS.pod
openssl-1.1.1w/doc/man3/BIO_parse_hostserv.pod
openssl-1.1.1w/doc/man3/BIO_printf.pod
openssl-1.1.1w/doc/man3/BIO_push.pod
openssl-1.1.1w/doc/man3/BIO_read.pod
openssl-1.1.1w/doc/man3/BIO_s_accept.pod
openssl-1.1.1w/doc/man3/BIO_s_bio.pod
openssl-1.1.1w/doc/man3/BIO_s_connect.pod
openssl-1.1.1w/doc/man3/BIO_s_fd.pod
openssl-1.1.1w/doc/man3/BIO_s_file.pod
openssl-1.1.1w/doc/man3/BIO_s_mem.pod
openssl-1.1.1w/doc/man3/BIO_s_null.pod
openssl-1.1.1w/doc/man3/BIO_s_socket.pod
openssl-1.1.1w/doc/man3/BIO_set_callback.pod
openssl-1.1.1w/doc/man3/BIO_should_retry.pod
openssl-1.1.1w/doc/man3/BN_BLINDING_new.pod
openssl-1.1.1w/doc/man3/BN_CTX_new.pod
openssl-1.1.1w/doc/man3/BN_CTX_start.pod
openssl-1.1.1w/doc/man3/BN_add.pod
openssl-1.1.1w/doc/man3/BN_add_word.pod
openssl-1.1.1w/doc/man3/BN_bn2bin.pod
openssl-1.1.1w/doc/man3/BN_cmp.pod
openssl-1.1.1w/doc/man3/BN_copy.pod
openssl-1.1.1w/doc/man3/BN_generate_prime.pod
openssl-1.1.1w/doc/man3/BN_mod_inverse.pod
openssl-1.1.1w/doc/man3/BN_mod_mul_montgomery.pod
openssl-1.1.1w/doc/man3/BN_mod_mul_reciprocal.pod
openssl-1.1.1w/doc/man3/BN_new.pod
openssl-1.1.1w/doc/man3/BN_num_bytes.pod
openssl-1.1.1w/doc/man3/BN_rand.pod
openssl-1.1.1w/doc/man3/BN_security_bits.pod
openssl-1.1.1w/doc/man3/BN_set_bit.pod
openssl-1.1.1w/doc/man3/BN_swap.pod
openssl-1.1.1w/doc/man3/BN_zero.pod
openssl-1.1.1w/doc/man3/BUF_MEM_new.pod
openssl-1.1.1w/doc/man3/CMS_add0_cert.pod
openssl-1.1.1w/doc/man3/CMS_add1_recipient_cert.pod
openssl-1.1.1w/doc/man3/CMS_add1_signer.pod
openssl-1.1.1w/doc/man3/CMS_compress.pod
openssl-1.1.1w/doc/man3/CMS_decrypt.pod
openssl-1.1.1w/doc/man3/CMS_encrypt.pod
openssl-1.1.1w/doc/man3/CMS_final.pod
openssl-1.1.1w/doc/man3/CMS_get0_RecipientInfos.pod
openssl-1.1.1w/doc/man3/CMS_get0_SignerInfos.pod
openssl-1.1.1w/doc/man3/CMS_get0_type.pod
openssl-1.1.1w/doc/man3/CMS_get1_ReceiptRequest.pod
openssl-1.1.1w/doc/man3/CMS_sign.pod
openssl-1.1.1w/doc/man3/CMS_sign_receipt.pod
openssl-1.1.1w/doc/man3/CMS_uncompress.pod
openssl-1.1.1w/doc/man3/CMS_verify.pod
openssl-1.1.1w/doc/man3/CMS_verify_receipt.pod
openssl-1.1.1w/doc/man3/CONF_modules_free.pod
openssl-1.1.1w/doc/man3/CONF_modules_load_file.pod
openssl-1.1.1w/doc/man3/CRYPTO_THREAD_run_once.pod
openssl-1.1.1w/doc/man3/CRYPTO_get_ex_new_index.pod
openssl-1.1.1w/doc/man3/CRYPTO_memcmp.pod
openssl-1.1.1w/doc/man3/CTLOG_STORE_get0_log_by_id.pod
openssl-1.1.1w/doc/man3/CTLOG_STORE_new.pod
openssl-1.1.1w/doc/man3/CTLOG_new.pod
openssl-1.1.1w/doc/man3/CT_POLICY_EVAL_CTX_new.pod
openssl-1.1.1w/doc/man3/DEFINE_STACK_OF.pod
openssl-1.1.1w/doc/man3/DES_random_key.pod
openssl-1.1.1w/doc/man3/DH_generate_key.pod
openssl-1.1.1w/doc/man3/DH_generate_parameters.pod
openssl-1.1.1w/doc/man3/DH_get0_pqg.pod
openssl-1.1.1w/doc/man3/DH_get_1024_160.pod
openssl-1.1.1w/doc/man3/DH_meth_new.pod
openssl-1.1.1w/doc/man3/DH_new.pod
openssl-1.1.1w/doc/man3/DH_new_by_nid.pod
openssl-1.1.1w/doc/man3/DH_set_method.pod
openssl-1.1.1w/doc/man3/DH_size.pod
openssl-1.1.1w/doc/man3/DSA_SIG_new.pod
openssl-1.1.1w/doc/man3/DSA_do_sign.pod
openssl-1.1.1w/doc/man3/DSA_dup_DH.pod
openssl-1.1.1w/doc/man3/DSA_generate_key.pod
openssl-1.1.1w/doc/man3/DSA_generate_parameters.pod
openssl-1.1.1w/doc/man3/DSA_get0_pqg.pod
openssl-1.1.1w/doc/man3/DSA_meth_new.pod
openssl-1.1.1w/doc/man3/DSA_new.pod
openssl-1.1.1w/doc/man3/DSA_set_method.pod
openssl-1.1.1w/doc/man3/DSA_sign.pod
openssl-1.1.1w/doc/man3/DSA_size.pod
openssl-1.1.1w/doc/man3/DTLS_get_data_mtu.pod
openssl-1.1.1w/doc/man3/DTLS_set_timer_cb.pod
openssl-1.1.1w/doc/man3/DTLSv1_listen.pod
openssl-1.1.1w/doc/man3/ECDSA_SIG_new.pod
openssl-1.1.1w/doc/man3/ECPKParameters_print.pod
openssl-1.1.1w/doc/man3/EC_GFp_simple_method.pod
openssl-1.1.1w/doc/man3/EC_GROUP_copy.pod
openssl-1.1.1w/doc/man3/EC_GROUP_new.pod
openssl-1.1.1w/doc/man3/EC_KEY_get_enc_flags.pod
openssl-1.1.1w/doc/man3/EC_KEY_new.pod
openssl-1.1.1w/doc/man3/EC_POINT_add.pod
openssl-1.1.1w/doc/man3/EC_POINT_new.pod
openssl-1.1.1w/doc/man3/ENGINE_add.pod
openssl-1.1.1w/doc/man3/ERR_GET_LIB.pod
openssl-1.1.1w/doc/man3/ERR_clear_error.pod
openssl-1.1.1w/doc/man3/ERR_error_string.pod
openssl-1.1.1w/doc/man3/ERR_get_error.pod
openssl-1.1.1w/doc/man3/ERR_load_crypto_strings.pod
openssl-1.1.1w/doc/man3/ERR_load_strings.pod
openssl-1.1.1w/doc/man3/ERR_print_errors.pod
openssl-1.1.1w/doc/man3/ERR_put_error.pod
openssl-1.1.1w/doc/man3/ERR_remove_state.pod
openssl-1.1.1w/doc/man3/ERR_set_mark.pod
openssl-1.1.1w/doc/man3/EVP_BytesToKey.pod
openssl-1.1.1w/doc/man3/EVP_CIPHER_CTX_get_cipher_data.pod
openssl-1.1.1w/doc/man3/EVP_CIPHER_meth_new.pod
openssl-1.1.1w/doc/man3/EVP_DigestInit.pod
openssl-1.1.1w/doc/man3/EVP_DigestSignInit.pod
openssl-1.1.1w/doc/man3/EVP_DigestVerifyInit.pod
openssl-1.1.1w/doc/man3/EVP_EncodeInit.pod
openssl-1.1.1w/doc/man3/EVP_EncryptInit.pod
openssl-1.1.1w/doc/man3/EVP_MD_meth_new.pod
openssl-1.1.1w/doc/man3/EVP_OpenInit.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_ASN1_METHOD.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_CTX_ctrl.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_CTX_new.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_CTX_set1_pbe_pass.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_CTX_set_hkdf_md.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_CTX_set_rsa_pss_keygen_md.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_CTX_set_scrypt_N.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_CTX_set_tls1_prf_md.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_asn1_get_count.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_cmp.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_decrypt.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_derive.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_encrypt.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_get_default_digest_nid.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_keygen.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_meth_get_count.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_meth_new.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_new.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_print_private.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_set1_RSA.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_sign.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_size.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_verify.pod
openssl-1.1.1w/doc/man3/EVP_PKEY_verify_recover.pod
openssl-1.1.1w/doc/man3/EVP_SealInit.pod
openssl-1.1.1w/doc/man3/EVP_SignInit.pod
openssl-1.1.1w/doc/man3/EVP_VerifyInit.pod
openssl-1.1.1w/doc/man3/EVP_aes.pod
openssl-1.1.1w/doc/man3/EVP_aria.pod
openssl-1.1.1w/doc/man3/EVP_bf_cbc.pod
openssl-1.1.1w/doc/man3/EVP_blake2b512.pod
openssl-1.1.1w/doc/man3/EVP_camellia.pod
openssl-1.1.1w/doc/man3/EVP_cast5_cbc.pod
openssl-1.1.1w/doc/man3/EVP_chacha20.pod
openssl-1.1.1w/doc/man3/EVP_des.pod
openssl-1.1.1w/doc/man3/EVP_desx_cbc.pod
openssl-1.1.1w/doc/man3/EVP_idea_cbc.pod
openssl-1.1.1w/doc/man3/EVP_md2.pod
openssl-1.1.1w/doc/man3/EVP_md4.pod
openssl-1.1.1w/doc/man3/EVP_md5.pod
openssl-1.1.1w/doc/man3/EVP_mdc2.pod
openssl-1.1.1w/doc/man3/EVP_rc2_cbc.pod
openssl-1.1.1w/doc/man3/EVP_rc4.pod
openssl-1.1.1w/doc/man3/EVP_rc5_32_12_16_cbc.pod
openssl-1.1.1w/doc/man3/EVP_ripemd160.pod
openssl-1.1.1w/doc/man3/EVP_seed_cbc.pod
openssl-1.1.1w/doc/man3/EVP_sha1.pod
openssl-1.1.1w/doc/man3/EVP_sha224.pod
openssl-1.1.1w/doc/man3/EVP_sha3_224.pod
openssl-1.1.1w/doc/man3/EVP_sm3.pod
openssl-1.1.1w/doc/man3/EVP_sm4_cbc.pod
openssl-1.1.1w/doc/man3/EVP_whirlpool.pod
openssl-1.1.1w/doc/man3/HMAC.pod
openssl-1.1.1w/doc/man3/MD5.pod
openssl-1.1.1w/doc/man3/MDC2_Init.pod
openssl-1.1.1w/doc/man3/OBJ_nid2obj.pod
openssl-1.1.1w/doc/man3/OCSP_REQUEST_new.pod
openssl-1.1.1w/doc/man3/OCSP_cert_to_id.pod
openssl-1.1.1w/doc/man3/OCSP_request_add1_nonce.pod
openssl-1.1.1w/doc/man3/OCSP_resp_find_status.pod
openssl-1.1.1w/doc/man3/OCSP_response_status.pod
openssl-1.1.1w/doc/man3/OCSP_sendreq_new.pod
openssl-1.1.1w/doc/man3/OPENSSL_Applink.pod
openssl-1.1.1w/doc/man3/OPENSSL_LH_COMPFUNC.pod
openssl-1.1.1w/doc/man3/OPENSSL_LH_stats.pod
openssl-1.1.1w/doc/man3/OPENSSL_VERSION_NUMBER.pod
openssl-1.1.1w/doc/man3/OPENSSL_config.pod
openssl-1.1.1w/doc/man3/OPENSSL_fork_prepare.pod
openssl-1.1.1w/doc/man3/OPENSSL_ia32cap.pod
openssl-1.1.1w/doc/man3/OPENSSL_init_crypto.pod
openssl-1.1.1w/doc/man3/OPENSSL_init_ssl.pod
openssl-1.1.1w/doc/man3/OPENSSL_instrument_bus.pod
openssl-1.1.1w/doc/man3/OPENSSL_load_builtin_modules.pod
openssl-1.1.1w/doc/man3/OPENSSL_malloc.pod
openssl-1.1.1w/doc/man3/OPENSSL_secure_malloc.pod
openssl-1.1.1w/doc/man3/OSSL_STORE_INFO.pod
openssl-1.1.1w/doc/man3/OSSL_STORE_LOADER.pod
openssl-1.1.1w/doc/man3/OSSL_STORE_SEARCH.pod
openssl-1.1.1w/doc/man3/OSSL_STORE_expect.pod
openssl-1.1.1w/doc/man3/OSSL_STORE_open.pod
openssl-1.1.1w/doc/man3/OpenSSL_add_all_algorithms.pod
openssl-1.1.1w/doc/man3/PEM_bytes_read_bio.pod
openssl-1.1.1w/doc/man3/PEM_read.pod
openssl-1.1.1w/doc/man3/PEM_read_CMS.pod
openssl-1.1.1w/doc/man3/PEM_read_bio_PrivateKey.pod
openssl-1.1.1w/doc/man3/PEM_read_bio_ex.pod
openssl-1.1.1w/doc/man3/PEM_write_bio_CMS_stream.pod
openssl-1.1.1w/doc/man3/PEM_write_bio_PKCS7_stream.pod
openssl-1.1.1w/doc/man3/PKCS12_create.pod
openssl-1.1.1w/doc/man3/PKCS12_newpass.pod
openssl-1.1.1w/doc/man3/PKCS12_parse.pod
openssl-1.1.1w/doc/man3/PKCS5_PBKDF2_HMAC.pod
openssl-1.1.1w/doc/man3/PKCS7_decrypt.pod
openssl-1.1.1w/doc/man3/PKCS7_encrypt.pod
openssl-1.1.1w/doc/man3/PKCS7_sign.pod
openssl-1.1.1w/doc/man3/PKCS7_sign_add_signer.pod
openssl-1.1.1w/doc/man3/PKCS7_verify.pod
openssl-1.1.1w/doc/man3/RAND_DRBG_generate.pod
openssl-1.1.1w/doc/man3/RAND_DRBG_get0_master.pod
openssl-1.1.1w/doc/man3/RAND_DRBG_new.pod
openssl-1.1.1w/doc/man3/RAND_DRBG_reseed.pod
openssl-1.1.1w/doc/man3/RAND_DRBG_set_callbacks.pod
openssl-1.1.1w/doc/man3/RAND_DRBG_set_ex_data.pod
openssl-1.1.1w/doc/man3/RAND_add.pod
openssl-1.1.1w/doc/man3/RAND_bytes.pod
openssl-1.1.1w/doc/man3/RAND_cleanup.pod
openssl-1.1.1w/doc/man3/RAND_egd.pod
openssl-1.1.1w/doc/man3/RAND_load_file.pod
openssl-1.1.1w/doc/man3/RAND_set_rand_method.pod
openssl-1.1.1w/doc/man3/RC4_set_key.pod
openssl-1.1.1w/doc/man3/RIPEMD160_Init.pod
openssl-1.1.1w/doc/man3/RSA_blinding_on.pod
openssl-1.1.1w/doc/man3/RSA_check_key.pod
openssl-1.1.1w/doc/man3/RSA_generate_key.pod
openssl-1.1.1w/doc/man3/RSA_get0_key.pod
openssl-1.1.1w/doc/man3/RSA_meth_new.pod
openssl-1.1.1w/doc/man3/RSA_new.pod
openssl-1.1.1w/doc/man3/RSA_padding_add_PKCS1_type_1.pod
openssl-1.1.1w/doc/man3/RSA_print.pod
openssl-1.1.1w/doc/man3/RSA_private_encrypt.pod
openssl-1.1.1w/doc/man3/RSA_public_encrypt.pod
openssl-1.1.1w/doc/man3/RSA_set_method.pod
openssl-1.1.1w/doc/man3/RSA_sign.pod
openssl-1.1.1w/doc/man3/RSA_sign_ASN1_OCTET_STRING.pod
openssl-1.1.1w/doc/man3/RSA_size.pod
openssl-1.1.1w/doc/man3/SCT_new.pod
openssl-1.1.1w/doc/man3/SCT_print.pod
openssl-1.1.1w/doc/man3/SCT_validate.pod
openssl-1.1.1w/doc/man3/SHA256_Init.pod
openssl-1.1.1w/doc/man3/SMIME_read_CMS.pod
openssl-1.1.1w/doc/man3/SMIME_read_PKCS7.pod
openssl-1.1.1w/doc/man3/SMIME_write_CMS.pod
openssl-1.1.1w/doc/man3/SMIME_write_PKCS7.pod
openssl-1.1.1w/doc/man3/SSL_CIPHER_get_name.pod
openssl-1.1.1w/doc/man3/SSL_COMP_add_compression_method.pod
openssl-1.1.1w/doc/man3/SSL_CONF_CTX_new.pod
openssl-1.1.1w/doc/man3/SSL_CONF_CTX_set1_prefix.pod
openssl-1.1.1w/doc/man3/SSL_CONF_CTX_set_flags.pod
openssl-1.1.1w/doc/man3/SSL_CONF_CTX_set_ssl_ctx.pod
openssl-1.1.1w/doc/man3/SSL_CONF_cmd.pod
openssl-1.1.1w/doc/man3/SSL_CONF_cmd_argv.pod
openssl-1.1.1w/doc/man3/SSL_CTX_add1_chain_cert.pod
openssl-1.1.1w/doc/man3/SSL_CTX_add_extra_chain_cert.pod
openssl-1.1.1w/doc/man3/SSL_CTX_add_session.pod
openssl-1.1.1w/doc/man3/SSL_CTX_config.pod
openssl-1.1.1w/doc/man3/SSL_CTX_ctrl.pod
openssl-1.1.1w/doc/man3/SSL_CTX_dane_enable.pod
openssl-1.1.1w/doc/man3/SSL_CTX_flush_sessions.pod
openssl-1.1.1w/doc/man3/SSL_CTX_free.pod
openssl-1.1.1w/doc/man3/SSL_CTX_get0_param.pod
openssl-1.1.1w/doc/man3/SSL_CTX_get_verify_mode.pod
openssl-1.1.1w/doc/man3/SSL_CTX_has_client_custom_ext.pod
openssl-1.1.1w/doc/man3/SSL_CTX_load_verify_locations.pod
openssl-1.1.1w/doc/man3/SSL_CTX_new.pod
openssl-1.1.1w/doc/man3/SSL_CTX_sess_number.pod
openssl-1.1.1w/doc/man3/SSL_CTX_sess_set_cache_size.pod
openssl-1.1.1w/doc/man3/SSL_CTX_sess_set_get_cb.pod
openssl-1.1.1w/doc/man3/SSL_CTX_sessions.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set0_CA_list.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set1_curves.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set1_sigalgs.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set1_verify_cert_store.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_alpn_select_cb.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_cert_cb.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_cert_store.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_cert_verify_callback.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_cipher_list.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_client_cert_cb.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_client_hello_cb.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_ct_validation_callback.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_ctlog_list_file.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_default_passwd_cb.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_ex_data.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_generate_session_id.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_info_callback.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_keylog_callback.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_max_cert_list.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_min_proto_version.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_mode.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_msg_callback.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_num_tickets.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_options.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_psk_client_callback.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_quiet_shutdown.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_read_ahead.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_record_padding_callback.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_security_level.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_session_cache_mode.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_session_id_context.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_session_ticket_cb.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_split_send_fragment.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_ssl_version.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_stateless_cookie_generate_cb.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_timeout.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_tlsext_servername_callback.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_tlsext_status_cb.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_tlsext_ticket_key_cb.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_tlsext_use_srtp.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_tmp_dh_callback.pod
openssl-1.1.1w/doc/man3/SSL_CTX_set_verify.pod
openssl-1.1.1w/doc/man3/SSL_CTX_use_certificate.pod
openssl-1.1.1w/doc/man3/SSL_CTX_use_psk_identity_hint.pod
openssl-1.1.1w/doc/man3/SSL_CTX_use_serverinfo.pod
openssl-1.1.1w/doc/man3/SSL_SESSION_free.pod
openssl-1.1.1w/doc/man3/SSL_SESSION_get0_cipher.pod
openssl-1.1.1w/doc/man3/SSL_SESSION_get0_hostname.pod
openssl-1.1.1w/doc/man3/SSL_SESSION_get0_id_context.pod
openssl-1.1.1w/doc/man3/SSL_SESSION_get0_peer.pod
openssl-1.1.1w/doc/man3/SSL_SESSION_get_compress_id.pod
openssl-1.1.1w/doc/man3/SSL_SESSION_get_ex_data.pod
openssl-1.1.1w/doc/man3/SSL_SESSION_get_protocol_version.pod
openssl-1.1.1w/doc/man3/SSL_SESSION_get_time.pod
openssl-1.1.1w/doc/man3/SSL_SESSION_has_ticket.pod
openssl-1.1.1w/doc/man3/SSL_SESSION_is_resumable.pod
openssl-1.1.1w/doc/man3/SSL_SESSION_print.pod
openssl-1.1.1w/doc/man3/SSL_SESSION_set1_id.pod
openssl-1.1.1w/doc/man3/SSL_accept.pod
openssl-1.1.1w/doc/man3/SSL_alert_type_string.pod
openssl-1.1.1w/doc/man3/SSL_alloc_buffers.pod
openssl-1.1.1w/doc/man3/SSL_check_chain.pod
openssl-1.1.1w/doc/man3/SSL_clear.pod
openssl-1.1.1w/doc/man3/SSL_connect.pod
openssl-1.1.1w/doc/man3/SSL_do_handshake.pod
openssl-1.1.1w/doc/man3/SSL_export_keying_material.pod
openssl-1.1.1w/doc/man3/SSL_extension_supported.pod
openssl-1.1.1w/doc/man3/SSL_free.pod
openssl-1.1.1w/doc/man3/SSL_get0_peer_scts.pod
openssl-1.1.1w/doc/man3/SSL_get_SSL_CTX.pod
openssl-1.1.1w/doc/man3/SSL_get_all_async_fds.pod
openssl-1.1.1w/doc/man3/SSL_get_ciphers.pod
openssl-1.1.1w/doc/man3/SSL_get_client_random.pod
openssl-1.1.1w/doc/man3/SSL_get_current_cipher.pod
openssl-1.1.1w/doc/man3/SSL_get_default_timeout.pod
openssl-1.1.1w/doc/man3/SSL_get_error.pod
openssl-1.1.1w/doc/man3/SSL_get_extms_support.pod
openssl-1.1.1w/doc/man3/SSL_get_fd.pod
openssl-1.1.1w/doc/man3/SSL_get_peer_cert_chain.pod
openssl-1.1.1w/doc/man3/SSL_get_peer_certificate.pod
openssl-1.1.1w/doc/man3/SSL_get_peer_signature_nid.pod
openssl-1.1.1w/doc/man3/SSL_get_peer_tmp_key.pod
openssl-1.1.1w/doc/man3/SSL_get_psk_identity.pod
openssl-1.1.1w/doc/man3/SSL_get_rbio.pod
openssl-1.1.1w/doc/man3/SSL_get_session.pod
openssl-1.1.1w/doc/man3/SSL_get_shared_sigalgs.pod
openssl-1.1.1w/doc/man3/SSL_get_verify_result.pod
openssl-1.1.1w/doc/man3/SSL_get_version.pod
openssl-1.1.1w/doc/man3/SSL_in_init.pod
openssl-1.1.1w/doc/man3/SSL_key_update.pod
openssl-1.1.1w/doc/man3/SSL_library_init.pod
openssl-1.1.1w/doc/man3/SSL_load_client_CA_file.pod
openssl-1.1.1w/doc/man3/SSL_new.pod
openssl-1.1.1w/doc/man3/SSL_pending.pod
openssl-1.1.1w/doc/man3/SSL_read.pod
openssl-1.1.1w/doc/man3/SSL_read_early_data.pod
openssl-1.1.1w/doc/man3/SSL_rstate_string.pod
openssl-1.1.1w/doc/man3/SSL_session_reused.pod
openssl-1.1.1w/doc/man3/SSL_set1_host.pod
openssl-1.1.1w/doc/man3/SSL_set_bio.pod
openssl-1.1.1w/doc/man3/SSL_set_connect_state.pod
openssl-1.1.1w/doc/man3/SSL_set_fd.pod
openssl-1.1.1w/doc/man3/SSL_set_session.pod
openssl-1.1.1w/doc/man3/SSL_set_shutdown.pod
openssl-1.1.1w/doc/man3/SSL_set_verify_result.pod
openssl-1.1.1w/doc/man3/SSL_shutdown.pod
openssl-1.1.1w/doc/man3/SSL_state_string.pod
openssl-1.1.1w/doc/man3/SSL_want.pod
openssl-1.1.1w/doc/man3/SSL_write.pod
openssl-1.1.1w/doc/man3/UI_STRING.pod
openssl-1.1.1w/doc/man3/UI_UTIL_read_pw.pod
openssl-1.1.1w/doc/man3/UI_create_method.pod
openssl-1.1.1w/doc/man3/UI_new.pod
openssl-1.1.1w/doc/man3/X509V3_get_d2i.pod
openssl-1.1.1w/doc/man3/X509_ALGOR_dup.pod
openssl-1.1.1w/doc/man3/X509_CRL_get0_by_serial.pod
openssl-1.1.1w/doc/man3/X509_EXTENSION_set_object.pod
openssl-1.1.1w/doc/man3/X509_LOOKUP.pod
openssl-1.1.1w/doc/man3/X509_LOOKUP_hash_dir.pod
openssl-1.1.1w/doc/man3/X509_LOOKUP_meth_new.pod
openssl-1.1.1w/doc/man3/X509_NAME_ENTRY_get_object.pod
openssl-1.1.1w/doc/man3/X509_NAME_add_entry_by_txt.pod
openssl-1.1.1w/doc/man3/X509_NAME_get0_der.pod
openssl-1.1.1w/doc/man3/X509_NAME_get_index_by_NID.pod
openssl-1.1.1w/doc/man3/X509_NAME_print_ex.pod
openssl-1.1.1w/doc/man3/X509_PUBKEY_new.pod
openssl-1.1.1w/doc/man3/X509_SIG_get0.pod
openssl-1.1.1w/doc/man3/X509_STORE_CTX_get_error.pod
openssl-1.1.1w/doc/man3/X509_STORE_CTX_new.pod
openssl-1.1.1w/doc/man3/X509_STORE_CTX_set_verify_cb.pod
openssl-1.1.1w/doc/man3/X509_STORE_add_cert.pod
openssl-1.1.1w/doc/man3/X509_STORE_get0_param.pod
openssl-1.1.1w/doc/man3/X509_STORE_new.pod
openssl-1.1.1w/doc/man3/X509_STORE_set_verify_cb_func.pod
openssl-1.1.1w/doc/man3/X509_VERIFY_PARAM_set_flags.pod
openssl-1.1.1w/doc/man3/X509_check_ca.pod
openssl-1.1.1w/doc/man3/X509_check_host.pod
openssl-1.1.1w/doc/man3/X509_check_issued.pod
openssl-1.1.1w/doc/man3/X509_check_private_key.pod
openssl-1.1.1w/doc/man3/X509_check_purpose.pod
openssl-1.1.1w/doc/man3/X509_cmp.pod
openssl-1.1.1w/doc/man3/X509_cmp_time.pod
openssl-1.1.1w/doc/man3/X509_digest.pod
openssl-1.1.1w/doc/man3/X509_dup.pod
openssl-1.1.1w/doc/man3/X509_get0_notBefore.pod
openssl-1.1.1w/doc/man3/X509_get0_signature.pod
openssl-1.1.1w/doc/man3/X509_get0_uids.pod
openssl-1.1.1w/doc/man3/X509_get_extension_flags.pod
openssl-1.1.1w/doc/man3/X509_get_pubkey.pod
openssl-1.1.1w/doc/man3/X509_get_serialNumber.pod
openssl-1.1.1w/doc/man3/X509_get_subject_name.pod
openssl-1.1.1w/doc/man3/X509_get_version.pod
openssl-1.1.1w/doc/man3/X509_new.pod
openssl-1.1.1w/doc/man3/X509_sign.pod
openssl-1.1.1w/doc/man3/X509_verify_cert.pod
openssl-1.1.1w/doc/man3/X509v3_get_ext_by_NID.pod
openssl-1.1.1w/doc/man3/d2i_DHparams.pod
openssl-1.1.1w/doc/man3/d2i_PKCS8PrivateKey_bio.pod
openssl-1.1.1w/doc/man3/d2i_PrivateKey.pod
openssl-1.1.1w/doc/man3/d2i_SSL_SESSION.pod
openssl-1.1.1w/doc/man3/d2i_X509.pod
openssl-1.1.1w/doc/man3/i2d_CMS_bio_stream.pod
openssl-1.1.1w/doc/man3/i2d_PKCS7_bio_stream.pod
openssl-1.1.1w/doc/man3/i2d_re_X509_tbs.pod
openssl-1.1.1w/doc/man3/o2i_SCT_LIST.pod
openssl-1.1.1w/doc/man5/
openssl-1.1.1w/doc/man5/config.pod
openssl-1.1.1w/doc/man5/x509v3_config.pod
openssl-1.1.1w/doc/man7/
openssl-1.1.1w/doc/man7/Ed25519.pod
openssl-1.1.1w/doc/man7/RAND.pod
openssl-1.1.1w/doc/man7/RAND_DRBG.pod
openssl-1.1.1w/doc/man7/RSA-PSS.pod
openssl-1.1.1w/doc/man7/SM2.pod
openssl-1.1.1w/doc/man7/X25519.pod
openssl-1.1.1w/doc/man7/bio.pod
openssl-1.1.1w/doc/man7/crypto.pod
openssl-1.1.1w/doc/man7/ct.pod
openssl-1.1.1w/doc/man7/des_modes.pod
openssl-1.1.1w/doc/man7/evp.pod
openssl-1.1.1w/doc/man7/ossl_store-file.pod
openssl-1.1.1w/doc/man7/ossl_store.pod
openssl-1.1.1w/doc/man7/passphrase-encoding.pod
openssl-1.1.1w/doc/man7/proxy-certificates.pod
openssl-1.1.1w/doc/man7/scrypt.pod
openssl-1.1.1w/doc/man7/ssl.pod
openssl-1.1.1w/doc/man7/x509.pod
openssl-1.1.1w/doc/openssl-c-indent.el
openssl-1.1.1w/e_os.h
openssl-1.1.1w/engines/
openssl-1.1.1w/engines/asm/
openssl-1.1.1w/engines/asm/e_padlock-x86.pl
openssl-1.1.1w/engines/asm/e_padlock-x86_64.pl
openssl-1.1.1w/engines/build.info
openssl-1.1.1w/engines/e_afalg.c
openssl-1.1.1w/engines/e_afalg.ec
openssl-1.1.1w/engines/e_afalg.h
openssl-1.1.1w/engines/e_afalg.txt
openssl-1.1.1w/engines/e_afalg_err.c
openssl-1.1.1w/engines/e_afalg_err.h
openssl-1.1.1w/engines/e_capi.c
openssl-1.1.1w/engines/e_capi.ec
openssl-1.1.1w/engines/e_capi.txt
openssl-1.1.1w/engines/e_capi_err.c
openssl-1.1.1w/engines/e_capi_err.h
openssl-1.1.1w/engines/e_dasync.c
openssl-1.1.1w/engines/e_dasync.ec
openssl-1.1.1w/engines/e_dasync.txt
openssl-1.1.1w/engines/e_dasync_err.c
openssl-1.1.1w/engines/e_dasync_err.h
openssl-1.1.1w/engines/e_ossltest.c
openssl-1.1.1w/engines/e_ossltest.ec
openssl-1.1.1w/engines/e_ossltest.txt
openssl-1.1.1w/engines/e_ossltest_err.c
openssl-1.1.1w/engines/e_ossltest_err.h
openssl-1.1.1w/engines/e_padlock.c
openssl-1.1.1w/external/
openssl-1.1.1w/external/perl/
openssl-1.1.1w/external/perl/Downloaded.txt
openssl-1.1.1w/external/perl/Text-Template-1.46/
openssl-1.1.1w/external/perl/Text-Template-1.46/Artistic
openssl-1.1.1w/external/perl/Text-Template-1.46/COPYING
openssl-1.1.1w/external/perl/Text-Template-1.46/INSTALL
openssl-1.1.1w/external/perl/Text-Template-1.46/MANIFEST
openssl-1.1.1w/external/perl/Text-Template-1.46/META.json
openssl-1.1.1w/external/perl/Text-Template-1.46/META.yml
openssl-1.1.1w/external/perl/Text-Template-1.46/Makefile.PL
openssl-1.1.1w/external/perl/Text-Template-1.46/README
openssl-1.1.1w/external/perl/Text-Template-1.46/lib/
openssl-1.1.1w/external/perl/Text-Template-1.46/lib/Text/
openssl-1.1.1w/external/perl/Text-Template-1.46/lib/Text/Template.pm
openssl-1.1.1w/external/perl/Text-Template-1.46/lib/Text/Template/
openssl-1.1.1w/external/perl/Text-Template-1.46/lib/Text/Template/Preprocess.pm
openssl-1.1.1w/external/perl/Text-Template-1.46/t/
openssl-1.1.1w/external/perl/Text-Template-1.46/t/00-version.t
openssl-1.1.1w/external/perl/Text-Template-1.46/t/01-basic.t
openssl-1.1.1w/external/perl/Text-Template-1.46/t/02-hash.t
openssl-1.1.1w/external/perl/Text-Template-1.46/t/03-out.t
openssl-1.1.1w/external/perl/Text-Template-1.46/t/04-safe.t
openssl-1.1.1w/external/perl/Text-Template-1.46/t/05-safe2.t
openssl-1.1.1w/external/perl/Text-Template-1.46/t/06-ofh.t
openssl-1.1.1w/external/perl/Text-Template-1.46/t/07-safe3.t
openssl-1.1.1w/external/perl/Text-Template-1.46/t/08-exported.t
openssl-1.1.1w/external/perl/Text-Template-1.46/t/09-error.t
openssl-1.1.1w/external/perl/Text-Template-1.46/t/10-delimiters.t
openssl-1.1.1w/external/perl/Text-Template-1.46/t/11-prepend.t
openssl-1.1.1w/external/perl/Text-Template-1.46/t/12-preprocess.t
openssl-1.1.1w/external/perl/Text-Template-1.46/t/13-taint.t
openssl-1.1.1w/external/perl/Text-Template-1.46/t/14-broken.t
openssl-1.1.1w/external/perl/transfer/
openssl-1.1.1w/external/perl/transfer/Text/
openssl-1.1.1w/external/perl/transfer/Text/Template.pm
openssl-1.1.1w/fuzz/
openssl-1.1.1w/fuzz/README.md
openssl-1.1.1w/fuzz/asn1.c
openssl-1.1.1w/fuzz/asn1parse.c
openssl-1.1.1w/fuzz/bignum.c
openssl-1.1.1w/fuzz/bndiv.c
openssl-1.1.1w/fuzz/build.info
openssl-1.1.1w/fuzz/client.c
openssl-1.1.1w/fuzz/cms.c
openssl-1.1.1w/fuzz/conf.c
openssl-1.1.1w/fuzz/crl.c
openssl-1.1.1w/fuzz/ct.c
openssl-1.1.1w/fuzz/driver.c
openssl-1.1.1w/fuzz/fuzzer.h
openssl-1.1.1w/fuzz/helper.py
openssl-1.1.1w/fuzz/mkfuzzoids.pl
openssl-1.1.1w/fuzz/oids.txt
openssl-1.1.1w/fuzz/rand.inc
openssl-1.1.1w/fuzz/server.c
openssl-1.1.1w/fuzz/test-corpus.c
openssl-1.1.1w/fuzz/x509.c
openssl-1.1.1w/include/
openssl-1.1.1w/include/crypto/
openssl-1.1.1w/include/crypto/__DECC_INCLUDE_EPILOGUE.H
openssl-1.1.1w/include/crypto/__DECC_INCLUDE_PROLOGUE.H
openssl-1.1.1w/include/crypto/aria.h
openssl-1.1.1w/include/crypto/asn1.h
openssl-1.1.1w/include/crypto/async.h
openssl-1.1.1w/include/crypto/bn.h
openssl-1.1.1w/include/crypto/bn_conf.h.in
openssl-1.1.1w/include/crypto/bn_dh.h
openssl-1.1.1w/include/crypto/bn_srp.h
openssl-1.1.1w/include/crypto/chacha.h
openssl-1.1.1w/include/crypto/cryptlib.h
openssl-1.1.1w/include/crypto/ctype.h
openssl-1.1.1w/include/crypto/dso_conf.h.in
openssl-1.1.1w/include/crypto/ec.h
openssl-1.1.1w/include/crypto/engine.h
openssl-1.1.1w/include/crypto/err.h
openssl-1.1.1w/include/crypto/evp.h
openssl-1.1.1w/include/crypto/lhash.h
openssl-1.1.1w/include/crypto/md32_common.h
openssl-1.1.1w/include/crypto/objects.h
openssl-1.1.1w/include/crypto/poly1305.h
openssl-1.1.1w/include/crypto/rand.h
openssl-1.1.1w/include/crypto/sha.h
openssl-1.1.1w/include/crypto/siphash.h
openssl-1.1.1w/include/crypto/sm2.h
openssl-1.1.1w/include/crypto/sm2err.h
openssl-1.1.1w/include/crypto/sm3.h
openssl-1.1.1w/include/crypto/sm4.h
openssl-1.1.1w/include/crypto/store.h
openssl-1.1.1w/include/crypto/x509.h
openssl-1.1.1w/include/internal/
openssl-1.1.1w/include/internal/__DECC_INCLUDE_EPILOGUE.H
openssl-1.1.1w/include/internal/__DECC_INCLUDE_PROLOGUE.H
openssl-1.1.1w/include/internal/bio.h
openssl-1.1.1w/include/internal/comp.h
openssl-1.1.1w/include/internal/conf.h
openssl-1.1.1w/include/internal/constant_time.h
openssl-1.1.1w/include/internal/cryptlib.h
openssl-1.1.1w/include/internal/dane.h
openssl-1.1.1w/include/internal/dso.h
openssl-1.1.1w/include/internal/dsoerr.h
openssl-1.1.1w/include/internal/err.h
openssl-1.1.1w/include/internal/nelem.h
openssl-1.1.1w/include/internal/numbers.h
openssl-1.1.1w/include/internal/o_dir.h
openssl-1.1.1w/include/internal/o_str.h
openssl-1.1.1w/include/internal/refcount.h
openssl-1.1.1w/include/internal/sockets.h
openssl-1.1.1w/include/internal/sslconf.h
openssl-1.1.1w/include/internal/thread_once.h
openssl-1.1.1w/include/internal/tsan_assist.h
openssl-1.1.1w/include/openssl/
openssl-1.1.1w/include/openssl/__DECC_INCLUDE_EPILOGUE.H
openssl-1.1.1w/include/openssl/__DECC_INCLUDE_PROLOGUE.H
openssl-1.1.1w/include/openssl/aes.h
openssl-1.1.1w/include/openssl/asn1.h
openssl-1.1.1w/include/openssl/asn1_mac.h
openssl-1.1.1w/include/openssl/asn1err.h
openssl-1.1.1w/include/openssl/asn1t.h
openssl-1.1.1w/include/openssl/async.h
openssl-1.1.1w/include/openssl/asyncerr.h
openssl-1.1.1w/include/openssl/bio.h
openssl-1.1.1w/include/openssl/bioerr.h
openssl-1.1.1w/include/openssl/blowfish.h
openssl-1.1.1w/include/openssl/bn.h
openssl-1.1.1w/include/openssl/bnerr.h
openssl-1.1.1w/include/openssl/buffer.h
openssl-1.1.1w/include/openssl/buffererr.h
openssl-1.1.1w/include/openssl/camellia.h
openssl-1.1.1w/include/openssl/cast.h
openssl-1.1.1w/include/openssl/cmac.h
openssl-1.1.1w/include/openssl/cms.h
openssl-1.1.1w/include/openssl/cmserr.h
openssl-1.1.1w/include/openssl/comp.h
openssl-1.1.1w/include/openssl/comperr.h
openssl-1.1.1w/include/openssl/conf.h
openssl-1.1.1w/include/openssl/conf_api.h
openssl-1.1.1w/include/openssl/conferr.h
openssl-1.1.1w/include/openssl/crypto.h
openssl-1.1.1w/include/openssl/cryptoerr.h
openssl-1.1.1w/include/openssl/ct.h
openssl-1.1.1w/include/openssl/cterr.h
openssl-1.1.1w/include/openssl/des.h
openssl-1.1.1w/include/openssl/dh.h
openssl-1.1.1w/include/openssl/dherr.h
openssl-1.1.1w/include/openssl/dsa.h
openssl-1.1.1w/include/openssl/dsaerr.h
openssl-1.1.1w/include/openssl/dtls1.h
openssl-1.1.1w/include/openssl/e_os2.h
openssl-1.1.1w/include/openssl/ebcdic.h
openssl-1.1.1w/include/openssl/ec.h
openssl-1.1.1w/include/openssl/ecdh.h
openssl-1.1.1w/include/openssl/ecdsa.h
openssl-1.1.1w/include/openssl/ecerr.h
openssl-1.1.1w/include/openssl/engine.h
openssl-1.1.1w/include/openssl/engineerr.h
openssl-1.1.1w/include/openssl/err.h
openssl-1.1.1w/include/openssl/evp.h
openssl-1.1.1w/include/openssl/evperr.h
openssl-1.1.1w/include/openssl/hmac.h
openssl-1.1.1w/include/openssl/idea.h
openssl-1.1.1w/include/openssl/kdf.h
openssl-1.1.1w/include/openssl/kdferr.h
openssl-1.1.1w/include/openssl/lhash.h
openssl-1.1.1w/include/openssl/md2.h
openssl-1.1.1w/include/openssl/md4.h
openssl-1.1.1w/include/openssl/md5.h
openssl-1.1.1w/include/openssl/mdc2.h
openssl-1.1.1w/include/openssl/modes.h
openssl-1.1.1w/include/openssl/obj_mac.h
openssl-1.1.1w/include/openssl/objects.h
openssl-1.1.1w/include/openssl/objectserr.h
openssl-1.1.1w/include/openssl/ocsp.h
openssl-1.1.1w/include/openssl/ocsperr.h
openssl-1.1.1w/include/openssl/opensslconf.h.in
openssl-1.1.1w/include/openssl/opensslv.h
openssl-1.1.1w/include/openssl/ossl_typ.h
openssl-1.1.1w/include/openssl/pem.h
openssl-1.1.1w/include/openssl/pem2.h
openssl-1.1.1w/include/openssl/pemerr.h
openssl-1.1.1w/include/openssl/pkcs12.h
openssl-1.1.1w/include/openssl/pkcs12err.h
openssl-1.1.1w/include/openssl/pkcs7.h
openssl-1.1.1w/include/openssl/pkcs7err.h
openssl-1.1.1w/include/openssl/rand.h
openssl-1.1.1w/include/openssl/rand_drbg.h
openssl-1.1.1w/include/openssl/randerr.h
openssl-1.1.1w/include/openssl/rc2.h
openssl-1.1.1w/include/openssl/rc4.h
openssl-1.1.1w/include/openssl/rc5.h
openssl-1.1.1w/include/openssl/ripemd.h
openssl-1.1.1w/include/openssl/rsa.h
openssl-1.1.1w/include/openssl/rsaerr.h
openssl-1.1.1w/include/openssl/safestack.h
openssl-1.1.1w/include/openssl/seed.h
openssl-1.1.1w/include/openssl/sha.h
openssl-1.1.1w/include/openssl/srp.h
openssl-1.1.1w/include/openssl/srtp.h
openssl-1.1.1w/include/openssl/ssl.h
openssl-1.1.1w/include/openssl/ssl2.h
openssl-1.1.1w/include/openssl/ssl3.h
openssl-1.1.1w/include/openssl/sslerr.h
openssl-1.1.1w/include/openssl/stack.h
openssl-1.1.1w/include/openssl/store.h
openssl-1.1.1w/include/openssl/storeerr.h
openssl-1.1.1w/include/openssl/symhacks.h
openssl-1.1.1w/include/openssl/tls1.h
openssl-1.1.1w/include/openssl/ts.h
openssl-1.1.1w/include/openssl/tserr.h
openssl-1.1.1w/include/openssl/txt_db.h
openssl-1.1.1w/include/openssl/ui.h
openssl-1.1.1w/include/openssl/uierr.h
openssl-1.1.1w/include/openssl/whrlpool.h
openssl-1.1.1w/include/openssl/x509.h
openssl-1.1.1w/include/openssl/x509_vfy.h
openssl-1.1.1w/include/openssl/x509err.h
openssl-1.1.1w/include/openssl/x509v3.h
openssl-1.1.1w/include/openssl/x509v3err.h
openssl-1.1.1w/ms/
openssl-1.1.1w/ms/applink.c
openssl-1.1.1w/ms/cmp.pl
openssl-1.1.1w/ms/uplink-common.pl
openssl-1.1.1w/ms/uplink-ia64.pl
openssl-1.1.1w/ms/uplink-x86.pl
openssl-1.1.1w/ms/uplink-x86_64.pl
openssl-1.1.1w/ms/uplink.c
openssl-1.1.1w/ms/uplink.h
openssl-1.1.1w/os-dep/
openssl-1.1.1w/os-dep/haiku.h
openssl-1.1.1w/ssl/
openssl-1.1.1w/ssl/bio_ssl.c
openssl-1.1.1w/ssl/build.info
openssl-1.1.1w/ssl/d1_lib.c
openssl-1.1.1w/ssl/d1_msg.c
openssl-1.1.1w/ssl/d1_srtp.c
openssl-1.1.1w/ssl/methods.c
openssl-1.1.1w/ssl/packet.c
openssl-1.1.1w/ssl/packet_local.h
openssl-1.1.1w/ssl/pqueue.c
openssl-1.1.1w/ssl/record/
openssl-1.1.1w/ssl/record/README
openssl-1.1.1w/ssl/record/dtls1_bitmap.c
openssl-1.1.1w/ssl/record/rec_layer_d1.c
openssl-1.1.1w/ssl/record/rec_layer_s3.c
openssl-1.1.1w/ssl/record/record.h
openssl-1.1.1w/ssl/record/record_local.h
openssl-1.1.1w/ssl/record/ssl3_buffer.c
openssl-1.1.1w/ssl/record/ssl3_record.c
openssl-1.1.1w/ssl/record/ssl3_record_tls13.c
openssl-1.1.1w/ssl/s3_cbc.c
openssl-1.1.1w/ssl/s3_enc.c
openssl-1.1.1w/ssl/s3_lib.c
openssl-1.1.1w/ssl/s3_msg.c
openssl-1.1.1w/ssl/ssl_asn1.c
openssl-1.1.1w/ssl/ssl_cert.c
openssl-1.1.1w/ssl/ssl_cert_table.h
openssl-1.1.1w/ssl/ssl_ciph.c
openssl-1.1.1w/ssl/ssl_conf.c
openssl-1.1.1w/ssl/ssl_err.c
openssl-1.1.1w/ssl/ssl_init.c
openssl-1.1.1w/ssl/ssl_lib.c
openssl-1.1.1w/ssl/ssl_local.h
openssl-1.1.1w/ssl/ssl_mcnf.c
openssl-1.1.1w/ssl/ssl_rsa.c
openssl-1.1.1w/ssl/ssl_sess.c
openssl-1.1.1w/ssl/ssl_stat.c
openssl-1.1.1w/ssl/ssl_txt.c
openssl-1.1.1w/ssl/ssl_utst.c
openssl-1.1.1w/ssl/statem/
openssl-1.1.1w/ssl/statem/README
openssl-1.1.1w/ssl/statem/extensions.c
openssl-1.1.1w/ssl/statem/extensions_clnt.c
openssl-1.1.1w/ssl/statem/extensions_cust.c
openssl-1.1.1w/ssl/statem/extensions_srvr.c
openssl-1.1.1w/ssl/statem/statem.c
openssl-1.1.1w/ssl/statem/statem.h
openssl-1.1.1w/ssl/statem/statem_clnt.c
openssl-1.1.1w/ssl/statem/statem_dtls.c
openssl-1.1.1w/ssl/statem/statem_lib.c
openssl-1.1.1w/ssl/statem/statem_local.h
openssl-1.1.1w/ssl/statem/statem_srvr.c
openssl-1.1.1w/ssl/t1_enc.c
openssl-1.1.1w/ssl/t1_lib.c
openssl-1.1.1w/ssl/t1_trce.c
openssl-1.1.1w/ssl/tls13_enc.c
openssl-1.1.1w/ssl/tls_srp.c
openssl-1.1.1w/test/
openssl-1.1.1w/test/CAss.cnf
openssl-1.1.1w/test/CAssdh.cnf
openssl-1.1.1w/test/CAssdsa.cnf
openssl-1.1.1w/test/CAssrsa.cnf
openssl-1.1.1w/test/CAtsa.cnf
openssl-1.1.1w/test/P1ss.cnf
openssl-1.1.1w/test/P2ss.cnf
openssl-1.1.1w/test/README
openssl-1.1.1w/test/README.external
openssl-1.1.1w/test/README.ssltest.md
openssl-1.1.1w/test/Sssdsa.cnf
openssl-1.1.1w/test/Sssrsa.cnf
openssl-1.1.1w/test/Uss.cnf
openssl-1.1.1w/test/aborttest.c
openssl-1.1.1w/test/afalgtest.c
openssl-1.1.1w/test/asn1_decode_test.c
openssl-1.1.1w/test/asn1_encode_test.c
openssl-1.1.1w/test/asn1_internal_test.c
openssl-1.1.1w/test/asn1_string_table_test.c
openssl-1.1.1w/test/asn1_time_test.c
openssl-1.1.1w/test/asynciotest.c
openssl-1.1.1w/test/asynctest.c
openssl-1.1.1w/test/bad_dtls_test.c
openssl-1.1.1w/test/bftest.c
openssl-1.1.1w/test/bio_callback_test.c
openssl-1.1.1w/test/bio_enc_test.c
openssl-1.1.1w/test/bio_memleak_test.c
openssl-1.1.1w/test/bioprinttest.c
openssl-1.1.1w/test/bntest.c
openssl-1.1.1w/test/bntests.pl
openssl-1.1.1w/test/build.info
openssl-1.1.1w/test/casttest.c
openssl-1.1.1w/test/certs/
openssl-1.1.1w/test/certs/alt1-cert.pem
openssl-1.1.1w/test/certs/alt1-key.pem
openssl-1.1.1w/test/certs/alt2-cert.pem
openssl-1.1.1w/test/certs/alt2-key.pem
openssl-1.1.1w/test/certs/alt3-cert.pem
openssl-1.1.1w/test/certs/alt3-key.pem
openssl-1.1.1w/test/certs/bad-pc3-cert.pem
openssl-1.1.1w/test/certs/bad-pc3-key.pem
openssl-1.1.1w/test/certs/bad-pc4-cert.pem
openssl-1.1.1w/test/certs/bad-pc4-key.pem
openssl-1.1.1w/test/certs/bad-pc6-cert.pem
openssl-1.1.1w/test/certs/bad-pc6-key.pem
openssl-1.1.1w/test/certs/bad.key
openssl-1.1.1w/test/certs/bad.pem
openssl-1.1.1w/test/certs/badalt1-cert.pem
openssl-1.1.1w/test/certs/badalt1-key.pem
openssl-1.1.1w/test/certs/badalt10-cert.pem
openssl-1.1.1w/test/certs/badalt10-key.pem
openssl-1.1.1w/test/certs/badalt2-cert.pem
openssl-1.1.1w/test/certs/badalt2-key.pem
openssl-1.1.1w/test/certs/badalt3-cert.pem
openssl-1.1.1w/test/certs/badalt3-key.pem
openssl-1.1.1w/test/certs/badalt4-cert.pem
openssl-1.1.1w/test/certs/badalt4-key.pem
openssl-1.1.1w/test/certs/badalt5-cert.pem
openssl-1.1.1w/test/certs/badalt5-key.pem
openssl-1.1.1w/test/certs/badalt6-cert.pem
openssl-1.1.1w/test/certs/badalt6-key.pem
openssl-1.1.1w/test/certs/badalt7-cert.pem
openssl-1.1.1w/test/certs/badalt7-key.pem
openssl-1.1.1w/test/certs/badalt8-cert.pem
openssl-1.1.1w/test/certs/badalt8-key.pem
openssl-1.1.1w/test/certs/badalt9-cert.pem
openssl-1.1.1w/test/certs/badalt9-key.pem
openssl-1.1.1w/test/certs/badcn1-cert.pem
openssl-1.1.1w/test/certs/badcn1-key.pem
openssl-1.1.1w/test/certs/ca+anyEKU.pem
openssl-1.1.1w/test/certs/ca+clientAuth.pem
openssl-1.1.1w/test/certs/ca+serverAuth.pem
openssl-1.1.1w/test/certs/ca-anyEKU.pem
openssl-1.1.1w/test/certs/ca-cert-768.pem
openssl-1.1.1w/test/certs/ca-cert-768i.pem
openssl-1.1.1w/test/certs/ca-cert-ec-explicit.pem
openssl-1.1.1w/test/certs/ca-cert-ec-named.pem
openssl-1.1.1w/test/certs/ca-cert-md5-any.pem
openssl-1.1.1w/test/certs/ca-cert-md5.pem
openssl-1.1.1w/test/certs/ca-cert.pem
openssl-1.1.1w/test/certs/ca-cert2.pem
openssl-1.1.1w/test/certs/ca-clientAuth.pem
openssl-1.1.1w/test/certs/ca-expired.pem
openssl-1.1.1w/test/certs/ca-key-768.pem
openssl-1.1.1w/test/certs/ca-key-ec-explicit.pem
openssl-1.1.1w/test/certs/ca-key-ec-named.pem
openssl-1.1.1w/test/certs/ca-key.pem
openssl-1.1.1w/test/certs/ca-key2.pem
openssl-1.1.1w/test/certs/ca-name2.pem
openssl-1.1.1w/test/certs/ca-nonbc.pem
openssl-1.1.1w/test/certs/ca-nonca.pem
openssl-1.1.1w/test/certs/ca-pol-cert.pem
openssl-1.1.1w/test/certs/ca-pss-cert.pem
openssl-1.1.1w/test/certs/ca-pss-key.pem
openssl-1.1.1w/test/certs/ca-root2.pem
openssl-1.1.1w/test/certs/ca-serverAuth.pem
openssl-1.1.1w/test/certs/cca+anyEKU.pem
openssl-1.1.1w/test/certs/cca+clientAuth.pem
openssl-1.1.1w/test/certs/cca+serverAuth.pem
openssl-1.1.1w/test/certs/cca-anyEKU.pem
openssl-1.1.1w/test/certs/cca-cert.pem
openssl-1.1.1w/test/certs/cca-clientAuth.pem
openssl-1.1.1w/test/certs/cca-serverAuth.pem
openssl-1.1.1w/test/certs/client-ed25519-cert.pem
openssl-1.1.1w/test/certs/client-ed25519-key.pem
openssl-1.1.1w/test/certs/client-ed448-cert.pem
openssl-1.1.1w/test/certs/client-ed448-key.pem
openssl-1.1.1w/test/certs/croot+anyEKU.pem
openssl-1.1.1w/test/certs/croot+clientAuth.pem
openssl-1.1.1w/test/certs/croot+serverAuth.pem
openssl-1.1.1w/test/certs/croot-anyEKU.pem
openssl-1.1.1w/test/certs/croot-cert.pem
openssl-1.1.1w/test/certs/croot-clientAuth.pem
openssl-1.1.1w/test/certs/croot-serverAuth.pem
openssl-1.1.1w/test/certs/cross-key.pem
openssl-1.1.1w/test/certs/cross-root.pem
openssl-1.1.1w/test/certs/cyrillic.msb
openssl-1.1.1w/test/certs/cyrillic.pem
openssl-1.1.1w/test/certs/cyrillic.utf8
openssl-1.1.1w/test/certs/cyrillic_crl.pem
openssl-1.1.1w/test/certs/cyrillic_crl.utf8
openssl-1.1.1w/test/certs/dhp2048.pem
openssl-1.1.1w/test/certs/ee+clientAuth.pem
openssl-1.1.1w/test/certs/ee+serverAuth.pem
openssl-1.1.1w/test/certs/ee-cert-768.pem
openssl-1.1.1w/test/certs/ee-cert-768i.pem
openssl-1.1.1w/test/certs/ee-cert-ec-explicit.pem
openssl-1.1.1w/test/certs/ee-cert-ec-named-explicit.pem
openssl-1.1.1w/test/certs/ee-cert-ec-named-named.pem
openssl-1.1.1w/test/certs/ee-cert-md5.pem
openssl-1.1.1w/test/certs/ee-cert-policies-bad.pem
openssl-1.1.1w/test/certs/ee-cert-policies.pem
openssl-1.1.1w/test/certs/ee-cert.pem
openssl-1.1.1w/test/certs/ee-cert2.pem
openssl-1.1.1w/test/certs/ee-client-chain.pem
openssl-1.1.1w/test/certs/ee-client.pem
openssl-1.1.1w/test/certs/ee-clientAuth.pem
openssl-1.1.1w/test/certs/ee-ecdsa-client-chain.pem
openssl-1.1.1w/test/certs/ee-ecdsa-key.pem
openssl-1.1.1w/test/certs/ee-ed25519.pem
openssl-1.1.1w/test/certs/ee-expired.pem
openssl-1.1.1w/test/certs/ee-key-768.pem
openssl-1.1.1w/test/certs/ee-key-ec-explicit.pem
openssl-1.1.1w/test/certs/ee-key-ec-named-explicit.pem
openssl-1.1.1w/test/certs/ee-key-ec-named-named.pem
openssl-1.1.1w/test/certs/ee-key.pem
openssl-1.1.1w/test/certs/ee-name2.pem
openssl-1.1.1w/test/certs/ee-pathlen.pem
openssl-1.1.1w/test/certs/ee-pss-cert.pem
openssl-1.1.1w/test/certs/ee-pss-sha1-cert.pem
openssl-1.1.1w/test/certs/ee-pss-sha256-cert.pem
openssl-1.1.1w/test/certs/ee-self-signed.pem
openssl-1.1.1w/test/certs/ee-serverAuth.pem
openssl-1.1.1w/test/certs/embeddedSCTs1-key.pem
openssl-1.1.1w/test/certs/embeddedSCTs1.pem
openssl-1.1.1w/test/certs/embeddedSCTs1.sct
openssl-1.1.1w/test/certs/embeddedSCTs1_issuer-key.pem
openssl-1.1.1w/test/certs/embeddedSCTs1_issuer.pem
openssl-1.1.1w/test/certs/embeddedSCTs3.pem
openssl-1.1.1w/test/certs/embeddedSCTs3.sct
openssl-1.1.1w/test/certs/embeddedSCTs3_issuer.pem
openssl-1.1.1w/test/certs/goodcn1-cert.pem
openssl-1.1.1w/test/certs/goodcn1-key.pem
openssl-1.1.1w/test/certs/interCA.key
openssl-1.1.1w/test/certs/interCA.pem
openssl-1.1.1w/test/certs/invalid-cert.pem
openssl-1.1.1w/test/certs/leaf.key
openssl-1.1.1w/test/certs/leaf.pem
openssl-1.1.1w/test/certs/many-constraints.pem
openssl-1.1.1w/test/certs/many-names1.pem
openssl-1.1.1w/test/certs/many-names2.pem
openssl-1.1.1w/test/certs/many-names3.pem
openssl-1.1.1w/test/certs/mkcert.sh
openssl-1.1.1w/test/certs/nca+anyEKU.pem
openssl-1.1.1w/test/certs/nca+serverAuth.pem
openssl-1.1.1w/test/certs/ncca-cert.pem
openssl-1.1.1w/test/certs/ncca-key.pem
openssl-1.1.1w/test/certs/ncca1-cert.pem
openssl-1.1.1w/test/certs/ncca1-key.pem
openssl-1.1.1w/test/certs/ncca2-cert.pem
openssl-1.1.1w/test/certs/ncca2-key.pem
openssl-1.1.1w/test/certs/ncca3-cert.pem
openssl-1.1.1w/test/certs/ncca3-key.pem
openssl-1.1.1w/test/certs/nroot+anyEKU.pem
openssl-1.1.1w/test/certs/nroot+serverAuth.pem
openssl-1.1.1w/test/certs/p256-server-cert.pem
openssl-1.1.1w/test/certs/p256-server-key.pem
openssl-1.1.1w/test/certs/p384-root-key.pem
openssl-1.1.1w/test/certs/p384-root.pem
openssl-1.1.1w/test/certs/p384-server-cert.pem
openssl-1.1.1w/test/certs/p384-server-key.pem
openssl-1.1.1w/test/certs/pathlen.pem
openssl-1.1.1w/test/certs/pc1-cert.pem
openssl-1.1.1w/test/certs/pc1-key.pem
openssl-1.1.1w/test/certs/pc2-cert.pem
openssl-1.1.1w/test/certs/pc2-key.pem
openssl-1.1.1w/test/certs/pc5-cert.pem
openssl-1.1.1w/test/certs/pc5-key.pem
openssl-1.1.1w/test/certs/root+anyEKU.pem
openssl-1.1.1w/test/certs/root+clientAuth.pem
openssl-1.1.1w/test/certs/root+serverAuth.pem
openssl-1.1.1w/test/certs/root-anyEKU.pem
openssl-1.1.1w/test/certs/root-cert-768.pem
openssl-1.1.1w/test/certs/root-cert-md5.pem
openssl-1.1.1w/test/certs/root-cert-rsa2.pem
openssl-1.1.1w/test/certs/root-cert.pem
openssl-1.1.1w/test/certs/root-cert2.pem
openssl-1.1.1w/test/certs/root-clientAuth.pem
openssl-1.1.1w/test/certs/root-cross-cert.pem
openssl-1.1.1w/test/certs/root-ed25519.pem
openssl-1.1.1w/test/certs/root-ed448-cert.pem
openssl-1.1.1w/test/certs/root-ed448-key.pem
openssl-1.1.1w/test/certs/root-expired.pem
openssl-1.1.1w/test/certs/root-key-768.pem
openssl-1.1.1w/test/certs/root-key.pem
openssl-1.1.1w/test/certs/root-key2.pem
openssl-1.1.1w/test/certs/root-name2.pem
openssl-1.1.1w/test/certs/root-nonca.pem
openssl-1.1.1w/test/certs/root-noserver.pem
openssl-1.1.1w/test/certs/root-serverAuth.pem
openssl-1.1.1w/test/certs/root2+clientAuth.pem
openssl-1.1.1w/test/certs/root2+serverAuth.pem
openssl-1.1.1w/test/certs/root2-serverAuth.pem
openssl-1.1.1w/test/certs/rootCA.key
openssl-1.1.1w/test/certs/rootCA.pem
openssl-1.1.1w/test/certs/rootcert.pem
openssl-1.1.1w/test/certs/rootkey.pem
openssl-1.1.1w/test/certs/roots.pem
openssl-1.1.1w/test/certs/sca+anyEKU.pem
openssl-1.1.1w/test/certs/sca+clientAuth.pem
openssl-1.1.1w/test/certs/sca+serverAuth.pem
openssl-1.1.1w/test/certs/sca-anyEKU.pem
openssl-1.1.1w/test/certs/sca-cert.pem
openssl-1.1.1w/test/certs/sca-clientAuth.pem
openssl-1.1.1w/test/certs/sca-serverAuth.pem
openssl-1.1.1w/test/certs/server-cecdsa-cert.pem
openssl-1.1.1w/test/certs/server-cecdsa-key.pem
openssl-1.1.1w/test/certs/server-dsa-cert.pem
openssl-1.1.1w/test/certs/server-dsa-key.pem
openssl-1.1.1w/test/certs/server-ecdsa-brainpoolP256r1-cert.pem
openssl-1.1.1w/test/certs/server-ecdsa-brainpoolP256r1-key.pem
openssl-1.1.1w/test/certs/server-ecdsa-cert.pem
openssl-1.1.1w/test/certs/server-ecdsa-key.pem
openssl-1.1.1w/test/certs/server-ed25519-cert.pem
openssl-1.1.1w/test/certs/server-ed25519-key.pem
openssl-1.1.1w/test/certs/server-ed448-cert.pem
openssl-1.1.1w/test/certs/server-ed448-key.pem
openssl-1.1.1w/test/certs/server-pss-cert.pem
openssl-1.1.1w/test/certs/server-pss-key.pem
openssl-1.1.1w/test/certs/server-pss-restrict-cert.pem
openssl-1.1.1w/test/certs/server-pss-restrict-key.pem
openssl-1.1.1w/test/certs/server-trusted.pem
openssl-1.1.1w/test/certs/servercert.pem
openssl-1.1.1w/test/certs/serverkey.pem
openssl-1.1.1w/test/certs/setup.sh
openssl-1.1.1w/test/certs/some-names1.pem
openssl-1.1.1w/test/certs/some-names2.pem
openssl-1.1.1w/test/certs/some-names3.pem
openssl-1.1.1w/test/certs/sroot+anyEKU.pem
openssl-1.1.1w/test/certs/sroot+clientAuth.pem
openssl-1.1.1w/test/certs/sroot+serverAuth.pem
openssl-1.1.1w/test/certs/sroot-anyEKU.pem
openssl-1.1.1w/test/certs/sroot-cert.pem
openssl-1.1.1w/test/certs/sroot-clientAuth.pem
openssl-1.1.1w/test/certs/sroot-serverAuth.pem
openssl-1.1.1w/test/certs/subinterCA-ss.pem
openssl-1.1.1w/test/certs/subinterCA.key
openssl-1.1.1w/test/certs/subinterCA.pem
openssl-1.1.1w/test/certs/untrusted.pem
openssl-1.1.1w/test/certs/wrongcert.pem
openssl-1.1.1w/test/certs/wrongkey.pem
openssl-1.1.1w/test/certs/x509-check-key.pem
openssl-1.1.1w/test/certs/x509-check.csr
openssl-1.1.1w/test/chacha_internal_test.c
openssl-1.1.1w/test/cipher_overhead_test.c
openssl-1.1.1w/test/cipherbytes_test.c
openssl-1.1.1w/test/cipherlist_test.c
openssl-1.1.1w/test/ciphername_test.c
openssl-1.1.1w/test/clienthellotest.c
openssl-1.1.1w/test/cmactest.c
openssl-1.1.1w/test/cms-examples.pl
openssl-1.1.1w/test/cmsapitest.c
openssl-1.1.1w/test/conf_include_test.c
openssl-1.1.1w/test/constant_time_test.c
openssl-1.1.1w/test/crltest.c
openssl-1.1.1w/test/ct/
openssl-1.1.1w/test/ct/log_list.conf
openssl-1.1.1w/test/ct/tls1.sct
openssl-1.1.1w/test/ct_test.c
openssl-1.1.1w/test/ctype_internal_test.c
openssl-1.1.1w/test/curve448_internal_test.c
openssl-1.1.1w/test/d2i-tests/
openssl-1.1.1w/test/d2i-tests/bad-cms.der
openssl-1.1.1w/test/d2i-tests/bad-int-pad0.der
openssl-1.1.1w/test/d2i-tests/bad-int-padminus1.der
openssl-1.1.1w/test/d2i-tests/bad_bio.der
openssl-1.1.1w/test/d2i-tests/bad_cert.der
openssl-1.1.1w/test/d2i-tests/bad_generalname.der
openssl-1.1.1w/test/d2i-tests/high_tag.der
openssl-1.1.1w/test/d2i-tests/int0.der
openssl-1.1.1w/test/d2i-tests/int1.der
openssl-1.1.1w/test/d2i-tests/intminus1.der
openssl-1.1.1w/test/d2i_test.c
openssl-1.1.1w/test/dane-cross.in
openssl-1.1.1w/test/danetest.c
openssl-1.1.1w/test/danetest.in
openssl-1.1.1w/test/danetest.pem
openssl-1.1.1w/test/data.bin
openssl-1.1.1w/test/destest.c
openssl-1.1.1w/test/dhtest.c
openssl-1.1.1w/test/drbg_cavs_data.c
openssl-1.1.1w/test/drbg_cavs_data.h
openssl-1.1.1w/test/drbg_cavs_test.c
openssl-1.1.1w/test/drbgtest.c
openssl-1.1.1w/test/drbgtest.h
openssl-1.1.1w/test/dsa_no_digest_size_test.c
openssl-1.1.1w/test/dsatest.c
openssl-1.1.1w/test/dtls_mtu_test.c
openssl-1.1.1w/test/dtlstest.c
openssl-1.1.1w/test/dtlsv1listentest.c
openssl-1.1.1w/test/ec_internal_test.c
openssl-1.1.1w/test/ecdsatest.c
openssl-1.1.1w/test/ecdsatest.h
openssl-1.1.1w/test/ecstresstest.c
openssl-1.1.1w/test/ectest.c
openssl-1.1.1w/test/enginetest.c
openssl-1.1.1w/test/errtest.c
openssl-1.1.1w/test/evp_extra_test.c
openssl-1.1.1w/test/evp_test.c
openssl-1.1.1w/test/evp_test.h
openssl-1.1.1w/test/exdatatest.c
openssl-1.1.1w/test/exptest.c
openssl-1.1.1w/test/fatalerrtest.c
openssl-1.1.1w/test/generate_buildtest.pl
openssl-1.1.1w/test/generate_ssl_tests.pl
openssl-1.1.1w/test/gmdifftest.c
openssl-1.1.1w/test/gosttest.c
openssl-1.1.1w/test/handshake_helper.c
openssl-1.1.1w/test/handshake_helper.h
openssl-1.1.1w/test/hmactest.c
openssl-1.1.1w/test/ideatest.c
openssl-1.1.1w/test/igetest.c
openssl-1.1.1w/test/lhash_test.c
openssl-1.1.1w/test/md2test.c
openssl-1.1.1w/test/mdc2_internal_test.c
openssl-1.1.1w/test/mdc2test.c
openssl-1.1.1w/test/memleaktest.c
openssl-1.1.1w/test/modes_internal_test.c
openssl-1.1.1w/test/ocsp-tests/
openssl-1.1.1w/test/ocsp-tests/D1.ors
openssl-1.1.1w/test/ocsp-tests/D1_Cert_EE.pem
openssl-1.1.1w/test/ocsp-tests/D1_Issuer_ICA.pem
openssl-1.1.1w/test/ocsp-tests/D2.ors
openssl-1.1.1w/test/ocsp-tests/D2_Cert_ICA.pem
openssl-1.1.1w/test/ocsp-tests/D2_Issuer_Root.pem
openssl-1.1.1w/test/ocsp-tests/D3.ors
openssl-1.1.1w/test/ocsp-tests/D3_Cert_EE.pem
openssl-1.1.1w/test/ocsp-tests/D3_Issuer_Root.pem
openssl-1.1.1w/test/ocsp-tests/ISDOSC_D1.ors
openssl-1.1.1w/test/ocsp-tests/ISDOSC_D2.ors
openssl-1.1.1w/test/ocsp-tests/ISDOSC_D3.ors
openssl-1.1.1w/test/ocsp-tests/ISIC_D1_Issuer_ICA.pem
openssl-1.1.1w/test/ocsp-tests/ISIC_D2_Issuer_Root.pem
openssl-1.1.1w/test/ocsp-tests/ISIC_D3_Issuer_Root.pem
openssl-1.1.1w/test/ocsp-tests/ISIC_ND1_Issuer_ICA.pem
openssl-1.1.1w/test/ocsp-tests/ISIC_ND2_Issuer_Root.pem
openssl-1.1.1w/test/ocsp-tests/ISIC_ND3_Issuer_Root.pem
openssl-1.1.1w/test/ocsp-tests/ISOP_D1.ors
openssl-1.1.1w/test/ocsp-tests/ISOP_D2.ors
openssl-1.1.1w/test/ocsp-tests/ISOP_D3.ors
openssl-1.1.1w/test/ocsp-tests/ISOP_ND1.ors
openssl-1.1.1w/test/ocsp-tests/ISOP_ND2.ors
openssl-1.1.1w/test/ocsp-tests/ISOP_ND3.ors
openssl-1.1.1w/test/ocsp-tests/ND1.ors
openssl-1.1.1w/test/ocsp-tests/ND1_Cert_EE.pem
openssl-1.1.1w/test/ocsp-tests/ND1_Cross_Root.pem
openssl-1.1.1w/test/ocsp-tests/ND1_Issuer_ICA-Cross.pem
openssl-1.1.1w/test/ocsp-tests/ND1_Issuer_ICA.pem
openssl-1.1.1w/test/ocsp-tests/ND2.ors
openssl-1.1.1w/test/ocsp-tests/ND2_Cert_ICA.pem
openssl-1.1.1w/test/ocsp-tests/ND2_Issuer_Root.pem
openssl-1.1.1w/test/ocsp-tests/ND3.ors
openssl-1.1.1w/test/ocsp-tests/ND3_Cert_EE.pem
openssl-1.1.1w/test/ocsp-tests/ND3_Issuer_Root.pem
openssl-1.1.1w/test/ocsp-tests/WIKH_D1.ors
openssl-1.1.1w/test/ocsp-tests/WIKH_D2.ors
openssl-1.1.1w/test/ocsp-tests/WIKH_D3.ors
openssl-1.1.1w/test/ocsp-tests/WIKH_ND1.ors
openssl-1.1.1w/test/ocsp-tests/WIKH_ND2.ors
openssl-1.1.1w/test/ocsp-tests/WIKH_ND3.ors
openssl-1.1.1w/test/ocsp-tests/WINH_D1.ors
openssl-1.1.1w/test/ocsp-tests/WINH_D2.ors
openssl-1.1.1w/test/ocsp-tests/WINH_D3.ors
openssl-1.1.1w/test/ocsp-tests/WINH_ND1.ors
openssl-1.1.1w/test/ocsp-tests/WINH_ND2.ors
openssl-1.1.1w/test/ocsp-tests/WINH_ND3.ors
openssl-1.1.1w/test/ocsp-tests/WKDOSC_D1.ors
openssl-1.1.1w/test/ocsp-tests/WKDOSC_D2.ors
openssl-1.1.1w/test/ocsp-tests/WKDOSC_D3.ors
openssl-1.1.1w/test/ocsp-tests/WKIC_D1_Issuer_ICA.pem
openssl-1.1.1w/test/ocsp-tests/WKIC_D2_Issuer_Root.pem
openssl-1.1.1w/test/ocsp-tests/WKIC_D3_Issuer_Root.pem
openssl-1.1.1w/test/ocsp-tests/WKIC_ND1_Issuer_ICA.pem
openssl-1.1.1w/test/ocsp-tests/WKIC_ND2_Issuer_Root.pem
openssl-1.1.1w/test/ocsp-tests/WKIC_ND3_Issuer_Root.pem
openssl-1.1.1w/test/ocsp-tests/WRID_D1.ors
openssl-1.1.1w/test/ocsp-tests/WRID_D2.ors
openssl-1.1.1w/test/ocsp-tests/WRID_D3.ors
openssl-1.1.1w/test/ocsp-tests/WRID_ND1.ors
openssl-1.1.1w/test/ocsp-tests/WRID_ND2.ors
openssl-1.1.1w/test/ocsp-tests/WRID_ND3.ors
openssl-1.1.1w/test/ocsp-tests/WSNIC_D1_Issuer_ICA.pem
openssl-1.1.1w/test/ocsp-tests/WSNIC_D2_Issuer_Root.pem
openssl-1.1.1w/test/ocsp-tests/WSNIC_D3_Issuer_Root.pem
openssl-1.1.1w/test/ocsp-tests/WSNIC_ND1_Issuer_ICA.pem
openssl-1.1.1w/test/ocsp-tests/WSNIC_ND2_Issuer_Root.pem
openssl-1.1.1w/test/ocsp-tests/WSNIC_ND3_Issuer_Root.pem
openssl-1.1.1w/test/ocspapitest.c
openssl-1.1.1w/test/ossl_shim/
openssl-1.1.1w/test/ossl_shim/async_bio.cc
openssl-1.1.1w/test/ossl_shim/async_bio.h
openssl-1.1.1w/test/ossl_shim/build.info
openssl-1.1.1w/test/ossl_shim/include/
openssl-1.1.1w/test/ossl_shim/include/openssl/
openssl-1.1.1w/test/ossl_shim/include/openssl/base.h
openssl-1.1.1w/test/ossl_shim/ossl_config.json
openssl-1.1.1w/test/ossl_shim/ossl_shim.cc
openssl-1.1.1w/test/ossl_shim/packeted_bio.cc
openssl-1.1.1w/test/ossl_shim/packeted_bio.h
openssl-1.1.1w/test/ossl_shim/test_config.cc
openssl-1.1.1w/test/ossl_shim/test_config.h
openssl-1.1.1w/test/packettest.c
openssl-1.1.1w/test/pbelutest.c
openssl-1.1.1w/test/pemtest.c
openssl-1.1.1w/test/pkcs7-1.pem
openssl-1.1.1w/test/pkcs7.pem
openssl-1.1.1w/test/pkey_meth_kdf_test.c
openssl-1.1.1w/test/pkey_meth_test.c
openssl-1.1.1w/test/pkits-test.pl
openssl-1.1.1w/test/poly1305_internal_test.c
openssl-1.1.1w/test/rc2test.c
openssl-1.1.1w/test/rc4test.c
openssl-1.1.1w/test/rc5test.c
openssl-1.1.1w/test/rdrand_sanitytest.c
openssl-1.1.1w/test/recipes/
openssl-1.1.1w/test/recipes/01-test_abort.t
openssl-1.1.1w/test/recipes/01-test_sanity.t
openssl-1.1.1w/test/recipes/01-test_symbol_presence.t
openssl-1.1.1w/test/recipes/01-test_test.t
openssl-1.1.1w/test/recipes/02-test_errstr.t
openssl-1.1.1w/test/recipes/02-test_internal_ctype.t
openssl-1.1.1w/test/recipes/02-test_lhash.t
openssl-1.1.1w/test/recipes/02-test_ordinals.t
openssl-1.1.1w/test/recipes/02-test_stack.t
openssl-1.1.1w/test/recipes/03-test_exdata.t
openssl-1.1.1w/test/recipes/03-test_internal_asn1.t
openssl-1.1.1w/test/recipes/03-test_internal_chacha.t
openssl-1.1.1w/test/recipes/03-test_internal_curve448.t
openssl-1.1.1w/test/recipes/03-test_internal_ec.t
openssl-1.1.1w/test/recipes/03-test_internal_mdc2.t
openssl-1.1.1w/test/recipes/03-test_internal_modes.t
openssl-1.1.1w/test/recipes/03-test_internal_poly1305.t
openssl-1.1.1w/test/recipes/03-test_internal_siphash.t
openssl-1.1.1w/test/recipes/03-test_internal_sm2.t
openssl-1.1.1w/test/recipes/03-test_internal_sm4.t
openssl-1.1.1w/test/recipes/03-test_internal_ssl_cert_table.t
openssl-1.1.1w/test/recipes/03-test_internal_x509.t
openssl-1.1.1w/test/recipes/03-test_ui.t
openssl-1.1.1w/test/recipes/04-test_asn1_decode.t
openssl-1.1.1w/test/recipes/04-test_asn1_encode.t
openssl-1.1.1w/test/recipes/04-test_asn1_string_table.t
openssl-1.1.1w/test/recipes/04-test_bio_callback.t
openssl-1.1.1w/test/recipes/04-test_bioprint.t
openssl-1.1.1w/test/recipes/04-test_err.t
openssl-1.1.1w/test/recipes/04-test_pem.t
openssl-1.1.1w/test/recipes/04-test_pem_data/
openssl-1.1.1w/test/recipes/04-test_pem_data/NOTES
openssl-1.1.1w/test/recipes/04-test_pem_data/beermug.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-1023line.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-1024line.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-1025line.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-254-chars-at-the-end.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-254-chars-in-the-middle.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-255line.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-256line.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-257line.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-blankline.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-comment.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-earlypad.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-extrapad.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-infixwhitespace.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-junk.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-leadingwhitespace.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-longline.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-misalignedpad.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-onecolumn.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-oneline-multiple-of-254.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-oneline.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-shortandlongline.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-shortline.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-threecolumn.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert-trailingwhitespace.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/cert.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/csr.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-1023line.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-1024line.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-1025line.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-255line.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-256line.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-257line.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-blankline.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-comment.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-corruptedheader.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-corruptiv.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-earlypad.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-extrapad.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-infixwhitespace.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-junk.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-leadingwhitespace.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-longline.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-misalignedpad.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-onecolumn.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-oneline.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-onelineheader.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-shortandlongline.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-shortline.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-threecolumn.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa-trailingwhitespace.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsa.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/dsaparam.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/key.pem
openssl-1.1.1w/test/recipes/04-test_pem_data/wellknown
openssl-1.1.1w/test/recipes/05-test_bf.t
openssl-1.1.1w/test/recipes/05-test_cast.t
openssl-1.1.1w/test/recipes/05-test_cmac.t
openssl-1.1.1w/test/recipes/05-test_des.t
openssl-1.1.1w/test/recipes/05-test_hmac.t
openssl-1.1.1w/test/recipes/05-test_idea.t
openssl-1.1.1w/test/recipes/05-test_md2.t
openssl-1.1.1w/test/recipes/05-test_mdc2.t
openssl-1.1.1w/test/recipes/05-test_rand.t
openssl-1.1.1w/test/recipes/05-test_rc2.t
openssl-1.1.1w/test/recipes/05-test_rc4.t
openssl-1.1.1w/test/recipes/05-test_rc5.t
openssl-1.1.1w/test/recipes/06-test-rdrand.t
openssl-1.1.1w/test/recipes/10-test_bn.t
openssl-1.1.1w/test/recipes/10-test_bn_data/
openssl-1.1.1w/test/recipes/10-test_bn_data/bnexp.txt
openssl-1.1.1w/test/recipes/10-test_bn_data/bngcd.txt
openssl-1.1.1w/test/recipes/10-test_bn_data/bnmod.txt
openssl-1.1.1w/test/recipes/10-test_bn_data/bnmul.txt
openssl-1.1.1w/test/recipes/10-test_bn_data/bnshift.txt
openssl-1.1.1w/test/recipes/10-test_bn_data/bnsum.txt
openssl-1.1.1w/test/recipes/10-test_exp.t
openssl-1.1.1w/test/recipes/15-test_dh.t
openssl-1.1.1w/test/recipes/15-test_dsa.t
openssl-1.1.1w/test/recipes/15-test_ec.t
openssl-1.1.1w/test/recipes/15-test_ecdsa.t
openssl-1.1.1w/test/recipes/15-test_ecparam.t
openssl-1.1.1w/test/recipes/15-test_ecparam_data/
openssl-1.1.1w/test/recipes/15-test_ecparam_data/invalid/
openssl-1.1.1w/test/recipes/15-test_ecparam_data/invalid/c2pnb208w1-reducible.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/invalid/nistp256-nonprime.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/invalid/nistp256-offcurve.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/invalid/nistp256-wrongorder.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2pnb163v1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2pnb163v1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2pnb163v2-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2pnb163v2-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2pnb163v3-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2pnb163v3-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2pnb176v1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2pnb176v1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2pnb208w1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2pnb208w1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2pnb272w1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2pnb272w1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2pnb304w1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2pnb304w1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2pnb368w1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2pnb368w1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2tnb191v1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2tnb191v1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2tnb191v2-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2tnb191v2-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2tnb191v3-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2tnb191v3-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2tnb239v1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2tnb239v1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2tnb239v2-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2tnb239v2-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2tnb239v3-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2tnb239v3-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2tnb359v1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2tnb359v1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2tnb431r1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/c2tnb431r1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/prime192v1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/prime192v1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/prime192v2-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/prime192v2-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/prime192v3-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/prime192v3-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/prime239v1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/prime239v1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/prime239v2-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/prime239v2-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/prime239v3-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/prime239v3-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/prime256v1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/prime256v1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp112r1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp112r1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp112r2-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp112r2-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp128r1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp128r1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp128r2-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp128r2-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp160k1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp160k1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp160r1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp160r1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp160r2-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp160r2-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp192k1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp192k1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp224k1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp224k1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp224r1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp224r1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp256k1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp256k1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp384r1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp384r1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp521r1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/secp521r1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect113r1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect113r1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect113r2-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect113r2-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect131r1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect131r1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect131r2-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect131r2-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect163k1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect163k1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect163r1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect163r1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect163r2-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect163r2-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect193r1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect193r1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect193r2-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect193r2-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect233k1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect233k1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect233r1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect233r1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect239k1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect239k1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect283k1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect283k1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect283r1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect283r1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect409k1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect409k1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect409r1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect409r1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect571k1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect571k1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect571r1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/sect571r1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls1-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls1-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls10-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls10-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls11-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls11-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls12-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls12-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls3-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls3-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls4-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls4-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls5-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls5-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls6-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls6-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls7-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls7-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls8-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls8-named.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls9-explicit.pem
openssl-1.1.1w/test/recipes/15-test_ecparam_data/valid/wap-wsg-idm-ecid-wtls9-named.pem
openssl-1.1.1w/test/recipes/15-test_genec.t
openssl-1.1.1w/test/recipes/15-test_genrsa.t
openssl-1.1.1w/test/recipes/15-test_mp_rsa.t
openssl-1.1.1w/test/recipes/15-test_mp_rsa_data/
openssl-1.1.1w/test/recipes/15-test_mp_rsa_data/plain_text
openssl-1.1.1w/test/recipes/15-test_out_option.t
openssl-1.1.1w/test/recipes/15-test_rsa.t
openssl-1.1.1w/test/recipes/15-test_rsapss.t
openssl-1.1.1w/test/recipes/20-test_dgst.t
openssl-1.1.1w/test/recipes/20-test_enc.t
openssl-1.1.1w/test/recipes/20-test_enc_more.t
openssl-1.1.1w/test/recipes/20-test_passwd.t
openssl-1.1.1w/test/recipes/25-test_crl.t
openssl-1.1.1w/test/recipes/25-test_d2i.t
openssl-1.1.1w/test/recipes/25-test_pkcs7.t
openssl-1.1.1w/test/recipes/25-test_req.t
openssl-1.1.1w/test/recipes/25-test_sid.t
openssl-1.1.1w/test/recipes/25-test_verify.t
openssl-1.1.1w/test/recipes/25-test_x509.t
openssl-1.1.1w/test/recipes/30-test_afalg.t
openssl-1.1.1w/test/recipes/30-test_engine.t
openssl-1.1.1w/test/recipes/30-test_evp.t
openssl-1.1.1w/test/recipes/30-test_evp_data/
openssl-1.1.1w/test/recipes/30-test_evp_data/evpcase.txt
openssl-1.1.1w/test/recipes/30-test_evp_data/evpccmcavs.txt
openssl-1.1.1w/test/recipes/30-test_evp_data/evpciph.txt
openssl-1.1.1w/test/recipes/30-test_evp_data/evpdigest.txt
openssl-1.1.1w/test/recipes/30-test_evp_data/evpencod.txt
openssl-1.1.1w/test/recipes/30-test_evp_data/evpkdf.txt
openssl-1.1.1w/test/recipes/30-test_evp_data/evpmac.txt
openssl-1.1.1w/test/recipes/30-test_evp_data/evppbe.txt
openssl-1.1.1w/test/recipes/30-test_evp_data/evppkey.txt
openssl-1.1.1w/test/recipes/30-test_evp_data/evppkey_ecc.txt
openssl-1.1.1w/test/recipes/30-test_evp_extra.t
openssl-1.1.1w/test/recipes/30-test_pbelu.t
openssl-1.1.1w/test/recipes/30-test_pkey_meth.t
openssl-1.1.1w/test/recipes/30-test_pkey_meth_kdf.t
openssl-1.1.1w/test/recipes/40-test_rehash.t
openssl-1.1.1w/test/recipes/60-test_x509_check_cert_pkey.t
openssl-1.1.1w/test/recipes/60-test_x509_dup_cert.t
openssl-1.1.1w/test/recipes/60-test_x509_store.t
openssl-1.1.1w/test/recipes/60-test_x509_time.t
openssl-1.1.1w/test/recipes/70-test_asyncio.t
openssl-1.1.1w/test/recipes/70-test_bad_dtls.t
openssl-1.1.1w/test/recipes/70-test_clienthello.t
openssl-1.1.1w/test/recipes/70-test_comp.t
openssl-1.1.1w/test/recipes/70-test_key_share.t
openssl-1.1.1w/test/recipes/70-test_packet.t
openssl-1.1.1w/test/recipes/70-test_recordlen.t
openssl-1.1.1w/test/recipes/70-test_renegotiation.t
openssl-1.1.1w/test/recipes/70-test_servername.t
openssl-1.1.1w/test/recipes/70-test_sslcbcpadding.t
openssl-1.1.1w/test/recipes/70-test_sslcertstatus.t
openssl-1.1.1w/test/recipes/70-test_sslextension.t
openssl-1.1.1w/test/recipes/70-test_sslmessages.t
openssl-1.1.1w/test/recipes/70-test_sslrecords.t
openssl-1.1.1w/test/recipes/70-test_sslsessiontick.t
openssl-1.1.1w/test/recipes/70-test_sslsigalgs.t
openssl-1.1.1w/test/recipes/70-test_sslsignature.t
openssl-1.1.1w/test/recipes/70-test_sslskewith0p.t
openssl-1.1.1w/test/recipes/70-test_sslversions.t
openssl-1.1.1w/test/recipes/70-test_sslvertol.t
openssl-1.1.1w/test/recipes/70-test_tls13alerts.t
openssl-1.1.1w/test/recipes/70-test_tls13cookie.t
openssl-1.1.1w/test/recipes/70-test_tls13downgrade.t
openssl-1.1.1w/test/recipes/70-test_tls13hrr.t
openssl-1.1.1w/test/recipes/70-test_tls13kexmodes.t
openssl-1.1.1w/test/recipes/70-test_tls13messages.t
openssl-1.1.1w/test/recipes/70-test_tls13psk.t
openssl-1.1.1w/test/recipes/70-test_tlsextms.t
openssl-1.1.1w/test/recipes/70-test_verify_extra.t
openssl-1.1.1w/test/recipes/70-test_wpacket.t
openssl-1.1.1w/test/recipes/80-test_ca.t
openssl-1.1.1w/test/recipes/80-test_cipherbytes.t
openssl-1.1.1w/test/recipes/80-test_cipherlist.t
openssl-1.1.1w/test/recipes/80-test_ciphername.t
openssl-1.1.1w/test/recipes/80-test_cms.t
openssl-1.1.1w/test/recipes/80-test_cms_data/
openssl-1.1.1w/test/recipes/80-test_cms_data/bad_signtime_attr.cms
openssl-1.1.1w/test/recipes/80-test_cms_data/ct_multiple_attr.cms
openssl-1.1.1w/test/recipes/80-test_cms_data/no_ct_attr.cms
openssl-1.1.1w/test/recipes/80-test_cms_data/no_md_attr.cms
openssl-1.1.1w/test/recipes/80-test_cmsapi.t
openssl-1.1.1w/test/recipes/80-test_ct.t
openssl-1.1.1w/test/recipes/80-test_dane.t
openssl-1.1.1w/test/recipes/80-test_dtls.t
openssl-1.1.1w/test/recipes/80-test_dtls_mtu.t
openssl-1.1.1w/test/recipes/80-test_dtlsv1listen.t
openssl-1.1.1w/test/recipes/80-test_ocsp.t
openssl-1.1.1w/test/recipes/80-test_ocsp_data/
openssl-1.1.1w/test/recipes/80-test_ocsp_data/cert.pem
openssl-1.1.1w/test/recipes/80-test_ocsp_data/key.pem
openssl-1.1.1w/test/recipes/80-test_pkcs12.t
openssl-1.1.1w/test/recipes/80-test_policy_tree.t
openssl-1.1.1w/test/recipes/80-test_policy_tree_data/
openssl-1.1.1w/test/recipes/80-test_policy_tree_data/large_leaf.pem
openssl-1.1.1w/test/recipes/80-test_policy_tree_data/large_policy_tree.pem
openssl-1.1.1w/test/recipes/80-test_policy_tree_data/small_leaf.pem
openssl-1.1.1w/test/recipes/80-test_policy_tree_data/small_policy_tree.pem
openssl-1.1.1w/test/recipes/80-test_ssl_new.t
openssl-1.1.1w/test/recipes/80-test_ssl_old.t
openssl-1.1.1w/test/recipes/80-test_ssl_test_ctx.t
openssl-1.1.1w/test/recipes/80-test_sslcorrupt.t
openssl-1.1.1w/test/recipes/80-test_tsa.t
openssl-1.1.1w/test/recipes/80-test_x509aux.t
openssl-1.1.1w/test/recipes/90-test_asn1_time.t
openssl-1.1.1w/test/recipes/90-test_async.t
openssl-1.1.1w/test/recipes/90-test_bio_enc.t
openssl-1.1.1w/test/recipes/90-test_bio_memleak.t
openssl-1.1.1w/test/recipes/90-test_constant_time.t
openssl-1.1.1w/test/recipes/90-test_fatalerr.t
openssl-1.1.1w/test/recipes/90-test_gmdiff.t
openssl-1.1.1w/test/recipes/90-test_gost.t
openssl-1.1.1w/test/recipes/90-test_gost_data/
openssl-1.1.1w/test/recipes/90-test_gost_data/gost.conf
openssl-1.1.1w/test/recipes/90-test_gost_data/server-cert2001.pem
openssl-1.1.1w/test/recipes/90-test_gost_data/server-cert2012.pem
openssl-1.1.1w/test/recipes/90-test_gost_data/server-key2001.pem
openssl-1.1.1w/test/recipes/90-test_gost_data/server-key2012.pem
openssl-1.1.1w/test/recipes/90-test_ige.t
openssl-1.1.1w/test/recipes/90-test_includes.t
openssl-1.1.1w/test/recipes/90-test_includes_data/
openssl-1.1.1w/test/recipes/90-test_includes_data/conf-includes/
openssl-1.1.1w/test/recipes/90-test_includes_data/conf-includes/includes1.cnf
openssl-1.1.1w/test/recipes/90-test_includes_data/conf-includes/includes2.cnf
openssl-1.1.1w/test/recipes/90-test_includes_data/includes-broken.cnf
openssl-1.1.1w/test/recipes/90-test_includes_data/includes-eq-ws.cnf
openssl-1.1.1w/test/recipes/90-test_includes_data/includes-eq.cnf
openssl-1.1.1w/test/recipes/90-test_includes_data/includes-file.cnf
openssl-1.1.1w/test/recipes/90-test_includes_data/includes.cnf
openssl-1.1.1w/test/recipes/90-test_includes_data/vms-includes-file.cnf
openssl-1.1.1w/test/recipes/90-test_includes_data/vms-includes.cnf
openssl-1.1.1w/test/recipes/90-test_memleak.t
openssl-1.1.1w/test/recipes/90-test_overhead.t
openssl-1.1.1w/test/recipes/90-test_secmem.t
openssl-1.1.1w/test/recipes/90-test_shlibload.t
openssl-1.1.1w/test/recipes/90-test_srp.t
openssl-1.1.1w/test/recipes/90-test_sslapi.t
openssl-1.1.1w/test/recipes/90-test_sslapi_data/
openssl-1.1.1w/test/recipes/90-test_sslapi_data/passwd.txt
openssl-1.1.1w/test/recipes/90-test_sslbuffers.t
openssl-1.1.1w/test/recipes/90-test_store.t
openssl-1.1.1w/test/recipes/90-test_store_data/
openssl-1.1.1w/test/recipes/90-test_store_data/ca.cnf
openssl-1.1.1w/test/recipes/90-test_store_data/user.cnf
openssl-1.1.1w/test/recipes/90-test_sysdefault.t
openssl-1.1.1w/test/recipes/90-test_threads.t
openssl-1.1.1w/test/recipes/90-test_time_offset.t
openssl-1.1.1w/test/recipes/90-test_tls13ccs.t
openssl-1.1.1w/test/recipes/90-test_tls13encryption.t
openssl-1.1.1w/test/recipes/90-test_tls13secrets.t
openssl-1.1.1w/test/recipes/90-test_v3name.t
openssl-1.1.1w/test/recipes/95-test_external_boringssl.t
openssl-1.1.1w/test/recipes/95-test_external_krb5.t
openssl-1.1.1w/test/recipes/95-test_external_krb5_data/
openssl-1.1.1w/test/recipes/95-test_external_krb5_data/krb5.sh
openssl-1.1.1w/test/recipes/95-test_external_pyca.t
openssl-1.1.1w/test/recipes/95-test_external_pyca_data/
openssl-1.1.1w/test/recipes/95-test_external_pyca_data/cryptography.sh
openssl-1.1.1w/test/recipes/99-test_ecstress.t
openssl-1.1.1w/test/recipes/99-test_fuzz.t
openssl-1.1.1w/test/recipes/ocsp-response.der
openssl-1.1.1w/test/recipes/tconversion.pl
openssl-1.1.1w/test/recordlentest.c
openssl-1.1.1w/test/rsa_complex.c
openssl-1.1.1w/test/rsa_mp_test.c
openssl-1.1.1w/test/rsa_test.c
openssl-1.1.1w/test/run_tests.pl
openssl-1.1.1w/test/sanitytest.c
openssl-1.1.1w/test/secmemtest.c
openssl-1.1.1w/test/serverinfo.pem
openssl-1.1.1w/test/serverinfo2.pem
openssl-1.1.1w/test/servername_test.c
openssl-1.1.1w/test/session.pem
openssl-1.1.1w/test/shibboleth.pfx
openssl-1.1.1w/test/shlibloadtest.c
openssl-1.1.1w/test/siphash_internal_test.c
openssl-1.1.1w/test/sm2_internal_test.c
openssl-1.1.1w/test/sm4_internal_test.c
openssl-1.1.1w/test/smcont.txt
openssl-1.1.1w/test/smime-certs/
openssl-1.1.1w/test/smime-certs/badrsa.pem
openssl-1.1.1w/test/smime-certs/ca.cnf
openssl-1.1.1w/test/smime-certs/mksmime-certs.sh
openssl-1.1.1w/test/smime-certs/smdh.pem
openssl-1.1.1w/test/smime-certs/smdsa1.pem
openssl-1.1.1w/test/smime-certs/smdsa2.pem
openssl-1.1.1w/test/smime-certs/smdsa3.pem
openssl-1.1.1w/test/smime-certs/smdsap.pem
openssl-1.1.1w/test/smime-certs/smec1.pem
openssl-1.1.1w/test/smime-certs/smec2.pem
openssl-1.1.1w/test/smime-certs/smec3.pem
openssl-1.1.1w/test/smime-certs/smroot.pem
openssl-1.1.1w/test/smime-certs/smrsa1.pem
openssl-1.1.1w/test/smime-certs/smrsa2.pem
openssl-1.1.1w/test/smime-certs/smrsa3.pem
openssl-1.1.1w/test/srptest.c
openssl-1.1.1w/test/ssl-tests/
openssl-1.1.1w/test/ssl-tests/01-simple.conf
openssl-1.1.1w/test/ssl-tests/01-simple.conf.in
openssl-1.1.1w/test/ssl-tests/02-protocol-version.conf
openssl-1.1.1w/test/ssl-tests/02-protocol-version.conf.in
openssl-1.1.1w/test/ssl-tests/03-custom_verify.conf
openssl-1.1.1w/test/ssl-tests/03-custom_verify.conf.in
openssl-1.1.1w/test/ssl-tests/04-client_auth.conf
openssl-1.1.1w/test/ssl-tests/04-client_auth.conf.in
openssl-1.1.1w/test/ssl-tests/05-sni.conf
openssl-1.1.1w/test/ssl-tests/05-sni.conf.in
openssl-1.1.1w/test/ssl-tests/06-sni-ticket.conf
openssl-1.1.1w/test/ssl-tests/06-sni-ticket.conf.in
openssl-1.1.1w/test/ssl-tests/07-dtls-protocol-version.conf
openssl-1.1.1w/test/ssl-tests/07-dtls-protocol-version.conf.in
openssl-1.1.1w/test/ssl-tests/08-npn.conf
openssl-1.1.1w/test/ssl-tests/08-npn.conf.in
openssl-1.1.1w/test/ssl-tests/09-alpn.conf
openssl-1.1.1w/test/ssl-tests/09-alpn.conf.in
openssl-1.1.1w/test/ssl-tests/10-resumption.conf
openssl-1.1.1w/test/ssl-tests/10-resumption.conf.in
openssl-1.1.1w/test/ssl-tests/11-dtls_resumption.conf
openssl-1.1.1w/test/ssl-tests/11-dtls_resumption.conf.in
openssl-1.1.1w/test/ssl-tests/12-ct.conf
openssl-1.1.1w/test/ssl-tests/12-ct.conf.in
openssl-1.1.1w/test/ssl-tests/13-fragmentation.conf
openssl-1.1.1w/test/ssl-tests/13-fragmentation.conf.in
openssl-1.1.1w/test/ssl-tests/14-curves.conf
openssl-1.1.1w/test/ssl-tests/14-curves.conf.in
openssl-1.1.1w/test/ssl-tests/15-certstatus.conf
openssl-1.1.1w/test/ssl-tests/15-certstatus.conf.in
openssl-1.1.1w/test/ssl-tests/16-dtls-certstatus.conf
openssl-1.1.1w/test/ssl-tests/16-dtls-certstatus.conf.in
openssl-1.1.1w/test/ssl-tests/17-renegotiate.conf
openssl-1.1.1w/test/ssl-tests/17-renegotiate.conf.in
openssl-1.1.1w/test/ssl-tests/18-dtls-renegotiate.conf
openssl-1.1.1w/test/ssl-tests/18-dtls-renegotiate.conf.in
openssl-1.1.1w/test/ssl-tests/19-mac-then-encrypt.conf
openssl-1.1.1w/test/ssl-tests/19-mac-then-encrypt.conf.in
openssl-1.1.1w/test/ssl-tests/20-cert-select.conf
openssl-1.1.1w/test/ssl-tests/20-cert-select.conf.in
openssl-1.1.1w/test/ssl-tests/21-key-update.conf
openssl-1.1.1w/test/ssl-tests/21-key-update.conf.in
openssl-1.1.1w/test/ssl-tests/22-compression.conf
openssl-1.1.1w/test/ssl-tests/22-compression.conf.in
openssl-1.1.1w/test/ssl-tests/23-srp.conf
openssl-1.1.1w/test/ssl-tests/23-srp.conf.in
openssl-1.1.1w/test/ssl-tests/24-padding.conf
openssl-1.1.1w/test/ssl-tests/24-padding.conf.in
openssl-1.1.1w/test/ssl-tests/25-cipher.conf
openssl-1.1.1w/test/ssl-tests/25-cipher.conf.in
openssl-1.1.1w/test/ssl-tests/26-tls13_client_auth.conf
openssl-1.1.1w/test/ssl-tests/26-tls13_client_auth.conf.in
openssl-1.1.1w/test/ssl-tests/27-ticket-appdata.conf
openssl-1.1.1w/test/ssl-tests/27-ticket-appdata.conf.in
openssl-1.1.1w/test/ssl-tests/28-seclevel.conf
openssl-1.1.1w/test/ssl-tests/28-seclevel.conf.in
openssl-1.1.1w/test/ssl-tests/29-dtls-sctp-label-bug.conf
openssl-1.1.1w/test/ssl-tests/29-dtls-sctp-label-bug.conf.in
openssl-1.1.1w/test/ssl-tests/30-supported-groups.conf
openssl-1.1.1w/test/ssl-tests/30-supported-groups.conf.in
openssl-1.1.1w/test/ssl-tests/protocol_version.pm
openssl-1.1.1w/test/ssl-tests/ssltests_base.pm
openssl-1.1.1w/test/ssl_cert_table_internal_test.c
openssl-1.1.1w/test/ssl_ctx_test.c
openssl-1.1.1w/test/ssl_test.c
openssl-1.1.1w/test/ssl_test.tmpl
openssl-1.1.1w/test/ssl_test_ctx.c
openssl-1.1.1w/test/ssl_test_ctx.h
openssl-1.1.1w/test/ssl_test_ctx_test.c
openssl-1.1.1w/test/ssl_test_ctx_test.conf
openssl-1.1.1w/test/sslapitest.c
openssl-1.1.1w/test/sslbuffertest.c
openssl-1.1.1w/test/sslcorrupttest.c
openssl-1.1.1w/test/ssltest_old.c
openssl-1.1.1w/test/ssltestlib.c
openssl-1.1.1w/test/ssltestlib.h
openssl-1.1.1w/test/stack_test.c
openssl-1.1.1w/test/sysdefault.cnf
openssl-1.1.1w/test/sysdefaulttest.c
openssl-1.1.1w/test/test.cnf
openssl-1.1.1w/test/test_test.c
openssl-1.1.1w/test/testcrl.pem
openssl-1.1.1w/test/testdsa.pem
openssl-1.1.1w/test/testdsapub.pem
openssl-1.1.1w/test/testec-p256.pem
openssl-1.1.1w/test/testecpub-p256.pem
openssl-1.1.1w/test/tested25519.pem
openssl-1.1.1w/test/tested25519pub.pem
openssl-1.1.1w/test/tested448.pem
openssl-1.1.1w/test/tested448pub.pem
openssl-1.1.1w/test/testp7.pem
openssl-1.1.1w/test/testreq2.pem
openssl-1.1.1w/test/testrsa.pem
openssl-1.1.1w/test/testrsa_withattrs.der
openssl-1.1.1w/test/testrsa_withattrs.pem
openssl-1.1.1w/test/testrsapub.pem
openssl-1.1.1w/test/testsid.pem
openssl-1.1.1w/test/testutil.h
openssl-1.1.1w/test/testutil/
openssl-1.1.1w/test/testutil/basic_output.c
openssl-1.1.1w/test/testutil/cb.c
openssl-1.1.1w/test/testutil/driver.c
openssl-1.1.1w/test/testutil/format_output.c
openssl-1.1.1w/test/testutil/main.c
openssl-1.1.1w/test/testutil/output.h
openssl-1.1.1w/test/testutil/output_helpers.c
openssl-1.1.1w/test/testutil/random.c
openssl-1.1.1w/test/testutil/stanza.c
openssl-1.1.1w/test/testutil/tap_bio.c
openssl-1.1.1w/test/testutil/test_cleanup.c
openssl-1.1.1w/test/testutil/tests.c
openssl-1.1.1w/test/testutil/testutil_init.c
openssl-1.1.1w/test/testutil/tu_local.h
openssl-1.1.1w/test/testx509.pem
openssl-1.1.1w/test/threadstest.c
openssl-1.1.1w/test/time_offset_test.c
openssl-1.1.1w/test/tls13ccstest.c
openssl-1.1.1w/test/tls13encryptiontest.c
openssl-1.1.1w/test/tls13secretstest.c
openssl-1.1.1w/test/uitest.c
openssl-1.1.1w/test/v3-cert1.pem
openssl-1.1.1w/test/v3-cert2.pem
openssl-1.1.1w/test/v3ext.c
openssl-1.1.1w/test/v3nametest.c
openssl-1.1.1w/test/verify_extra_test.c
openssl-1.1.1w/test/versions.c
openssl-1.1.1w/test/wpackettest.c
openssl-1.1.1w/test/x509_check_cert_pkey_test.c
openssl-1.1.1w/test/x509_dup_cert_test.c
openssl-1.1.1w/test/x509_internal_test.c
openssl-1.1.1w/test/x509_time_test.c
openssl-1.1.1w/test/x509aux.c
openssl-1.1.1w/tools/
openssl-1.1.1w/tools/build.info
openssl-1.1.1w/tools/c_rehash.in
openssl-1.1.1w/util/
openssl-1.1.1w/util/add-depends.pl
openssl-1.1.1w/util/build.info
openssl-1.1.1w/util/cavs-to-evptest.pl
openssl-1.1.1w/util/check-malloc-errs
openssl-1.1.1w/util/ck_errf.pl
openssl-1.1.1w/util/copy.pl
openssl-1.1.1w/util/dofile.pl
openssl-1.1.1w/util/echo.pl
openssl-1.1.1w/util/find-doc-nits
openssl-1.1.1w/util/find-unused-errs
openssl-1.1.1w/util/fix-includes
openssl-1.1.1w/util/fix-includes.sed
openssl-1.1.1w/util/indent.pro
openssl-1.1.1w/util/libcrypto.num
openssl-1.1.1w/util/libssl.num
openssl-1.1.1w/util/local_shlib.com.in
openssl-1.1.1w/util/mkbuildinf.pl
openssl-1.1.1w/util/mkdef.pl
openssl-1.1.1w/util/mkdir-p.pl
openssl-1.1.1w/util/mkerr.pl
openssl-1.1.1w/util/mkrc.pl
openssl-1.1.1w/util/openssl-format-source
openssl-1.1.1w/util/openssl-update-copyright
openssl-1.1.1w/util/opensslwrap.sh
openssl-1.1.1w/util/perl/
openssl-1.1.1w/util/perl/OpenSSL/
openssl-1.1.1w/util/perl/OpenSSL/Glob.pm
openssl-1.1.1w/util/perl/OpenSSL/Test.pm
openssl-1.1.1w/util/perl/OpenSSL/Test/
openssl-1.1.1w/util/perl/OpenSSL/Test/Simple.pm
openssl-1.1.1w/util/perl/OpenSSL/Test/Utils.pm
openssl-1.1.1w/util/perl/OpenSSL/Util/
openssl-1.1.1w/util/perl/OpenSSL/Util/Pod.pm
openssl-1.1.1w/util/perl/OpenSSL/copyright.pm
openssl-1.1.1w/util/perl/TLSProxy/
openssl-1.1.1w/util/perl/TLSProxy/Alert.pm
openssl-1.1.1w/util/perl/TLSProxy/Certificate.pm
openssl-1.1.1w/util/perl/TLSProxy/CertificateRequest.pm
openssl-1.1.1w/util/perl/TLSProxy/CertificateVerify.pm
openssl-1.1.1w/util/perl/TLSProxy/ClientHello.pm
openssl-1.1.1w/util/perl/TLSProxy/EncryptedExtensions.pm
openssl-1.1.1w/util/perl/TLSProxy/Message.pm
openssl-1.1.1w/util/perl/TLSProxy/NewSessionTicket.pm
openssl-1.1.1w/util/perl/TLSProxy/Proxy.pm
openssl-1.1.1w/util/perl/TLSProxy/Record.pm
openssl-1.1.1w/util/perl/TLSProxy/ServerHello.pm
openssl-1.1.1w/util/perl/TLSProxy/ServerKeyExchange.pm
openssl-1.1.1w/util/perl/checkhandshake.pm
openssl-1.1.1w/util/perl/with_fallback.pm
openssl-1.1.1w/util/private.num
openssl-1.1.1w/util/process_docs.pl
openssl-1.1.1w/util/shlib_wrap.sh.in
openssl-1.1.1w/util/su-filter.pl
openssl-1.1.1w/util/unlocal_shlib.com.in
openssl-1.1.1w/wycheproof/
```

Заранее поставим все зависимости, чтобы в процессе сборки не было ошибок:

```
[root@rpm ~]# yum-builddep rpmbuild/SPECS/nginx.spec
Failed to set locale, defaulting to C.UTF-8
CentOS Stream 8 - AppStream                                                                                                                                7.7 kB/s | 4.4 kB     00:00    
CentOS Stream 8 - BaseOS                                                                                                                                   7.2 kB/s | 3.9 kB     00:00    
CentOS Stream 8 - Extras                                                                                                                                   6.2 kB/s | 2.9 kB     00:00    
CentOS Stream 8 - Extras common packages                                                                                                                   4.7 kB/s | 3.0 kB     00:00    
Extra Packages for Enterprise Linux 8 - x86_64                                                                                                              36 kB/s |  29 kB     00:00    
Extra Packages for Enterprise Linux 8 - Next - x86_64                                                                                                       46 kB/s |  37 kB     00:00    
Package openssl-devel-1:1.1.1k-11.el8.x86_64 is already installed.
Package systemd-239-78.el8.x86_64 is already installed.
Package zlib-devel-1.2.11-25.el8.x86_64 is already installed.
Dependencies resolved.
===========================================================================================================================================================================================
 Package                                         Architecture                             Version                                           Repository                                Size
===========================================================================================================================================================================================
Installing:
 pcre-devel                                      x86_64                                   8.42-6.el8                                        baseos                                   551 k
Upgrading:
 openssl                                         x86_64                                   1:1.1.1k-12.el8                                   baseos                                   738 k
 openssl-devel                                   x86_64                                   1:1.1.1k-12.el8                                   baseos                                   3.2 M
 openssl-libs                                    x86_64                                   1:1.1.1k-12.el8                                   baseos                                   1.5 M
 systemd                                         x86_64                                   239-82.el8                                        baseos                                   3.8 M
 systemd-libs                                    x86_64                                   239-82.el8                                        baseos                                   1.1 M
 systemd-pam                                     x86_64                                   239-82.el8                                        baseos                                   512 k
 systemd-udev                                    x86_64                                   239-82.el8                                        baseos                                   1.6 M
Installing dependencies:
 pcre-cpp                                        x86_64                                   8.42-6.el8                                        baseos                                    47 k
 pcre-utf16                                      x86_64                                   8.42-6.el8                                        baseos                                   195 k
 pcre-utf32                                      x86_64                                   8.42-6.el8                                        baseos                                   186 k

Transaction Summary
===========================================================================================================================================================================================
Install  4 Packages
Upgrade  7 Packages

Total download size: 13 M
Is this ok [y/N]: y
Downloading Packages:
(1/11): pcre-cpp-8.42-6.el8.x86_64.rpm                                                                                                                     125 kB/s |  47 kB     00:00    
(2/11): pcre-utf16-8.42-6.el8.x86_64.rpm                                                                                                                   409 kB/s | 195 kB     00:00    
(3/11): pcre-devel-8.42-6.el8.x86_64.rpm                                                                                                                   1.0 MB/s | 551 kB     00:00    
(4/11): pcre-utf32-8.42-6.el8.x86_64.rpm                                                                                                                   1.0 MB/s | 186 kB     00:00    
(5/11): openssl-1.1.1k-12.el8.x86_64.rpm                                                                                                                   2.4 MB/s | 738 kB     00:00    
(6/11): openssl-devel-1.1.1k-12.el8.x86_64.rpm                                                                                                             4.8 MB/s | 3.2 MB     00:00    
(7/11): openssl-libs-1.1.1k-12.el8.x86_64.rpm                                                                                                              1.9 MB/s | 1.5 MB     00:00    
(8/11): systemd-libs-239-82.el8.x86_64.rpm                                                                                                                 4.0 MB/s | 1.1 MB     00:00    
(9/11): systemd-pam-239-82.el8.x86_64.rpm                                                                                                                  1.4 MB/s | 512 kB     00:00    
(10/11): systemd-udev-239-82.el8.x86_64.rpm                                                                                                                3.9 MB/s | 1.6 MB     00:00    
(11/11): systemd-239-82.el8.x86_64.rpm                                                                                                                     3.0 MB/s | 3.8 MB     00:01    
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                      5.5 MB/s |  13 MB     00:02     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                                   1/1 
  Running scriptlet: openssl-libs-1:1.1.1k-12.el8.x86_64                                                                                                                               1/1 
  Upgrading        : openssl-libs-1:1.1.1k-12.el8.x86_64                                                                                                                              1/18 
  Running scriptlet: openssl-libs-1:1.1.1k-12.el8.x86_64                                                                                                                              1/18 
  Upgrading        : systemd-libs-239-82.el8.x86_64                                                                                                                                   2/18 
  Running scriptlet: systemd-libs-239-82.el8.x86_64                                                                                                                                   2/18 
  Upgrading        : systemd-pam-239-82.el8.x86_64                                                                                                                                    3/18 
  Running scriptlet: systemd-239-82.el8.x86_64                                                                                                                                        4/18 
  Upgrading        : systemd-239-82.el8.x86_64                                                                                                                                        4/18 
  Running scriptlet: systemd-239-82.el8.x86_64                                                                                                                                        4/18 
  Installing       : pcre-utf32-8.42-6.el8.x86_64                                                                                                                                     5/18 
  Installing       : pcre-utf16-8.42-6.el8.x86_64                                                                                                                                     6/18 
  Installing       : pcre-cpp-8.42-6.el8.x86_64                                                                                                                                       7/18 
  Installing       : pcre-devel-8.42-6.el8.x86_64                                                                                                                                     8/18 
  Upgrading        : systemd-udev-239-82.el8.x86_64                                                                                                                                   9/18 
  Running scriptlet: systemd-udev-239-82.el8.x86_64                                                                                                                                   9/18 
  Upgrading        : openssl-1:1.1.1k-12.el8.x86_64                                                                                                                                  10/18 
  Upgrading        : openssl-devel-1:1.1.1k-12.el8.x86_64                                                                                                                            11/18 
  Cleanup          : openssl-1:1.1.1k-11.el8.x86_64                                                                                                                                  12/18 
  Cleanup          : openssl-devel-1:1.1.1k-11.el8.x86_64                                                                                                                            13/18 
  Cleanup          : systemd-udev-239-78.el8.x86_64                                                                                                                                  14/18 
  Running scriptlet: systemd-udev-239-78.el8.x86_64                                                                                                                                  14/18 
  Running scriptlet: systemd-239-78.el8.x86_64                                                                                                                                       15/18 
  Cleanup          : systemd-239-78.el8.x86_64                                                                                                                                       15/18 
  Cleanup          : openssl-libs-1:1.1.1k-11.el8.x86_64                                                                                                                             16/18 
  Running scriptlet: openssl-libs-1:1.1.1k-11.el8.x86_64                                                                                                                             16/18 
  Cleanup          : systemd-libs-239-78.el8.x86_64                                                                                                                                  17/18 
  Cleanup          : systemd-pam-239-78.el8.x86_64                                                                                                                                   18/18 
  Running scriptlet: systemd-pam-239-78.el8.x86_64                                                                                                                                   18/18 
  Running scriptlet: systemd-239-82.el8.x86_64                                                                                                                                       18/18 
  Running scriptlet: systemd-udev-239-82.el8.x86_64                                                                                                                                  18/18 
  Verifying        : pcre-cpp-8.42-6.el8.x86_64                                                                                                                                       1/18 
  Verifying        : pcre-devel-8.42-6.el8.x86_64                                                                                                                                     2/18 
  Verifying        : pcre-utf16-8.42-6.el8.x86_64                                                                                                                                     3/18 
  Verifying        : pcre-utf32-8.42-6.el8.x86_64                                                                                                                                     4/18 
  Verifying        : openssl-1:1.1.1k-12.el8.x86_64                                                                                                                                   5/18 
  Verifying        : openssl-1:1.1.1k-11.el8.x86_64                                                                                                                                   6/18 
  Verifying        : openssl-devel-1:1.1.1k-12.el8.x86_64                                                                                                                             7/18 
  Verifying        : openssl-devel-1:1.1.1k-11.el8.x86_64                                                                                                                             8/18 
  Verifying        : openssl-libs-1:1.1.1k-12.el8.x86_64                                                                                                                              9/18 
  Verifying        : openssl-libs-1:1.1.1k-11.el8.x86_64                                                                                                                             10/18 
  Verifying        : systemd-239-82.el8.x86_64                                                                                                                                       11/18 
  Verifying        : systemd-239-78.el8.x86_64                                                                                                                                       12/18 
  Verifying        : systemd-libs-239-82.el8.x86_64                                                                                                                                  13/18 
  Verifying        : systemd-libs-239-78.el8.x86_64                                                                                                                                  14/18 
  Verifying        : systemd-pam-239-82.el8.x86_64                                                                                                                                   15/18 
  Verifying        : systemd-pam-239-78.el8.x86_64                                                                                                                                   16/18 
  Verifying        : systemd-udev-239-82.el8.x86_64                                                                                                                                  17/18 
  Verifying        : systemd-udev-239-78.el8.x86_64                                                                                                                                  18/18 

Upgraded:
  openssl-1:1.1.1k-12.el8.x86_64      openssl-devel-1:1.1.1k-12.el8.x86_64      openssl-libs-1:1.1.1k-12.el8.x86_64      systemd-239-82.el8.x86_64      systemd-libs-239-82.el8.x86_64     
  systemd-pam-239-82.el8.x86_64       systemd-udev-239-82.el8.x86_64           
Installed:
  pcre-cpp-8.42-6.el8.x86_64                   pcre-devel-8.42-6.el8.x86_64                   pcre-utf16-8.42-6.el8.x86_64                   pcre-utf32-8.42-6.el8.x86_64                  

Complete!
```

Правим сам spec файл, чтобы NGINX собирался с необходимыми нам опциями:

```
#
%define nginx_home %{_localstatedir}/cache/nginx
%define nginx_user nginx
%define nginx_group nginx
%define nginx_loggroup adm

BuildRequires: systemd
Requires(post): systemd
Requires(preun): systemd
Requires(postun): systemd

%if 0%{?rhel}
%define _group System Environment/Daemons
%endif

%if (0%{?rhel} == 7) && (0%{?amzn} == 0)
%define epoch 1
Epoch: %{epoch}
Requires(pre): shadow-utils
Requires: openssl >= 1.0.2
BuildRequires: openssl-devel >= 1.0.2
%define dist .el7
%endif

%if (0%{?rhel} == 7) && (0%{?amzn} == 2)
%define epoch 1
Epoch: %{epoch}
Requires(pre): shadow-utils
Requires: openssl11 >= 1.1.1
BuildRequires: openssl11-devel >= 1.1.1
%endif

%if 0%{?rhel} == 8
%define epoch 1
Epoch: %{epoch}
Requires(pre): shadow-utils
BuildRequires: openssl-devel >= 1.1.1
%define _debugsource_template %{nil}
%endif

%if 0%{?suse_version} >= 1315
%define _group Productivity/Networking/Web/Servers
%define nginx_loggroup trusted
Requires(pre): shadow
BuildRequires: libopenssl-devel
%define _debugsource_template %{nil}
%endif

%if 0%{?fedora}
%define _debugsource_template %{nil}
%global _hardened_build 1
%define _group System Environment/Daemons
BuildRequires: openssl-devel
Requires(pre): shadow-utils
%endif

# end of distribution specific definitions

%define base_version 1.20.2
%define base_release 1%{?dist}.ngx

%define bdir %{_builddir}/%{name}-%{base_version}

%define WITH_CC_OPT $(echo %{optflags} $(pcre-config --cflags)) -fPIC
%define WITH_LD_OPT -Wl,-z,relro -Wl,-z,now -pie

%define BASE_CONFIGURE_ARGS $(echo "--prefix=%{_sysconfdir}/nginx --sbin-path=%{_sbindir}/nginx --modules-path=%{_libdir}/nginx/modules --conf-path=%{_sysconfdir}/nginx/nginx.conf --error-log-path=%{_localstatedir}/log/nginx/error.log --http-log-path=%{_localstatedir}/log/nginx/access.log --pid-path=%{_localstatedir}/run/nginx.pid --lock-path=%{_localstatedir}/run/nginx.lock --http-client-body-temp-path=%{_localstatedir}/cache/nginx/client_temp --http-proxy-temp-path=%{_localstatedir}/cache/nginx/proxy_temp --http-fastcgi-temp-path=%{_localstatedir}/cache/nginx/fastcgi_temp --http-uwsgi-temp-path=%{_localstatedir}/cache/nginx/uwsgi_temp --http-scgi-temp-path=%{_localstatedir}/cache/nginx/scgi_temp --user=%{nginx_user} --group=%{nginx_group} --with-compat --with-file-aio --with-threads --with-http_addition_module --with-http_auth_request_module --with-http_dav_module --with-http_flv_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_mp4_module --with-http_random_index_module --with-http_realip_module --with-http_secure_link_module --with-http_slice_module --with-http_ssl_module --with-http_stub_status_module --with-http_sub_module --with-http_v2_module --with-mail --with-mail_ssl_module --with-stream --with-stream_realip_module --with-stream_ssl_module --with-stream_ssl_preread_module")

Summary: High performance web server
Name: nginx
Version: %{base_version}
Release: %{base_release}
Vendor: NGINX Packaging <nginx-packaging@f5.com>
URL: https://nginx.org/
Group: %{_group}

Source0: https://nginx.org/download/%{name}-%{version}.tar.gz
Source1: logrotate
Source2: nginx.conf
Source3: nginx.default.conf
Source4: nginx.service
Source5: nginx.upgrade.sh
Source6: nginx.suse.logrotate
Source7: nginx-debug.service
Source8: nginx.copyright
Source9: nginx.check-reload.sh



License: 2-clause BSD-like license

BuildRoot: %{_tmppath}/%{name}-%{base_version}-%{base_release}-root
BuildRequires: zlib-devel
BuildRequires: pcre-devel

Provides: webserver
Provides: nginx-r%{base_version}

%description
nginx [engine x] is an HTTP and reverse proxy server, as well as
a mail proxy server.

%if 0%{?suse_version} >= 1315
%debug_package
%endif

%prep
%autosetup -p1

%build
./configure %{BASE_CONFIGURE_ARGS} \
    --with-cc-opt="%{WITH_CC_OPT}" \
    --with-ld-opt="%{WITH_LD_OPT}" \
    --with-openssl=/root/openssl-1.1.1w
make %{?_smp_mflags}
%{__mv} %{bdir}/objs/nginx \
    %{bdir}/objs/nginx-debug
./configure %{BASE_CONFIGURE_ARGS} \
    --with-cc-opt="%{WITH_CC_OPT}" \
    --with-ld-opt="%{WITH_LD_OPT}"
make %{?_smp_mflags}

%install
%{__rm} -rf $RPM_BUILD_ROOT
%{__make} DESTDIR=$RPM_BUILD_ROOT INSTALLDIRS=vendor install

%{__mkdir} -p $RPM_BUILD_ROOT%{_datadir}/nginx
%{__mv} $RPM_BUILD_ROOT%{_sysconfdir}/nginx/html $RPM_BUILD_ROOT%{_datadir}/nginx/

%{__rm} -f $RPM_BUILD_ROOT%{_sysconfdir}/nginx/*.default
%{__rm} -f $RPM_BUILD_ROOT%{_sysconfdir}/nginx/fastcgi.conf

%{__mkdir} -p $RPM_BUILD_ROOT%{_localstatedir}/log/nginx
%{__mkdir} -p $RPM_BUILD_ROOT%{_localstatedir}/run/nginx
%{__mkdir} -p $RPM_BUILD_ROOT%{_localstatedir}/cache/nginx

%{__mkdir} -p $RPM_BUILD_ROOT%{_libdir}/nginx/modules
cd $RPM_BUILD_ROOT%{_sysconfdir}/nginx && \
    %{__ln_s} ../..%{_libdir}/nginx/modules modules && cd -

%{__mkdir} -p $RPM_BUILD_ROOT%{_datadir}/doc/%{name}-%{base_version}
%{__install} -m 644 -p %{SOURCE8} \
    $RPM_BUILD_ROOT%{_datadir}/doc/%{name}-%{base_version}/COPYRIGHT

%{__mkdir} -p $RPM_BUILD_ROOT%{_sysconfdir}/nginx/conf.d
%{__rm} $RPM_BUILD_ROOT%{_sysconfdir}/nginx/nginx.conf
%{__install} -m 644 -p %{SOURCE2} \
    $RPM_BUILD_ROOT%{_sysconfdir}/nginx/nginx.conf
%{__install} -m 644 -p %{SOURCE3} \
    $RPM_BUILD_ROOT%{_sysconfdir}/nginx/conf.d/default.conf

%{__install} -p -D -m 0644 %{bdir}/objs/nginx.8 \
    $RPM_BUILD_ROOT%{_mandir}/man8/nginx.8

%{__mkdir} -p $RPM_BUILD_ROOT%{_unitdir}
%{__install} -m644 %SOURCE4 \
    $RPM_BUILD_ROOT%{_unitdir}/nginx.service
%{__install} -m644 %SOURCE7 \
    $RPM_BUILD_ROOT%{_unitdir}/nginx-debug.service
%{__mkdir} -p $RPM_BUILD_ROOT%{_libexecdir}/initscripts/legacy-actions/nginx
%{__install} -m755 %SOURCE5 \
    $RPM_BUILD_ROOT%{_libexecdir}/initscripts/legacy-actions/nginx/upgrade
%{__install} -m755 %SOURCE9 \
    $RPM_BUILD_ROOT%{_libexecdir}/initscripts/legacy-actions/nginx/check-reload

# install log rotation stuff
%{__mkdir} -p $RPM_BUILD_ROOT%{_sysconfdir}/logrotate.d
%if 0%{?suse_version}
%{__install} -m 644 -p %{SOURCE6} \
    $RPM_BUILD_ROOT%{_sysconfdir}/logrotate.d/nginx
%else
%{__install} -m 644 -p %{SOURCE1} \
    $RPM_BUILD_ROOT%{_sysconfdir}/logrotate.d/nginx
%endif

%{__install} -m755 %{bdir}/objs/nginx-debug \
    $RPM_BUILD_ROOT%{_sbindir}/nginx-debug

%{__rm} $RPM_BUILD_ROOT%{_sysconfdir}/nginx/koi-utf
%{__rm} $RPM_BUILD_ROOT%{_sysconfdir}/nginx/koi-win
%{__rm} $RPM_BUILD_ROOT%{_sysconfdir}/nginx/win-utf

%check
%{__rm} -rf $RPM_BUILD_ROOT/usr/src
cd %{bdir}
grep -v 'usr/src' debugfiles.list > debugfiles.list.new && mv debugfiles.list.new debugfiles.list
cat /dev/null > debugsources.list
%if 0%{?suse_version} >= 1500
cat /dev/null > debugsourcefiles.list
%endif

%clean
%{__rm} -rf $RPM_BUILD_ROOT

%files
%defattr(-,root,root)

%{_sbindir}/nginx
%{_sbindir}/nginx-debug

%dir %{_sysconfdir}/nginx
%dir %{_sysconfdir}/nginx/conf.d
%{_sysconfdir}/nginx/modules

%config(noreplace) %{_sysconfdir}/nginx/nginx.conf
%config(noreplace) %{_sysconfdir}/nginx/conf.d/default.conf
%config(noreplace) %{_sysconfdir}/nginx/mime.types
%config(noreplace) %{_sysconfdir}/nginx/fastcgi_params
%config(noreplace) %{_sysconfdir}/nginx/scgi_params
%config(noreplace) %{_sysconfdir}/nginx/uwsgi_params

%config(noreplace) %{_sysconfdir}/logrotate.d/nginx
%{_unitdir}/nginx.service
%{_unitdir}/nginx-debug.service
%dir %{_libexecdir}/initscripts/legacy-actions/nginx
%{_libexecdir}/initscripts/legacy-actions/nginx/*

%attr(0755,root,root) %dir %{_libdir}/nginx
%attr(0755,root,root) %dir %{_libdir}/nginx/modules
%dir %{_datadir}/nginx
%dir %{_datadir}/nginx/html
%{_datadir}/nginx/html/*

%attr(0755,root,root) %dir %{_localstatedir}/cache/nginx
%attr(0755,root,root) %dir %{_localstatedir}/log/nginx

%dir %{_datadir}/doc/%{name}-%{base_version}
%doc %{_datadir}/doc/%{name}-%{base_version}/COPYRIGHT
%{_mandir}/man8/nginx.8*

%pre
# Add the "nginx" user
getent group %{nginx_group} >/dev/null || groupadd -r %{nginx_group}
getent passwd %{nginx_user} >/dev/null || \
    useradd -r -g %{nginx_group} -s /sbin/nologin \
    -d %{nginx_home} -c "nginx user"  %{nginx_user}
exit 0

%post
# Register the nginx service
if [ $1 -eq 1 ]; then
    /usr/bin/systemctl preset nginx.service >/dev/null 2>&1 ||:
    /usr/bin/systemctl preset nginx-debug.service >/dev/null 2>&1 ||:
    # print site info
    cat <<BANNER
----------------------------------------------------------------------

Thanks for using nginx!

Please find the official documentation for nginx here:
* https://nginx.org/en/docs/

Please subscribe to nginx-announce mailing list to get
the most important news about nginx:
* https://nginx.org/en/support.html

Commercial subscriptions for nginx are available on:
* https://nginx.com/products/

----------------------------------------------------------------------
BANNER

    # Touch and set permisions on default log files on installation

    if [ -d %{_localstatedir}/log/nginx ]; then
        if [ ! -e %{_localstatedir}/log/nginx/access.log ]; then
            touch %{_localstatedir}/log/nginx/access.log
            %{__chmod} 640 %{_localstatedir}/log/nginx/access.log
            %{__chown} nginx:%{nginx_loggroup} %{_localstatedir}/log/nginx/access.log
        fi

        if [ ! -e %{_localstatedir}/log/nginx/error.log ]; then
            touch %{_localstatedir}/log/nginx/error.log
            %{__chmod} 640 %{_localstatedir}/log/nginx/error.log
            %{__chown} nginx:%{nginx_loggroup} %{_localstatedir}/log/nginx/error.log
        fi
    fi
fi

%preun
if [ $1 -eq 0 ]; then
    /usr/bin/systemctl --no-reload disable nginx.service >/dev/null 2>&1 ||:
    /usr/bin/systemctl stop nginx.service >/dev/null 2>&1 ||:
fi

%postun
/usr/bin/systemctl daemon-reload >/dev/null 2>&1 ||:
if [ $1 -ge 1 ]; then
    /sbin/service nginx status  >/dev/null 2>&1 || exit 0
    /sbin/service nginx upgrade >/dev/null 2>&1 || echo \
        "Binary upgrade failed, please check nginx's error.log"
fi

%changelog
* Tue Nov 16 2021 Konstantin Pavlov <thresh@nginx.com> - 1.20.2-1%{?dist}.ngx
- 1.20.2-1

* Tue May 25 2021 Konstantin Pavlov <thresh@nginx.com> - 1.20.1-1%{?dist}.ngx
- 1.20.1-1

* Tue Apr 20 2021 Konstantin Pavlov <thresh@nginx.com> - 1.20.0-1%{?dist}.ngx
- 1.20.0-1
- Changed the default number of worker processes to auto
- Changed the default error log level to notice
- Dropped charset-related data from packages and default configuration

* Tue Apr 13 2021 Andrei Belov <defan@nginx.com> - 1.19.10-1%{?dist}.ngx
- 1.19.10-1

* Tue Mar 30 2021 Konstantin Pavlov <thresh@nginx.com> - 1.19.9-1%{?dist}.ngx
- 1.19.9-1

* Tue Mar  9 2021 Konstantin Pavlov <thresh@nginx.com> - 1.19.8-1%{?dist}.ngx
- 1.19.8-1

* Tue Feb 16 2021 Konstantin Pavlov <thresh@nginx.com> - 1.19.7-1%{?dist}.ngx
- 1.19.7-1

* Tue Dec 15 2020 Konstantin Pavlov <thresh@nginx.com> - 1.19.6-1%{?dist}.ngx
- 1.19.6-1

* Tue Nov 24 2020 Konstantin Pavlov <thresh@nginx.com> - 1.19.5-1%{?dist}.ngx
- 1.19.5-1

* Tue Oct 27 2020 Andrei Belov <defan@nginx.com> - 1.19.4-1%{?dist}.ngx
- 1.19.4-1

* Tue Sep 29 2020 Konstantin Pavlov <thresh@nginx.com> - 1.19.3-1%{?dist}.ngx
- 1.19.3

* Tue Aug 11 2020 Konstantin Pavlov <thresh@nginx.com> - 1.19.2-1%{?dist}.ngx
- 1.19.2

* Tue Jul  7 2020 Konstantin Pavlov <thresh@nginx.com> - 1.19.1-1%{?dist}.ngx
- 1.19.1

* Tue May 26 2020 Konstantin Pavlov <thresh@nginx.com> - 1.19.0-1%{?dist}.ngx
- 1.19.0

* Tue Apr 14 2020 Konstantin Pavlov <thresh@nginx.com> - 1.17.10-1%{?dist}.ngx
- 1.17.10

* Tue Mar  3 2020 Konstantin Pavlov <thresh@nginx.com> - 1.17.9-1%{?dist}.ngx
- 1.17.9

* Tue Jan 21 2020 Konstantin Pavlov <thresh@nginx.com> - 1.17.8-1%{?dist}.ngx
- 1.17.8

* Tue Dec 24 2019 Konstantin Pavlov <thresh@nginx.com> - 1.17.7-1%{?dist}.ngx
- 1.17.7

* Tue Nov 19 2019 Konstantin Pavlov <thresh@nginx.com> - 1.17.6-1%{?dist}.ngx
- 1.17.6

* Tue Oct 22 2019 Andrei Belov <defan@nginx.com> - 1.17.5-1%{?dist}.ngx
- 1.17.5

* Tue Sep 24 2019 Konstantin Pavlov <thresh@nginx.com> - 1.17.4-1%{?dist}.ngx
- 1.17.4

* Tue Aug 13 2019 Andrei Belov <defan@nginx.com> - 1.17.3-1%{?dist}.ngx
- 1.17.3

* Tue Jul 23 2019 Konstantin Pavlov <thresh@nginx.com> - 1.17.2-1%{?dist}.ngx
- 1.17.2

* Tue Jun 25 2019 Andrei Belov <defan@nginx.com> - 1.17.1-1%{?dist}.ngx
- 1.17.1

* Tue May 21 2019 Konstantin Pavlov <thresh@nginx.com> - 1.17.0-1%{?dist}.ngx
- 1.17.0

* Tue Apr 16 2019 Konstantin Pavlov <thresh@nginx.com> - 1.15.12-1%{?dist}.ngx
- 1.15.12

* Tue Apr  9 2019 Konstantin Pavlov <thresh@nginx.com> - 1.15.11-1%{?dist}.ngx
- 1.15.11

* Tue Mar 26 2019 Konstantin Pavlov <thresh@nginx.com> - 1.15.10-1%{?dist}.ngx
- 1.15.10

* Tue Feb 26 2019 Konstantin Pavlov <thresh@nginx.com> - 1.15.9-1%{?dist}.ngx
- 1.15.9

* Tue Dec 25 2018 Konstantin Pavlov <thresh@nginx.com> - 1.15.8-1%{?dist}.ngx
- 1.15.8

* Tue Nov 27 2018 Konstantin Pavlov <thresh@nginx.com> - 1.15.7-1%{?dist}.ngx
- 1.15.7

* Tue Nov  6 2018 Konstantin Pavlov <thresh@nginx.com> - 1.15.6-1%{?dist}.ngx
- 1.15.6
- Security: fixes CVE-2018-16843.
- Security: fixes CVE-2018-16844.
- Security: fixes CVE-2018-16845.

* Tue Oct  2 2018 Konstantin Pavlov <thresh@nginx.com> - 1.15.5-1%{?dist}.ngx
- 1.15.5

* Tue Sep 25 2018 Konstantin Pavlov <thresh@nginx.com> - 1.15.4-1%{?dist}.ngx
- 1.15.4

* Tue Aug 28 2018 Konstantin Pavlov <thresh@nginx.com> - 1.15.3-1%{?dist}.ngx
- 1.15.3

* Tue Jul 24 2018 Konstantin Pavlov <thresh@nginx.com> - 1.15.2-1%{?dist}.ngx
- 1.15.2

* Tue Jul  3 2018 Konstantin Pavlov <thresh@nginx.com> - 1.15.1-1%{?dist}.ngx
- 1.15.1

* Tue Jun  5 2018 Konstantin Pavlov <thresh@nginx.com> - 1.15.0-1%{?dist}.ngx
- 1.15.0

* Mon Apr  9 2018 Konstantin Pavlov <thresh@nginx.com> - 1.13.12-1%{?dist}.ngx
- 1.13.12

* Tue Apr  3 2018 Konstantin Pavlov <thresh@nginx.com> - 1.13.11-1%{?dist}.ngx
- 1.13.11

* Tue Mar 20 2018 Konstantin Pavlov <thresh@nginx.com> - 1.13.10-1%{?dist}.ngx
- 1.13.10

* Tue Feb 20 2018 Konstantin Pavlov <thresh@nginx.com> - 1.13.9-1%{?dist}.ngx
- 1.13.9

* Tue Dec 26 2017 Konstantin Pavlov <thresh@nginx.com> - 1.13.8-1%{?dist}.ngx
- 1.13.8

* Tue Nov 21 2017 Konstantin Pavlov <thresh@nginx.com> - 1.13.7-1%{?dist}.ngx
- 1.13.7

* Thu Sep 14 2017 Konstantin Pavlov <thresh@nginx.com> - 1.13.6-1%{?dist}.ngx
- 1.13.6
- Bugfix: in systemd service support
  (https://trac.nginx.org/nginx/ticket/1380).

* Thu Sep 14 2017 Konstantin Pavlov <thresh@nginx.com> - 1.13.5-1%{?dist}.ngx
- 1.13.5

* Tue Aug  8 2017 Sergey Budnevitch <sb@nginx.com> - 1.13.4-1%{?dist}.ngx
- 1.13.4

* Tue Jul 11 2017 Konstantin Pavlov <thresh@nginx.com> - 1.13.3-1%{?dist}.ngx
- 1.13.3
- Security: fixes CVE-2017-7529.

* Tue Jun 27 2017 Konstantin Pavlov <thresh@nginx.com> - 1.13.2-1%{?dist}.ngx
- 1.13.2

* Tue May 30 2017 Konstantin Pavlov <thresh@nginx.com> - 1.13.1-1%{?dist}.ngx
- 1.13.1

* Tue Apr 25 2017 Konstantin Pavlov <thresh@nginx.com> - 1.13.0-1%{?dist}.ngx
- 1.13.0

* Tue Apr  4 2017 Konstantin Pavlov <thresh@nginx.com> - 1.11.13-1%{?dist}.ngx
- 1.11.13
- Made upgrade loops/timeouts configurable via /etc/defaults/nginx.

* Fri Mar 24 2017 Konstantin Pavlov <thresh@nginx.com> - 1.11.12-1%{?dist}.ngx
- 1.11.12

* Tue Mar 21 2017 Konstantin Pavlov <thresh@nginx.com> - 1.11.11-1%{?dist}.ngx
- 1.11.11

* Tue Feb 14 2017 Konstantin Pavlov <thresh@nginx.com> - 1.11.10-1%{?dist}.ngx
- 1.11.10

* Tue Jan 24 2017 Konstantin Pavlov <thresh@nginx.com> - 1.11.9-1%{?dist}.ngx
- 1.11.9
- Extended hardening build flags.
- Added check-reload target to init script / systemd service.

* Tue Dec 27 2016 Konstantin Pavlov <thresh@nginx.com> - 1.11.8-1%{?dist}.ngx
- 1.11.8

* Tue Dec 13 2016 Konstantin Pavlov <thresh@nginx.com> - 1.11.7-1%{?dist}.ngx
- 1.11.7

* Fri Nov 25 2016 Konstantin Pavlov <thresh@nginx.com> - 1.11.6-1%{?dist}.ngx
- 1.11.6

* Mon Oct 10 2016 Andrei Belov <defan@nginx.com> - 1.11.5-1%{?dist}.ngx
- 1.11.5

* Tue Sep 13 2016 Konstantin Pavlov <thresh@nginx.com> - 1.11.4-1%{?dist}.ngx
- 1.11.4
- njs updated to 0.1.2.

* Tue Jul 26 2016 Konstantin Pavlov <thresh@nginx.com> - 1.11.3-1%{?dist}.ngx
- 1.11.3
- njs updated to 0.1.0.
- njs stream dynamic module added to nginx-module-njs package.
- geoip stream dynamic module added to nginx-module-geoip package.

* Tue Jul  5 2016 Konstantin Pavlov <thresh@nginx.com> - 1.11.2-1%{?dist}.ngx
- 1.11.2
- njs updated to ef2b708510b1.

* Tue May 31 2016 Konstantin Pavlov <thresh@nginx.com> - 1.11.1-1%{?dist}.ngx
- 1.11.1

* Tue May 24 2016 Sergey Budnevitch <sb@nginx.com> - 1.11.0-1%{?dist}.ngx
- 1.11.0
- Bugfix: fixed logrotate error if nginx is not running.

* Tue Apr 19 2016 Konstantin Pavlov <thresh@nginx.com> - 1.9.15-1%{?dist}.ngx
- 1.9.15
- njs updated to 1c50334fbea6.

* Tue Apr  5 2016 Konstantin Pavlov <thresh@nginx.com> - 1.9.14-1%{?dist}.ngx
- 1.9.14

* Tue Mar 29 2016 Konstantin Pavlov <thresh@nginx.com> - 1.9.13-1%{?dist}.ngx
- 1.9.13
- Fixed modules path
- Added perl and njs dynamic modules subpackages

* Wed Feb 24 2016 Sergey Budnevitch <sb@nginx.com> - 1.9.12-1%{?dist}.ngx
- 1.9.12
- common configure args are now in variable
- xslt, image-filter and geoip dynamic modules added

* Tue Feb  9 2016 Sergey Budnevitch <sb@nginx.com> - 1.9.11-1%{?dist}.ngx
- 1.9.11
- dynamic modules path and symlink in /etc/nginx added

* Tue Jan 26 2016 Konstantin Pavlov <thresh@nginx.com> - 1.9.10-1%{?dist}.ngx
- 1.9.10

* Wed Dec  9 2015 Konstantin Pavlov <thresh@nginx.com> - 1.9.9-1%{?dist}.ngx
- 1.9.9

* Tue Dec  8 2015 Konstantin Pavlov <thresh@nginx.com> - 1.9.8-1%{?dist}.ngx
- 1.9.8
- http_slice module enabled

* Tue Nov 17 2015 Konstantin Pavlov <thresh@nginx.com> - 1.9.7-1%{?dist}.ngx
- 1.9.7

* Tue Oct 27 2015 Sergey Budnevitch <sb@nginx.com> - 1.9.6-1%{?dist}.ngx
- 1.9.6

* Tue Sep 22 2015 Andrei Belov <defan@nginx.com> - 1.9.5-1%{?dist}.ngx
- 1.9.5
- http_spdy module replaced with http_v2 module

* Tue Aug 18 2015 Konstantin Pavlov <thresh@nginx.com> - 1.9.4-1%{?dist}.ngx
- 1.9.4

* Tue Jul 14 2015 Sergey Budnevitch <sb@nginx.com> - 1.9.3-1%{?dist}.ngx
- 1.9.3

* Tue Jun 16 2015 Sergey Budnevitch <sb@nginx.com> - 1.9.2-1%{?dist}.ngx
- 1.9.2

* Tue May 26 2015 Sergey Budnevitch <sb@nginx.com> - 1.9.1-1%{?dist}.ngx
- 1.9.1

* Tue Apr 28 2015 Sergey Budnevitch <sb@nginx.com> - 1.9.0-1%{?dist}.ngx
- 1.9.0
- thread pool support added
- stream module added
- example_ssl.conf removed

* Tue Apr  7 2015 Sergey Budnevitch <sb@nginx.com> - 1.7.12-1%{?dist}.ngx
- 1.7.12

* Tue Mar 24 2015 Sergey Budnevitch <sb@nginx.com> - 1.7.11-1%{?dist}.ngx
- 1.7.11

* Tue Feb 10 2015 Sergey Budnevitch <sb@nginx.com> - 1.7.10-1%{?dist}.ngx
- 1.7.10

* Tue Dec 23 2014 Sergey Budnevitch <sb@nginx.com> - 1.7.9-1%{?dist}.ngx
- 1.7.9
- init-script now sends signal only to the PID derived from pidfile

* Tue Dec  2 2014 Sergey Budnevitch <sb@nginx.com> - 1.7.8-1%{?dist}.ngx
- 1.7.8
- package with debug symbols added

* Tue Oct 28 2014 Sergey Budnevitch <sb@nginx.com> - 1.7.7-1%{?dist}.ngx
- 1.7.7

* Tue Sep 30 2014 Sergey Budnevitch <sb@nginx.com> - 1.7.6-1%{?dist}.ngx
- 1.7.6

* Tue Sep 16 2014 Sergey Budnevitch <sb@nginx.com> - 1.7.5-1%{?dist}.ngx
- 1.7.5

* Tue Aug  5 2014 Sergey Budnevitch <sb@nginx.com> - 1.7.4-1%{?dist}.ngx
- 1.7.4
- init-script now returns 0 on stop command if nginx is not running

* Tue Jul  8 2014 Sergey Budnevitch <sb@nginx.com> - 1.7.3-1%{?dist}.ngx
- 1.7.3

* Tue Jun 17 2014 Sergey Budnevitch <sb@nginx.com> - 1.7.2-1%{?dist}.ngx
- 1.7.2

* Tue May 27 2014 Sergey Budnevitch <sb@nginx.com> - 1.7.1-1%{?dist}.ngx
- 1.7.1

* Thu Apr 24 2014 Konstantin Pavlov <thresh@nginx.com> - 1.7.0-1%{?dist}.ngx
- 1.7.0

* Tue Apr  8 2014 Sergey Budnevitch <sb@nginx.com> - 1.5.13-1%{?dist}.ngx
- 1.5.13

* Tue Mar 18 2014 Sergey Budnevitch <sb@nginx.com> - 1.5.12-1%{?dist}.ngx
- 1.5.12
- warning added when binary upgrade returns non-zero exit code

* Tue Mar  4 2014 Sergey Budnevitch <sb@nginx.com> - 1.5.11-1%{?dist}.ngx
- 1.5.11

* Tue Feb  4 2014 Sergey Budnevitch <sb@nginx.com> - 1.5.10-1%{?dist}.ngx
- 1.5.10

* Wed Jan 22 2014 Sergey Budnevitch <sb@nginx.com> - 1.5.9-1%{?dist}.ngx
- 1.5.9

* Tue Dec 17 2013 Sergey Budnevitch <sb@nginx.com> - 1.5.8-1%{?dist}.ngx
- 1.5.8

* Fri Nov 29 2013 Sergey Budnevitch <sb@nginx.com> - 1.5.7-1%{?dist}.ngx
- 1.5.7
- init script now honours additional options sourced from /etc/default/nginx

* Tue Oct  1 2013 Sergey Budnevitch <sb@nginx.com> - 1.5.6-1%{?dist}.ngx
- 1.5.6

* Tue Sep 17 2013 Andrei Belov <defan@nginx.com> - 1.5.5-1%{?dist}.ngx
- 1.5.5

* Tue Aug 27 2013 Sergey Budnevitch <sb@nginx.com> - 1.5.4-1%{?dist}.ngx
- 1.5.4
- auth request module added

* Tue Jul 30 2013 Sergey Budnevitch <sb@nginx.com> - 1.5.3-1%{?dist}.ngx
- 1.5.3

* Tue Jul  2 2013 Sergey Budnevitch <sb@nginx.com> - 1.5.2-1%{?dist}.ngx
- 1.5.2

* Tue Jun  4 2013 Sergey Budnevitch <sb@nginx.com> - 1.5.1-1%{?dist}.ngx
- 1.5.1
- dpkg-buildflags options now passed by --with-{cc,ld}-opt

* Mon May  6 2013 Sergey Budnevitch <sb@nginx.com> - 1.5.0-1%{?dist}.ngx
- 1.5.0
- fixed openssl version detection with dash as /bin/sh

* Tue Apr 16 2013 Sergey Budnevitch <sb@nginx.com> - 1.3.16-1%{?dist}.ngx
- 1.3.16

* Tue Mar 26 2013 Sergey Budnevitch <sb@nginx.com> - 1.3.15-1%{?dist}.ngx
- 1.3.15
- gunzip module added
- spdy module added if openssl version >= 1.0.1
- set permissions on default log files at installation
```

Приступаем к сборке RPM пакета:

```
[root@rpm ~]# rpmbuild -bb rpmbuild/SPECS/nginx.spec
Executing(%prep): /bin/sh -e /var/tmp/rpm-tmp.y0srQK
+ umask 022
+ cd /root/rpmbuild/BUILD
+ cd /root/rpmbuild/BUILD
+ rm -rf nginx-1.20.2
+ /usr/bin/gzip -dc /root/rpmbuild/SOURCES/nginx-1.20.2.tar.gz
+ /usr/bin/tar -xof -
+ STATUS=0
+ '[' 0 -ne 0 ']'
+ cd nginx-1.20.2
+ /usr/bin/chmod -Rf a+rX,u+w,g-w,o-w .
+ exit 0
Executing(%build): /bin/sh -e /var/tmp/rpm-tmp.boRpn1
+ umask 022
+ cd /root/rpmbuild/BUILD
+ cd nginx-1.20.2
...
...
Checking for unpackaged file(s): /usr/lib/rpm/check-files /root/rpmbuild/BUILDROOT/nginx-1.20.2-1.el8.ngx.x86_64
Wrote: /root/rpmbuild/RPMS/x86_64/nginx-1.20.2-1.el8.ngx.x86_64.rpm
Wrote: /root/rpmbuild/RPMS/x86_64/nginx-debuginfo-1.20.2-1.el8.ngx.x86_64.rpm
Executing(%clean): /bin/sh -e /var/tmp/rpm-tmp.Vf2TiL
+ umask 022
+ cd /root/rpmbuild/BUILD
+ cd nginx-1.20.2
+ /usr/bin/rm -rf /root/rpmbuild/BUILDROOT/nginx-1.20.2-1.el8.ngx.x86_64
+ exit 0
```

Убедимся, что пакеты создались:

```
[root@rpm ~]# ll rpmbuild/RPMS/x86_64/
total 4456
-rw-r--r--. 1 root root 2060628 Apr 15 13:35 nginx-1.20.2-1.el8.ngx.x86_64.rpm
-rw-r--r--. 1 root root 2495864 Apr 15 13:35 nginx-debuginfo-1.20.2-1.el8.ngx.x86_64.rpm
```

Устанавливаем созданный пакет и проверяем, что nginx работает:

```
[root@rpm ~]# yum localinstall -y \
> rpmbuild/RPMS/x86_64/nginx-1.20.2-1.el8.ngx.x86_64.rpm
Failed to set locale, defaulting to C.UTF-8
CentOS Stream 8 - AppStream                                                                                                                                6.5 kB/s | 4.4 kB     00:00    
CentOS Stream 8 - BaseOS                                                                                                                                   6.2 kB/s | 3.9 kB     00:00    
CentOS Stream 8 - Extras                                                                                                                                   6.6 kB/s | 2.9 kB     00:00    
CentOS Stream 8 - Extras common packages                                                                                                                   6.3 kB/s | 3.0 kB     00:00    
Extra Packages for Enterprise Linux 8 - x86_64                                                                                                              39 kB/s |  35 kB     00:00    
Extra Packages for Enterprise Linux 8 - Next - x86_64                                                                                                       44 kB/s |  37 kB     00:00    
Dependencies resolved.
===========================================================================================================================================================================================
 Package                                Architecture                            Version                                                Repository                                     Size
===========================================================================================================================================================================================
Installing:
 nginx                                  x86_64                                  1:1.20.2-1.el8.ngx                                     @commandline                                  2.0 M

Transaction Summary
===========================================================================================================================================================================================
Install  1 Package

Total size: 2.0 M
Installed size: 5.9 M
Downloading Packages:
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                                   1/1 
  Running scriptlet: nginx-1:1.20.2-1.el8.ngx.x86_64                                                                                                                                   1/1 
  Installing       : nginx-1:1.20.2-1.el8.ngx.x86_64                                                                                                                                   1/1 
  Running scriptlet: nginx-1:1.20.2-1.el8.ngx.x86_64                                                                                                                                   1/1 
----------------------------------------------------------------------

Thanks for using nginx!

Please find the official documentation for nginx here:
* https://nginx.org/en/docs/

Please subscribe to nginx-announce mailing list to get
the most important news about nginx:
* https://nginx.org/en/support.html

Commercial subscriptions for nginx are available on:
* https://nginx.com/products/

----------------------------------------------------------------------

  Verifying        : nginx-1:1.20.2-1.el8.ngx.x86_64                                                                                                                                   1/1 

Installed:
  nginx-1:1.20.2-1.el8.ngx.x86_64                                                                                                                                                          

Complete!
```

```
[root@rpm ~]# systemctl start nginx
```

```
[root@rpm ~]# systemctl status nginx
● nginx.service - nginx - high performance web server
   Loaded: loaded (/usr/lib/systemd/system/nginx.service; disabled; vendor preset: disabled)
   Active: active (running) since Mon 2024-04-15 15:53:49 UTC; 40s ago
     Docs: http://nginx.org/en/docs/
  Process: 2452 ExecStart=/usr/sbin/nginx -c /etc/nginx/nginx.conf (code=exited, status=0/SUCCESS)
 Main PID: 2453 (nginx)
    Tasks: 3 (limit: 4694)
   Memory: 2.9M
   CGroup: /system.slice/nginx.service
           ├─2453 nginx: master process /usr/sbin/nginx -c /etc/nginx/nginx.conf
           ├─2454 nginx: worker process
           └─2455 nginx: worker process

Apr 15 15:53:49 rpm systemd[1]: Starting nginx - high performance web server...
Apr 15 15:53:49 rpm systemd[1]: Started nginx - high performance web server.
```

### **Создать свой репозиторий и разместить там ранее собранный RPM** ###

Создадим каталог repo в `/usr/share/nginx/html`:

```
[root@rpm ~]# mkdir /usr/share/nginx/html/repo
```

Копируем туда собранный RPM и, например, RPM для установки репозитория Percona-Server:

```
[root@rpm ~]# cp rpmbuild/RPMS/x86_64/nginx-1.20.2-1.el8.ngx.x86_64.rpm /usr/share/nginx/html/repo/
```

```
[root@rpm ~]# wget https://downloads.percona.com/downloads/percona-distribution-mysql-ps/percona-distribution-mysql-ps-8.0.28/binary/redhat/8/x86_64/percona-orchestrator-3.2.6-2.el8.x86_64.rpm -O /usr/share/nginx/html/repo/percona-orchestrator-3.2.6-2.el8.x86_64.rpm
--2024-04-15 16:15:15--  https://downloads.percona.com/downloads/percona-distribution-mysql-ps/percona-distribution-mysql-ps-8.0.28/binary/redhat/8/x86_64/percona-orchestrator-3.2.6-2.el8.x86_64.rpm
Resolving downloads.percona.com (downloads.percona.com)... 49.12.125.205, 2a01:4f8:242:5792::2
Connecting to downloads.percona.com (downloads.percona.com)|49.12.125.205|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 5222976 (5.0M) [application/x-redhat-package-manager]
Saving to: '/usr/share/nginx/html/repo/percona-orchestrator-3.2.6-2.el8.x86_64.rpm'

/usr/share/nginx/html/repo/percona-orchestrato 100%[===================================================================================================>]   4.98M  7.42MB/s    in 0.7s    

2024-04-15 16:15:16 (7.42 MB/s) - '/usr/share/nginx/html/repo/percona-orchestrator-3.2.6-2.el8.x86_64.rpm' saved [5222976/5222976]
```

Инициализируем репозиторий командой:

```
[root@rpm ~]# createrepo /usr/share/nginx/html/repo/
Directory walk started
Directory walk done - 2 packages
Temporary output repo path: /usr/share/nginx/html/repo/.repodata/
Preparing sqlite DBs
Pool started (with 5 workers)
Pool finished
```

Настроим в NGINX доступ к листингу каталога. В файле /etc/nginx/conf.d/default.conf добавим директиву autoindex on.

Проверяем синтаксис и перезапускаем NGINX:

```
[root@rpm ~]# nginx -t
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

```
[root@rpm ~]# nginx -s reload
```
Проверим репозиторий:

```
[root@rpm ~]# curl -a http://localhost/repo/
<html>
<head><title>Index of /repo/</title></head>
<body>
<h1>Index of /repo/</h1><hr><pre><a href="../">../</a>
<a href="repodata/">repodata/</a>                                          15-Apr-2024 16:17                   -
<a href="nginx-1.20.2-1.el8.ngx.x86_64.rpm">nginx-1.20.2-1.el8.ngx.x86_64.rpm</a>                  15-Apr-2024 16:09             2060628
<a href="percona-orchestrator-3.2.6-2.el8.x86_64.rpm">percona-orchestrator-3.2.6-2.el8.x86_64.rpm</a>        16-Feb-2022 15:57             5222976
</pre><hr></body>
</html>
```

Добавим его в /etc/yum.repos.d:

```
[root@rpm repo]# cat >> /etc/yum.repos.d/otus.repo << EOF
> [otus]
> name=otus-linux
> baseurl=http://localhost/repo
> gpgcheck=0
> enabled=1
> EOF
```

Убедимся, что репозиторий подключился и посмотрим, что в нем есть:

```
[root@rpm repo]# yum repolist enabled | grep otus
Failed to set locale, defaulting to C.UTF-8
otus                otus-linux
```

```
[root@rpm x86_64]# yum list | grep otus
Failed to set locale, defaulting to C.UTF-8
otus-linux                                      2.9 MB/s | 3.0 kB     00:00    
otus-linux                                       37 kB/s | 2.8 kB     00:00    
percona-orchestrator.x86_64                                       2:3.2.6-2.el8                                                     @otus     
nginx.x86_64                                                     2:1.20.2-1.el8                                                     @otus
```

Так как NGINX у нас уже стоит, установим репозиторий percona-release:

```
[root@rpm repo]# yum install percona-orchestrator.x86_64 -y
Failed to set locale, defaulting to C.UTF-8
Last metadata expiration check: 0:01:15 ago on Thu Apr 18 14:51:20 2024.
Dependencies resolved.
============================================================================================================================================================================================
 Package                                              Architecture                           Version                                        Repository                                 Size
============================================================================================================================================================================================
Installing:
 percona-orchestrator                                 x86_64                                 2:3.2.6-2.el8                                  otus                                      5.0 M
Installing dependencies:
 jq                                                   x86_64                                 1.6-8.el8                                      appstream                                 203 k
 oniguruma                                            x86_64                                 6.8.2-3.el8                                    appstream                                 188 k

Transaction Summary
============================================================================================================================================================================================
Install  3 Packages

Total download size: 5.4 M
Installed size: 17 M
Downloading Packages:
(1/3): percona-orchestrator-3.2.6-2.el8.x86_64.rpm                                                                                                           60 MB/s | 5.0 MB     00:00    
(2/3): oniguruma-6.8.2-3.el8.x86_64.rpm                                                                                                                     452 kB/s | 188 kB     00:00    
(3/3): jq-1.6-8.el8.x86_64.rpm                                                                                                                              482 kB/s | 203 kB     00:00    
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                       7.6 MB/s | 5.4 MB     00:00     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                                                                    1/1 
  Installing       : oniguruma-6.8.2-3.el8.x86_64                                                                                                                                       1/3 
  Running scriptlet: oniguruma-6.8.2-3.el8.x86_64                                                                                                                                       1/3 
  Installing       : jq-1.6-8.el8.x86_64                                                                                                                                                2/3 
  Installing       : percona-orchestrator-2:3.2.6-2.el8.x86_64                                                                                                                          3/3 
  Running scriptlet: percona-orchestrator-2:3.2.6-2.el8.x86_64                                                                                                                          3/3 
  Verifying        : jq-1.6-8.el8.x86_64                                                                                                                                                1/3 
  Verifying        : oniguruma-6.8.2-3.el8.x86_64                                                                                                                                       2/3 
  Verifying        : percona-orchestrator-2:3.2.6-2.el8.x86_64                                                                                                                          3/3 

Installed:
  jq-1.6-8.el8.x86_64                                 oniguruma-6.8.2-3.el8.x86_64                                 percona-orchestrator-2:3.2.6-2.el8.x86_64                                

Complete!
```
