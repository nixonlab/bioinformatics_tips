# Working on remote compute clusters

## SSH through proxy

WCM and other cluster infrastructures use ["gateway nodes"](https://wcmscu.atlassian.net/wiki/spaces/WIKI/pages/753692/Gateway+Nodes) to control access to the cluster. Instead of connecting to a gateway node, then connecting to a submit host from that gateway node, you can use "SSH ProxyJump" to jump directly to the submit node.

![Proxy Jump](https://i0.wp.com/oooops.dev/wp-content/uploads/2021/02/image-5.png?resize=720%2C330&ssl=1)

For example, instead of this:

```bash
[name@localmachine ~]$ ssh <login_name>@pascal.med.cornell.edu
Last login: Wed Oct  5 13:06:34 2022 from XXX.XXX.XXX.XXX
[login_name@pascal ~]$ ssh curie.pbtech
Last login: Wed Oct  5 13:09:10 2022 from 10.0.0.19
```

you can jump directly to `curie.pbtech` by tunneling through `pascal.med.cornell.edu`:

```bash
ssh -l usr4001 -i ~/.ssh/id_ecdsa -J usr4001@pascal.med.cornell.edu curie.pbtech
```

*Replace `usr4001` with your login name, and `~/.ssh/id_ecdsa` with an identity file you have set up in your authorized keys*


General format for the SSH ProxyJump:

```bash
ssh -l <login_name> -i <identity_file> -J <jump_host> <destination>
```

