---
layout: page
comments: true
title: MATLAB on Linux
---

#### 1. Install

```
sudo mpm install --release=R2026a --destination=/usr/local/MATLAB/R2026a MATLAB
```
<br>

#### 2. Small fix

<https://archive.archlinux.org/packages/g/gnutls/gnutls-3.8.9-1-x86_64.pkg.tar.zst>

```
mkdir -p /tmp/gnutls_extract
tar -I zstd -xvf ~/gnutls-3.8.9-1-x86_64.pkg.tar.zst -C /tmp/gnutls_extract
```

```
sudo cp -d /tmp/gnutls_extract/usr/lib/libgnutls.so* /usr/local/MATLAB/R2026a/sys/os/glnxa64/
```

`rm -rf /tmp/gnutls_extract`
<br><br>

#### 3. Activate

`sudo /usr/local/MATLAB/R2026a/bin/glnxa64/MathWorksProductAuthorizer`
<br><br>

#### 4. Run

`/usr/local/MATLAB/R2026a/bin/matlab`
