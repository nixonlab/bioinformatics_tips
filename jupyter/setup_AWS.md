# Running jupyter on remote server (AWS EC2)

### 0. _Setup_  - Create a conda environment with `jupyterlab`

```bash
mamba create -c conda-forge -n jupyterlab\
  jupyterlab\
  nb_conda_kernels\
  jupyter_contrib_nbextensions\
  nodejs\
  pip
```

### 1. Start jupyterlab server

Recommend running server in its own session using terminal multiplexer (i.e. tmux, screen, etc.)

```bash
conda activate jupyterlab

jupyter-lab --no-browser --port 8889
```

**IMPORTANT** Make sure no one else is using the same port number. You can do something like this:

```bash
jlport=6${UID}
jupyter-lab --no-browser --port $jlport
```

Once the server starts up, you should see a message like this:

```
    To access the server, open this file in a browser:
        file:///efs/users/bendall/.local/share/jupyter/runtime/jpserver-22683-open.html
    Or copy and paste one of these URLs:
        http://localhost:8889/lab?token=6a518403688c076f27f0598a57f724df7004314853b8b547
        http://127.0.0.1:8889/lab?token=6a518403688c076f27f0598a57f724df7004314853b8b547
```



### 2. Open SSH tunnel (_local machine_)

Open SSH tunnel to connect your computer (`localhost`) to remote server.

![Example of SSH tunnel](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*uGLPZIeLPkvvaRkVG1-tkw.png)

The general format of the tunnel command looks like this:

```bash
ssh [user@]remote_hostname -NL local_port:local_hostname:remote_port
```

+ `[user@]remote_hostname` is the remote machine hostname or IP address. This is the same as when you open an SSH shell session to the remote machine, so if you typically include `user@` or an identity file (`-i ~/.ssh/id_rsa`), than include these here.
+ `-NL local_port:local_host:remote_port` – The local port on the local host is being forwarded to the remote port of the remote server.

A practical example 

```bash
ssh ec2-XX-XX-XX-XX.compute-1.amazonaws.com -NL 8888:localhost:8889
```

This connects to an EC2 instance whose hostname is `ec2-XX-XX-XX-XX.compute-1.amazonaws.com` and creates a tunnel between port `8888` on your local machine and `8889` on the remote server.


### 3. Open jupyterlab in browser (_local machine_)

Open a new browser window and cut and paste the URL provided by the server. If the local port is not the same as your remote port, you will need to replace the remote port in the URL with the correct local port. For example, if you started jupyterlab on port 8889 (`--port 8889` in step 1) and created a tunnel between remote port 8889 and local port 8888 (`8888:localhost:8889` in step 2) then your URL should look like this:

```bash
http://localhost:8888/lab?token=6a518403688c076f27f0598a57f724df7004314853b8b547
```





