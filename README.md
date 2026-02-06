# 4640-in-class-wk5

## Team

- Misha Makaroff
- Angad Bains


## Visiting Our NGINX Instance

![Alt text for the image](lab5-proof.png)

![Alt text for the image](lab5-proof2.png)

## Steps Taken

1. We defined the image source in a build block
```
build {
  name = "web-nginx"
  sources = [
    # COMPLETE ME Use the source defined above
    "sources.amazon-ebs.debian"
  ]
```

2. We used a shell provisioner to run commands to create folders and set permissions on them
```
  provisioner "shell" {
    inline = [
      "echo creating directories",
      # COMPLETE ME add inline scripts to create necessary directories and change directory ownership.
      # See nginx.conf file for root directory where files will be served.
      # Files need appropriate ownership for default user
      "sudo mkdir -p /web/html /tmp/web",
      "sudo chown admin /web/html /tmp/web"
    ]
  }

```
3. We used two file provisioners to upload our NGINX configuration and website index files.
```
  provisioner "file" {
    # COMPLETE ME add the HTML file to your image
    source      = "files/index.html"
    destination = "/web/html/index.html"
  }
```
```
  provisioner "file" {
    # COMPLETE ME add the nginx.conf file to your image
    source      = "files/nginx.conf"
    destination = "/tmp/web/nginx.conf"
  }
```
4. We used a shell provisioner to specify the two scripts to upload and run (NGINX installation and configuration scripts)
```
  provisioner "shell" {
    scripts = [
      "scripts/install-nginx",
      "scripts/setup-nginx"
    ]
```
