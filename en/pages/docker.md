# Docker Containerization

## Tips and Tricks

### Nice Docker Stats Filter

[Github](https://github.com/moby/moby/issues/20973)

thaJeztah commented on May 17

@mjaggard open the file ```~/.docker/config.json``` in an editor, and modify it to look like this (where "other-option-1" and "other-option-2" are existing configuration options you may have in that file);

```
{
  "other-option-1":"foo",
  "other-option-2":"bar",
  "statsFormat": "table {{.Name}}\t{{.CPUPerc}}\t{{.MemUsage}}\t{{.MemPerc}}\t{{.NetIO}}\t{{.BlockIO}}\t{{.PIDs}}"
}
```

After that, Names will be used by default. You can add/remove other columns by changing the template, valid options can be found here:

[https://docs.docker.com/engine/reference/commandline/stats/#formatting](https://docs.docker.com/engine/reference/commandline/stats/#formatting)

### Enabling Docker Remote API on Ubuntu

I tried to find instructions on how to enable the Docker remote API when running Docker in Ubuntu 16.04, but none of the instructions I came across managed to take me all the way, so here are a few short notes on how I managed to accomplish this:

* Edit the file ```/lib/systemd/system/docker.service```, I used the vi editor:

```sudo vi /lib/systemd/system/docker.service```

* Modify the line that starts with ExecStart to look like this:

```ExecStart=/usr/bin/docker daemon -H fd:// -H tcp://0.0.0.0:4243```

Where my addition is the “-H tcp://0.0.0.0:4243” part.

* Save the modified file.
* Make sure the Docker service notices the modified configuration:

```systemctl daemon-reload```

* Restart the Docker service:

```sudo service docker restart```

* Test that the Docker API is indeed accessible:

```curl http://localhost:4243/version```

* You should see output similar to this as the result:

```{"Version":"1.11.0","ApiVersion":"1.23","GitCommit":"4dc5990","GoVersion":"go1.5.4","Os":"linux","Arch":"amd64","KernelVersion":"4.4.0-22-generic","BuildTime":"2016-04-13T18:38:59.968579007+00:00"}```

* To access the Docker API from another computer, use the IP address of the Ubuntu computer found at either wlan0 or eth0, depending on whether you use wifi or ethernet network connection. To learn the IP addresses of the different interfaces, use the ifconfig command in a terminal window. In my case it is 192.168.1.68.