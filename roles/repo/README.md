# Repo (ansible role)

This role will bootstrap a local yum repo and download rpm packages

Tasks:

```yaml
tasks:
  repo : Create local repo directory	    TAGS: [init-meta, repo_precheck]
  repo : Check pigsty repo cache exists	    TAGS: [init-meta, repo_precheck]
  repo : Check pigsty boot cache exists	    TAGS: [init-meta, repo_precheck]
  repo : Enable default centos yum repos	TAGS: [init-meta, repo_bootstrap]
  repo : Install official centos yum repos	TAGS: [init-meta, repo_bootstrap]
  repo : Install additional nginx yum repo	TAGS: [init-meta, repo_bootstrap]
  repo : Download bootstrap packages	    TAGS: [init-meta, repo_bootstrap]
  repo : Bootstrap packages downloaded	    TAGS: [init-meta, repo_bootstrap]
  repo : Install bootstrap packages (nginx)	TAGS: [init-meta, repo_nginx]
  repo : Copy default nginx server config	TAGS: [init-meta, repo_nginx]
  repo : Copy default nginx index page	    TAGS: [init-meta, repo_nginx]
  repo : Copy nginx pigsty repo files	    TAGS: [init-meta, repo_nginx]
  repo : Start nginx service to serve repo	TAGS: [init-meta, repo_nginx]
  repo : Waits yum repo nginx online	    TAGS: [init-meta, repo_nginx]
  repo : Install default centos yum repos	TAGS: [init-meta, repo_download]
  repo : Enable default centos yum repos	TAGS: [init-meta, repo_download]
  repo : Install additional yum repos	    TAGS: [init-meta, repo_download]
  repo : Enlist building packages to repo	TAGS: [init-meta, repo_download]
  repo : Enlist addional packages to repo	TAGS: [init-meta, repo_download]
  repo : Print packages to be downloaded	TAGS: [init-meta, repo_download]
  repo : Download packages to /www/pigsty	TAGS: [init-meta, repo_download]
  repo : Download additional url packages	TAGS: [init-meta, repo_download]
  repo : Download cloud native packages	    TAGS: [init-meta, repo_download]
  repo : Create local yum repo index	    TAGS: [init-meta, repo_download]
  repo : Mark local yum repo complete	    TAGS: [init-meta, repo_download]
  repo : Install local yum repos on meta	TAGS: [init-meta, repo_install]
```

Related variables:

```yaml
################################################################
# Meta repo variable: how to build local yum repo
################################################################
# how to download
repo_force_download:   false     # force download even cache exists
repo_proxy_env: {}               # add proxy environment variable here

repo_package_list:
  # postgres core packages
  - postgresql13*
  - postgresql12*
  - postgis30_12*

  # postgres extension packages 12
  - wal2json12,pg_repack12,pg_qualstats12,pg_stat_kcache12,pgrouting_12,pg_cron_12,timescaledb_12,pglogical_12,pgpool-II-12
  # postgres common misc
  - pgbouncer,pgadmin4,pg_top,pgbadger,pgdg-redhat-repo
  # ansible and python environment
  - ansible,python,python-pip,python-ipython,python-psycopg2
  # system utils
  - ntp,uuid,readline,lz4,nc,pv,jq,vim,make,patch,bash,libxml2,libxslt,lsof,wget,unzip,git,numactl,grubby,zlib,openssl,perl-ExtUtils-Embed
  # network utils
  - bind-utils,net-tools,sysstat,tcpdump,socat,ipvsadm
  # monitoring packages
  - grafana,prometheus2,pushgateway,alertmanager,node_exporter,postgres_exporter,nginx_exporter,blackbox_exporter
  # dcs packages
  - consul,consul_exporter,consul-template,etcd
  # proxy and dns
  - nginx,haproxy,keepalived,dnsmasq

# download necessary url packages
repo_url_package_list:
  - name: pg_exporter-0.2.0-1.el7.x86_64.rpm
    url: https://github.com/Vonng/pg_exporter/releases/download/v0.2.0/pg_exporter-0.2.0-1.el7.x86_64.rpm
  - name: patroni-1.6.5-1.rhel7.x86_64.rpm
    url: https://github.com/cybertec-postgresql/patroni-packaging/releases/download/1.6.5-1/patroni-1.6.5-1.rhel7.x86_64.rpm
  - name: vip-manager_0.6-1_amd64.rpm
    url: https://github.com/cybertec-postgresql/vip-manager/releases/download/v0.6/vip-manager_0.6-1_amd64.rpm

#==============================================================#
# additional packages
#==============================================================#
# additional packages to be downloaded
repo_additional_package_list: []

# download cloud native packages: kubectl kubeadm helm docker, etc..
repo_cloud_native: true
repo_cloud_native_package_list:
  - docker-ce,docker-ce-cli,docker-ce-selinux,cri-tools,kubeadm,kubectl,kubelet,kubernetes-cni,rkt,helm

# download build essential packages: gcc, g++, rpmbuild, etc...
repo_build_essential: true
repo_build_essential_package_list:
  - gcc,gcc-c++,clang,coreutils,diffutils,rpm-build,rpm-devel,rpmlint,rpmdevtools
  - zlib-devel,openssl-libs,openssl-devel,pam-devel,libxml2-devel,libxslt-devel,openldap-devel,systemd-devel,tcl-devel,python-devel

```