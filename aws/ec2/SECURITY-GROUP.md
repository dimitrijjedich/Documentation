# AWS EC2 Security Groups

You can create a security group and add rules that reflect the role of the instance that's associated with the security group. For example, an instance that's configured as a web server needs security group rules that allow inbound HTTP and HTTPS access. Likewise, a database instance needs rules that allow access for the type of database, such as access over port 3306 for MySQL.

## Create a Security Group
A security group acts as a virtual firewall for your instance to control inbound and outbound traffic. The command to create a Security Group is:
```bash
aws ec2 create-security-group \
	--description <descript> \
	--group-name <name>
```
The output will look like this:
```JSON
{
    "GroupId": "sg-0d34c2349b7812821"
}
```
The created Security group will allow all Outbound traffic and have no allow inbound traffic as default.

### Add rules to Security Group
Adds the specified inbound (ingress) rules to a security group.
An inbound rule permits instances to receive traffic from the specified IPv4 or IPv6 address range, the IP address ranges that are specified by a prefix list, or the instances that are associated with a destination security group.

You must specify exactly one of the following sources: an IPv4 or IPv6 address range, a prefix list, or a security group. You must specify a protocol for each rule (for example, TCP). If the protocol is TCP or UDP, you must also specify a port or port range. If the protocol is ICMP or ICMPv6, you must also specify the ICMP/ICMPv6 type and code.

```bash
aws ec2 authorize-security-group-ingress \
	--group-id <value> \
	--protocol <tcp/udp> \
	--port <value> \
	--cidr <value>
```
`--group-id` as provided in the output on creation
`--protocol` the protocol for the rule (tcp or udp)
`--port` the port the rule ist for (80 for http, 3306 for MySQL and so on)
`--cidr` the IP the rule is for (0.0.0.0/0 for all IPv4 and ::/0 for all IPv6 adresses)
