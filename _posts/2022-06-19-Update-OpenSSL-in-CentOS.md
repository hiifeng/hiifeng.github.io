---
layout: post
title: "CentOS 7 升级 OpenSSL 1.1.1"
author: "ifeng"
header-style: text
tags:
  - CentOS
  - OpenSSL
---

> 这篇文章转载自 [HiFeng'Blog](https://www.hicairo.com/post/50.html),转载请保留链接 ;)

CentOS7 自带的是 OpenSSL 1.0.2 ，某些软件需要更高的版本 OpenSSL ，因此就有了这篇文章。为考虑到系统兼容性，建议不覆盖原来的版本，而采用安装到 /usr/local/openssl111 的路径。

本文安装后不对系统做任何兼容性的破坏，增加的文件和目录如下：

```shell
/usr/local/openssl111/
/etc/ld.so.conf.d/openssl111.conf
```

编译后的 RPM 包名为 openssl111 ，也不影响系统自带的 openssl 1.0.2 的后续升级。

从官网进行下载。

```shell
####  以下所有操作都是在普通用户下进行，不能使用 root 
cd ~
wget -c https://www.openssl.org/source/openssl-1.1.1k.tar.gz

mkdir -p ~/rpmbuild/{SOURCES,SPECS,SRPMS}
cp openssl-1.1.1k.tar.gz  ~/rpmbuild/SOURCES
tar zxf ~/rpmbuild/SOURCES/openssl-1.1.1k.tar.gz -C ~/rpmbuild/SOURCES

# SPEC file
cat << 'EOF' > ~/rpmbuild/SPECS/openssl.spec
%global src  openssl
Summary: OpenSSL 1.1.1 for Centos
Name: openssl111
Version: %{?version}%{!?version:1.1.1k}
Release: 2%{?dist}
Epoch: 1
Obsoletes: %{name} <= %{epoch}:%{version}
Provides: %{name} = %{epoch}:%{version}
URL: https://www.openssl.org/
License: GPLv2+

Source: https://www.openssl.org/source/%{src}-%{version}.tar.gz

BuildRequires: make gcc perl perl-WWW-Curl
BuildRoot: %{_tmppath}/%{name}-%{epoch}:%{version}-%{release}-root
%global openssldir /usr/local/openssl111

%description
OpenSSL RPM for version 1.1.1 on CentOS

%package devel
Summary: Development files for programs which will use the openssl library
Group: Development/Libraries
Requires: %{name} = %{epoch}:%{version}-%{release}

%description devel
OpenSSL RPM for version 1.1.1 on CentOS (development package)

%prep
%setup -q -n %{src}-%{version}

%build
./config shared --prefix=%{openssldir} --openssldir=%{openssldir} -Wl,-rpath,%{openssldir}/lib
make clean
make -j8

%install
[ "%{buildroot}" != "/" ] && %{__rm} -rf %{buildroot}
%make_install

mkdir -p %{buildroot}%{_bindir}
mkdir -p %{buildroot}%{_libdir}
#ln -sf %{openssldir}/lib/libssl.so.1.1 %{buildroot}%{_libdir}
#ln -sf %{openssldir}/lib/libcrypto.so.1.1 %{buildroot}%{_libdir}
#ln -sf %{openssldir}/bin/openssl %{buildroot}%{_bindir}

%clean
[ "%{buildroot}" != "/" ] && %{__rm} -rf %{buildroot}

%files
%{openssldir}
%defattr(-,root,root)
#/usr/bin/openssl
#/usr/lib64/libcrypto.so.1.1
#/usr/lib64/libssl.so.1.1

%files devel
%{openssldir}/include/*
%defattr(-,root,root)

#%post -p /sbin/ldconfig
%post
  echo /usr/local/openssl111/lib | tee /etc/ld.so.conf.d/openssl111.conf
  /sbin/ldconfig
%postun -p /sbin/ldconfig

EOF

rpmbuild -ba ~/rpmbuild/SPECS/openssl.spec

sudo yum install ~/rpmbuild/RPMS/x86_64/openssl111-1.1.1k-1.el7.x86_64.rpm
```

另外，也可以直接从 EPEL 仓库下载 openssl 1.1.1 libs ，这样就不用以上的编译步骤了。

```shell
yum install openssl11-libs
```
