# 12. Networking and SSH

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Pipes, redirection, and text processing](./11-pipes-redirection-and-text-processing.md) | [Notes index](../README.md) | [Next: Storage, filesystems, and mounts](./13-storage-filesystems-and-mounts.md) |

## Basic network checks

A network connection involves more than one step: the local interface needs an address, a route must lead to the destination, and name resolution must map a host name to an address.

Inspect local interfaces and routes:

~~~sh
ip address
ip route
hostname
~~~

The loopback interface lets a computer communicate with itself. The address <code>127.0.0.1</code> is a common IPv4 loopback address.

Check whether the system can resolve a host name:

~~~sh
getent hosts example.com
~~~

Test basic reachability with <code>ping</code>:

~~~sh
ping -c 4 example.com
~~~

A failed ping does not prove that a web service is down. A network or firewall may block ICMP while allowing other traffic.

## Check ports and services

A port identifies a service endpoint on a host. View listening TCP sockets with:

~~~sh
ss -ltn
~~~

Add <code>-p</code> to request process details. Some details may require elevated access:

~~~sh
sudo ss -ltnp
~~~

The local address shown by a listening socket matters. A service bound to loopback accepts connections only from the same host. A service bound to a network interface may accept remote connections, subject to firewall rules.

## Check an HTTP endpoint

Use <code>curl</code> to request a web resource:

~~~sh
curl -I https://example.com
curl -fsS https://example.com -o /dev/null
~~~

The first command asks for response headers. The second fetches the response while hiding the body. An HTTP status code describes the server's response, while DNS, routing, TLS, and firewall problems can prevent any HTTP response from arriving.

## Connect with SSH

SSH provides encrypted remote shell access. Connect with an account name and host:

~~~sh
ssh ashish@example.com
~~~

The first connection may ask you to verify the server's host key. Check the fingerprint through a trusted channel before accepting it. The saved host key helps SSH detect an unexpected server identity later.

Generate an Ed25519 key pair on your own computer:

~~~sh
ssh-keygen -t ed25519 -C "ashish@laptop"
~~~

The private key stays on your computer. Protect it with a passphrase and never send it to another person. Only the public key, whose filename ends in <code>.pub</code>, is installed on the remote account. On systems with <code>ssh-copy-id</code>, this command can install it:

~~~sh
ssh-copy-id ashish@example.com
~~~

If a connection fails, check the host name, network route, server availability, account name, and SSH service status. Verbose SSH output can help diagnose a connection, but review it before sharing because it may reveal account names and host details.

## Practice questions

1. Which command displays local IP addresses?
2. What does <code>ip route</code> show?
3. Why can a failed ping occur while a web service is available?
4. What does <code>ss -ltn</code> list?
5. What does it mean for a service to listen on loopback?
6. Which command checks HTTP response headers?
7. Which SSH key should remain private?
8. Why should a server host key be verified?

## References

- [OpenSSH manual pages](https://www.openssh.com/manual.html)
- [Linux manual page for ssh](https://man7.org/linux/man-pages/man1/ssh.1.html)
- [Linux manual page for ip](https://man7.org/linux/man-pages/man8/ip.8.html)
- [Linux manual page for ss](https://man7.org/linux/man-pages/man8/ss.8.html)
- [Ubuntu networking documentation](https://ubuntu.com/server/docs/networking/)