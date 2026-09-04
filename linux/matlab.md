---
layout: page
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
tar -I zstd -xvf ~/Downloads/gnutls-3.8.9-1-x86_64.pkg.tar.zst -C /tmp/gnutls_extract
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
<br><br>

#### 5. Icon

```
[Desktop Entry]
Type=Application
Terminal=false
MimeType=text/x-matlab
Name=MATLAB R2026a
Exec=/usr/local/MATLAB/R2026a/bin/matlab -desktop -useStartupFolderPref
Icon=/usr/local/MATLAB/R2026a/ui/webgui/src/favicon.ico
```
