Introduction
============

About runadock
--------------

runadock is implemented as a PaaS for Developers to run and test applications in an easy way. We strongly focus on
* performance and 
* usability.

For more information about Docker look at https://www.docker.com/whatisdocker/

Features
--------

* dedicated IPv4 address
* use of GitHub repository to start a container and to run application
* cli (command line interface)
* REST API
* different sizes:

<table border="1">
  <tr>
    <th>Name</th><th>CPU</th><th>RAM</th>
  </tr>
  <tr>
    <td>XS (default)</td><td>128 shares</td><td>512 MB</td>
  </tr>
  <tr>
    <td>S</td><td>256 shares</td><td>1024 MB</td>
  </tr>
  <tr>
    <td>M</td><td>512 shares</td><td>2048 MB</td>
  </tr>
  <tr>
    <td>L</td><td>1028 shares</td><td>4096 MB</td>
  </tr>
</table>


* different plans: shared IPv4 addresses and dedicated IPv4 addresses
* disk space: 5 GB for all sizes
