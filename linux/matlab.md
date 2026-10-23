---
layout: page
title: MATLAB on Linux
---

#### 1. Install

```
sudo mpm install --release=R2026b --destination=/usr/local/MATLAB/R2026b MATLAB
```
<br>

#### 2. Small fix

<https://archive.archlinux.org/packages/g/gnutls/gnutls-3.8.9-1-x86_64.pkg.tar.zst>

```
mkdir -p /tmp/gnutls_extract
tar -I zstd -xvf ~/Downloads/gnutls-3.8.9-1-x86_64.pkg.tar.zst -C /tmp/gnutls_extract
```

```
sudo cp -d /tmp/gnutls_extract/usr/lib/libgnutls.so* /usr/local/MATLAB/R2026b/sys/os/glnxa64/
```

`rm -rf /tmp/gnutls_extract`
<br><br>

#### 3. Activate

```
ls /usr/lib/libleancrypto* 
sudo ln -s /usr/lib/libleancrypto.so.1.9 /usr/lib/libleancrypto.so.1
```

`sudo /usr/local/MATLAB/R2026b/bin/glnxa64/MathWorksProductAuthorizer.sh`
<br><br>

#### 4. Run

`/usr/local/MATLAB/R2026b/bin/matlab`
<br><br>

#### 5. Icon

`sudo nano /usr/share/applications/matlab.desktop`

```
[Desktop Entry]
Type=Application
Terminal=false
MimeType=text/x-matlab
Name=MATLAB R2026b
Exec=/usr/local/MATLAB/R2026b/bin/matlab -desktop -useStartupFolderPref
Icon=/usr/local/MATLAB/R2026b/ui/webgui/src/favicon.ico
```
