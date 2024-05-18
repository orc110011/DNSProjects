# DNSDIG

<h2>Description</h2>
The purpose of this project is to use dig to see the structure of the DNS hierarchy.

<h2>Languages and Utilities Used</h2>
- <b>DOS</b>
- <b>VMWARE Workstation Pro </b>

<h2>Environments Used </h2>

- <b> WINDOWS Server 2022 </b> 
  
<h2>Program walk-through:</h2>
-Authoritative Servers for the Root
<p align="center">
In a Command Prompt window, execute this command: dig

This command asks the default DNS server set for information about the empty domain, which means the root.
You see the authoritative root servers, as shown below:<br>
<p align="center">
<img src="https://i.imgur.com/Sfz4sOH.png height="65%" width="65%" />
<br />
<br /> 
<img src="https://i.imgur.com/FyG8muR.png height="65%" width="65%" />
<br />
<br />
-Understanding DNS Replies
In the "ANSWER SECTION", the first field is empty, indicating that this is the root domain.
The second field is the TTL. This should be a large number of seconds. 

The third field contains "IN", indicating that these are Internet records. DNS has the capacity to carry other types of data, but it's almost never used.

The fourth field contains "NS", indicating that these are Name Servers.

In the "ANSWER SECTION", the fifth field contains the names of the authoritative root servers.

In the "ADDITIONAL SECTION", the fifth field contains IP addresses for some of the servers.

At the bottom, this information is shown:

The time it took to perform the query
The DNS server that provided this data to you
A timestamp
Message size (max. 512 bytes for classical UDP-based DNS)
<br />
<br />
-Specifying the DNS Server: <br/>
<p align="center">
In a Command Prompt window, we need to execute this command:
dig @8.8.8.8
The answer is very similar to the one you saw before, but this time it comes from 8.8.8.8, which is Google's public DNS server, as shown below.
<img src="https://i.imgur.com/2lrvnIo.png height="65%" width="65%" /> 
<br />
<br />
-Resolving Juniper.com' Address at Google: <br/>
<p align="center">
In a Command Prompt window, we need to execute this command:
dig @8.8.8.8 www.juniper.com
<img src="https://i.imgur.com/YbyXweo.png) height="65%" width="65%" />
<br />
<br />
Notice that "QUESTION SECTION" shows...
juniper.com    IN     A
This indicates that dig performed a default query for the IN A record--the IPv4 internet address of the server.

The ANSWER section also resolves that FQDN, finding the IPv4 address "23.208.58.53".

Finally, in the top section of the response, notice the "flags: qr rd ra" message.

These flags indicate:

QR: Query Response
RD: Recursion Desired
RA: Recursion Available

-Resolving CCSF's Address from an Authoritative Server<br/>
<p align="center">
In a Command Prompt window, we need to execute this command:
dig @ns3.ccsf.edu www.ccsf.edu
<br />
<br />
<img src="https://i.imgur.com/02KFP69.png height="65%" width="65%" />
<br />
<br />
At the top left, notice the "flags: qr aa rd" message. The "aa" indicates that this is an authoritative response for the CCSF domain.

-Finding SOA Servers<br>
<p align="center">
To find the Start of Authority for the ccsf.edu domain, in a Command Prompt window, we need to execute this command:
dig @8.8.8.8 nba.com soa
<br />
<br />
The answer is a-148.akam.net, as shown below:
<p align="center"> 
<img src="https://i.imgur.com/ssrLFqd.pngheight="65%" width="65%" />
<br />
<br />
  
-Reverse DNS Queries<br>
<p align="center">
To perform reverse DNS queries, use the "-x" switch, as shown below:
dig @ns3.ccsf.edu -x 147.144.1.212
<br />
<br /> 
  
The answer is cloud.ccsf.edu, as shown below:<br>
<p align="center">
<img src="https://i.imgur.com/31zcoPT.png height="65%" width="65%" /> 
<br />
<br />

-Other Query Types: MX, ANY, RRSIG, AAAA
<p align="center">
You can find mail exchanges with an "mx" query, like this:
dig @8.8.8.8 nba.com mx
<img src="https://i.imgur.com/4kB6OyN.png height="65% width="65%" />
<br />
<br />
<p align="center">
-The "any" query finds all records on the server so in a Command Prompt window, we need to execute this command:
dig @8.8.8.8 nba.com any
<img src="https://i.imgur.com/B4VJlJ6.png height="65"% width="65%" />
<br />
<br />
-The RRSIG record finds DNSSEC signatures
<p align="center">
-For example, this query finds the signature of the .com top-level domain so in a Command Prompt, we need to execute this command:
dig @8.8.8.8 com rrsig
<br />
<br />
<img src="https://i.imgur.com/USyG1uw.png height="65%" width="65%" />
<br />
<br />
-IPv6 for CISCO.com
<p align="center"> 
-This query finds the IPv6 address for CISCO.  In a Command Prompt, we need to execute this command:
dig @ cisco.com aaaa
<br />
<br />
<img src="https://i.imgur.com/sWFahjU.png height="65%" width="65%" />










