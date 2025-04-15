# BUILD KERNEL
#
#
### CLONE KERNEL
```sh
git clone git@gitlab.com:xanmod/linux.git --branch=6.18 xanmod-6.18 && cd xanmod-6.18
```

### PATCH KERNEL
- **Lenovo-b490**
	```sh
	git am Patch/Lenovo-B490/xanmod-6.18.patch
	```

### EXTERNAL DRIVER
- **V4L2LOOPBACK**
	```sh
	git clone https://github.com/v4l2loopback/v4l2loopback.git drivers/media/v4l2-core/v4l2loopback
	```

### INSTALL DEPENDENCIES
```sh
Scripts/kernel_package_install
```

### COMPILE
```sh
Scripts/kernel_compile
```

### INSTALL MODULES
```sh
Scripts/kernel_modules_install
```

### INSTALL KERNEL
```sh
Scripts/kernel_install
```

### SIGNED KERNEL FOR SECUREBOOT
- **ENV**
	```sh
	CERT_DIR=<CERTIFICATE_DIR>
	```

- **Make Cert**
	```sh
	mkdir -p $CERT_DIR
	openssl req -nodes -new -x509 -newkey rsa:2048 -keyout $CERT_DIR/MOK.priv -outform DER -out $CERT_DIR/MOK.der -days 36500 -subj "/CN=$(cat /sys/class/dmi/id/product_version)/"
	openssl x509 -inform der -in $CERT_DIR/MOK.der -out $CERT_DIR/MOK.pem
	```

- **Enrollin Key**
	```sh
	apt install --no-install-suggests --no-install-recommends mokutil
	mokutil --import $CERT_DIR/MOK.der
	```

- **Sign Kernel**
	```sh
	Scripts/kernel_signed $CERT_DIR /boot/vmlinuz-$(uname -r)
	```