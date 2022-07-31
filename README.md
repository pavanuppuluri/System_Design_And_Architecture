# Software Development Concepts - Design & Architecture
This repo contains various concepts realted to software development, design and architecture

## Monolithic architecture
<br>

* Self contained - packaged & deployed as single unit
* Three tiered application architecture
  * Presentation Layer
  * Application Layer
  * Data Layer
  
 ### Monolithic advantantages & disadvantages
 <table>
  <tr><td align="center"><b>Advantages</b> </td><td align="center"><b>Disadvantages</b> </td></tr>
  <tr><td>Single unit of deployment</td><td>Can be very large</td></tr>
  <tr><td>IDE Support</td><td>Technology dependency on initial decision</td></tr>
  <tr><td></td><td>Tight coupling between components</td></tr>
  <tr><td></td><td>Frequent deployments are difficult</td></tr>
  <tr><td></td><td>Need to scale entire application stack. Granular scaling not possible.</td></tr>
  <tr><td></td><td>Dynamic scaling is difficult</td></tr>
 <tr><td></td><td>If one component fails, entire application gets down</td></tr>
 </table>
 
 ## MicroServices

* Characteristics
  * Autonomous
  * Specialized

 ### MicroServices advantantages & disadvantages
 <table>
  <tr><td align="center"><b>Advantages</b> </td><td align="center"><b>Disadvantages</b> </td></tr>
  <tr><td>Flexible Scaling</td><td>Communication among different micro services</td></tr>
  <tr><td>Easy Deployment</td><td>Security</td></tr>
  <tr><td>Freedom to choose any technology</td><td>Maintenance</td></tr>
  <tr><td>Code reusability</td><td>Network performance</td></tr>
  <tr><td>Resilience</td><td></td></tr>  
 </table>


## Monolithic vs MicroServices
 <table>
  <tr><td align="center"><b>Monolithic</b> </td><td align="center"><b>MicroServices</b> </td></tr>
  <tr><td>Processes are tightly coupled and run as a single service</td><td>One service per process</td></tr>
  <tr><td>Adding features becomes more complex</td><td>Each service performs one single function</td></tr>
  <tr><td>Technology dependent</td><td>Technology independent</td></tr>
  <tr><td>Difficult to scale</td><td>Can be updated, deployed and scaled rapidly to meet demand</td></tr>
 </table>
 
 


