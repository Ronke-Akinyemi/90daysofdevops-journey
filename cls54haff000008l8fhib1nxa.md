---
title: "Grafana Setup"
datePublished: Fri Feb 02 2024 20:53:27 GMT+0000 (Coordinated Universal Time)
cuid: cls54haff000008l8fhib1nxa
slug: grafana-setup
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1706906999876/a0272de1-efa5-4cc1-b73a-6962fb4580a2.png
tags: aws, devops, grafana, 90daysofdevops

---

# Setting up Grafana in your local environment on AWS EC2

* Launch an EC2 instance:
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706903237184/6fee1761-0aca-456e-9996-32d829852060.png align="center")

* Connect to your EC2 instance through SSH
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706903361921/165700db-5678-427c-b29b-2e41ab2e6d38.png align="center")

* Update your package list
    

```basic
sudo apt-get update
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706905181505/fc253db3-b86c-4244-9ef3-b5b0e451dab5.png align="center")

* Install software-properties-common
    

```basic
sudo apt-get install -y software-properties-common
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706905598128/00f8fcde-0144-43b5-94b9-b46ed976322e.png align="center")

* Download the GPG keys and add them to the trusted keys list.
    

```basic
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add 
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706905615540/8d56be12-8118-425e-a2c8-dede3d68ea70.png align="center")

* Add it to the Grafana repository.
    

```basic
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706905645481/9b71ed99-d8eb-41a4-85f0-921492f83076.png align="center")

* Then, update and install grafana
    

```basic
sudo apt-get update
sudo apt-get install grafana
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706905669849/8aaa5b7c-cdf6-45e0-9332-1bfab9a7cf77.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706905690547/787f39d2-e591-42ce-aedf-017d92b03eb3.png align="center")

* After installation, enable and start grafana
    

```basic
sudo systemctl enable grafana-server
sudo systemctl start grafana-server 
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706905718274/0b794036-caf9-45e3-84b6-1cb72068817f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706905734832/59752375-a00f-407e-80b7-1e07f54db5b9.png align="center")

* Check whether grafana is running
    

```basic
sudo systemctl status grafana-server
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706905757583/07e3d095-4f62-4723-a4c3-f83be8ec9c2c.png align="center")

* Configure your security group to allow the inbound rule on port 3000 to access Grafana directly.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706905774003/660bb77f-9f5a-4f37-a1d6-5f6c4cf5cb3d.png align="center")

* Navigate to the public url of the EC2 instance, "public URL:3000"
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706905906603/48f7a27b-58a1-493f-9bce-6510d32a9c3b.png align="center")

The default login credentials are `admin` for both the username and password. Upon first login, you will be prompted to change the password.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1706906057834/bbcc6cb6-0e97-4160-b72f-79c13ae932d5.png align="center")

Thank you.