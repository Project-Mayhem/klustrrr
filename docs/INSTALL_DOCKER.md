# Docker Installation

```bash
# Install Docker
yum install -y docker-engine

# Move default files (if they exist, and you're scared...)
mv /usr/lib/systemd/system/docker.service /usr/lib/systemd/system/docker.service.org
mv /usr/lib/systemd/system/docker.socket /usr/lib/systemd/system/docker.socket.org
mv /etc/sysconfig/docker /etc/sysconfig/docker.org

# Copy in configuration files for docker bootstrap instance
cp ${klustrrr-root}/usr/lib/systemd/system/docker-bootstrap.service \
  /usr/lib/systemd/system/docker-bootstrap.service
cp ${klustrrr-root}/usr/lib/systemd/system/docker-bootstrap.socket \
  /usr/lib/systemd/system/docker-bootstrap.socket
chmod 644 /usr/lib/systemd/system/docker-bootstrap.service
chmod 644 /usr/lib/systemd/system/docker-bootstrap.socket
cp ${klustrrr-root}/etc/sysconfig/docker-bootstrap \
  /etc/sysconfig/docker-bootstrap
chmod 644 /etc/sysconfig/docker-bootstrap
mkdir -p /etc/systemd/system/docker-bootstrap.service.d
cp ${klustrrr-root}/etc/systemd/system/docker-bootstrap.service.d/custom-environment-file.conf \
  /etc/systemd/system/docker-bootstrap.service.d/custom-environment-file.conf
chmod 644 /etc/systemd/system/docker-bootstrap.service.d/custom-environment-file.conf
systemctl enable docker-bootstrap.socket
systemctl enable docker-bootstrap
systemctl start docker-bootstrap

# Copy in configuration files for default docker instance
cp ${klustrrr-root}/usr/lib/systemd/system/docker.service \
  /usr/lib/systemd/system/docker.service
cp ${klustrrr-root}/usr/lib/systemd/system/docker.socket \
  /usr/lib/systemd/system/docker.socket
chmod 644 /usr/lib/systemd/system/docker.service
chmod 644 /usr/lib/systemd/system/docker.socket
cp ${klustrrr-root}/etc/sysconfig/docker /etc/sysconfig/docker
chmod 644 /etc/sysconfig/docker
mkdir -p /etc/systemd/system/docker.service.d
cp ${klustrrr-root}/etc/systemd/system/docker.service.d/custom-environment-file.conf \
  /etc/systemd/system/docker.service.d/custom-environment-file.conf
chmod 644 /etc/systemd/system/docker.service.d/custom-environment-file.conf

# Mods for flannel
to be continued...
```
