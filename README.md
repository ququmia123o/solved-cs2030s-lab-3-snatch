Download Link: https://assignmentchef.com/product/solved-cs2030s-lab-3-snatch
<br>
<h3></h3>

<h4>Topic Coverage</h4>

<ul>

 <li>Abstract Classes / Interfaces</li>

 <li>Inheritance vs Composition</li>

 <li>Design Principles</li>

 <li><a href="https://www.comp.nus.edu.sg/~cs2030/style/" target="_blank" rel="noopener">CS2030 Java Style Guide</a></li>

 <li><a href="https://www.comp.nus.edu.sg/~cs2030/javadoc/" target="_blank" rel="noopener">CS2030 Java Documentation</a></li>

</ul>

<h4>Problem Description</h4>

<i>Snatch</i> is yet another transport service provider trying to vie for a place in the public transport arena.

<i>Snatch</i> provides three types of ride services:

<ul>

 <li><tt>JustRide</tt>

  <ul>

   <li>Fare is based on the distance <tt>@ 22</tt> cents per km</li>

   <li>Fare is the same regardless of the number of passengers (pax)</li>

   <li>There is no booking fee.</li>

   <li>A surcharge of 500 cents if a ride request is issued between the peak hour of <tt>600</tt> hrs to <tt>900</tt> hrs, both inclusive</li>

  </ul></li>

 <li><tt>TakeACab</tt>

  <ul>

   <li>Fare is based on the distance <tt>@ 33</tt> cents per km, but there is a booking fee of 200 cents</li>

   <li>Fare is the same regardless of the number of passengers (pax)</li>

   <li>No peak hour surcharge</li>

  </ul></li>

 <li><tt>ShareARide</tt>

  <ul>

   <li>Fare is based on the distance <tt>@ 50</tt> cents per km</li>

   <li>Fare is divided equally among the number of passengers</li>

   <li>There is no booking fee.</li>

   <li>Any fractional part of the fare is absorbed by your friendly driver</li>

   <li>A surcharge of 500 cents if a ride request is issued between <tt>600</tt> hrs to <tt>900</tt> hrs, both inclusive</li>

  </ul></li>

</ul>

In addition, there are two types of drivers under <i>Snatch</i>. Each can provide a subset of the services above.

<ul>

 <li><tt>NormalCab</tt> drivers provide <tt>JustRide</tt> and <tt>TakeACab</tt> services.</li>

 <li><tt>PrivateCar</tt> drivers provide <tt>JustRide</tt> and <tt>ShareARide</tt> services.</li>

</ul>

A customer can issue a <i>Snatch</i> ride request, specified by the distance of the ride, the number of passengers, and the time of the request.

<h4>Task</h4>

You shall be given a request, followed by a list of <tt>NormalCab</tt> or <tt>PrivateCar</tt> drivers together with their corresponding waiting times. A booking is a pairing of a driver with the request. The task is to find the best booking with the lowest fare by matching the available drivers based on the services they provide to the given request. Break ties among the same lowest fares by selecting the booking with the smaller waiting time.

<b>You may assume that no two bookings have the same fare and the same waiting time.</b>

This task is divided into several levels. Read through all the levels to see how the different levels are related.

Remember to:

<ul>

 <li>always compile your program files first before using <tt>jshell</tt> to test your program</li>

 <li>use <tt>checkstyle</tt> and <tt>javadoc</tt> comments to enhance code readability and facilitating code review</li>

</ul>




<table border="1" width="900" cellpadding="10">

 <tbody>

  <tr>

   <td><h4>Level 1</h4>Define a <tt>Request</tt> class to handle a request comprising the distance, number of passengers, and time.<pre>$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test1.jshjshell&gt; new Request(20, 3, 1000)$.. ==&gt; 20km for 3pax @ 1000hrsjshell&gt; new Request(10, 1, 900)$.. ==&gt; 10km for 1pax @ 900hrsjshell&gt; /exit</pre></td>

  </tr>

 </tbody>

</table>

<table border="1" width="900" cellpadding="10">

 <tbody>

  <tr>

   <td><h4>Level 2</h4>Now include the <tt>JustRide</tt> and <tt>TakeACab</tt> services. Note that every service needs to implement the <tt>computeFare</tt> method that returns the fare in cents.<pre>$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test2.jshjshell&gt; new JustRide()$.. ==&gt; JustRidejshell&gt; new JustRide().computeFare(new Request(20, 3, 1000))$.. ==&gt; 440jshell&gt; new JustRide().computeFare(new Request(10, 1, 900))$.. ==&gt; 720jshell&gt; new TakeACab()$.. ==&gt; TakeACabjshell&gt; new TakeACab().computeFare(new Request(20, 3, 1000))$.. ==&gt; 860jshell&gt; new TakeACab().computeFare(new Request(10, 1, 900))$.. ==&gt; 530jshell&gt; /exit</pre></td>

  </tr>

 </tbody>

</table>

<table border="1" width="900" cellpadding="10">

 <tbody>

  <tr>

   <td><h4>Level 3</h4>Now, include a <tt>NormalCab</tt> driver who is identified by its license plate number (a string) and the passenger waiting time in minutes.Then, add a <tt>Booking</tt> class that takes in a driver and a request. From the services that a driver provides, the best service with the lowest fare is selected.Two bookings may be compared using their computed fares; if both fares are the same, prefer the one with the shorter waiting time.<pre>$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test3.jshjshell&gt; new NormalCab("SHA1234", 5)$.. ==&gt; SHA1234 (5 mins away) NormalCabjshell&gt; new Booking(new NormalCab("SHA1234", 5), new Request(20, 3, 1000))$.. ==&gt; $4.40 using SHA1234 (5 mins away) NormalCab (JustRide)jshell&gt; new NormalCab("SHA2345", 10)$.. ==&gt; SHA2345 (10 mins away) NormalCabjshell&gt; new Booking(new NormalCab("SHA2345", 10), new Request(10, 1, 900))$.. ==&gt; $5.30 using SHA2345 (10 mins away) NormalCab (TakeACab)jshell&gt; Booking b1 = new Booking(new NormalCab("SHA2345", 10), new Request(10, 1, 900))jshell&gt; Booking b2 = new Booking(new NormalCab("SHA2345", 10), new Request(10, 1, 900))jshell&gt; b1.compareTo(b2) == 0$.. ==&gt; truejshell&gt; Booking b3 = new Booking(new NormalCab("SHA1234", 5), new Request(10, 1, 900))jshell&gt; Booking b4 = new Booking(new NormalCab("SHA2345", 10), new Request(10, 1, 900))jshell&gt; b3.compareTo(b4) &lt; 0$.. ==&gt; truejshell&gt; /exit</pre></td>

  </tr>

 </tbody>

</table>

<table border="1" width="900" cellpadding="10">

 <tbody>

  <tr>

   <td><h4>Level 4</h4>Now include the <tt>ShareARide</tt> service and <tt>PrivateCar</tt> driver.You should aim to make the <tt>Booking</tt> class general such that it does not need to check for any invalid pairing, say between <tt>PrivateCar</tt> driver and <tt>TakeACab</tt> service. If you have designed your program appropriately, then extending your program with additional drivers and services would not require any modification to existing classes.<pre>$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order &lt; test4.jshjshell&gt; new ShareARide()$.. ==&gt; ShareARidejshell&gt; new PrivateCar("SMA7890", 5)$.. ==&gt; SMA7890 (5 mins away) PrivateCarjshell&gt; new Booking(new PrivateCar("SMA7890", 5), new Request(20, 3, 1000))$.. ==&gt; $3.33 using SMA7890 (5 mins away) PrivateCar (ShareARide)jshell&gt; new PrivateCar("SLA5678", 10)$.. ==&gt; SLA5678 (10 mins away) PrivateCarjshell&gt; new Booking(new PrivateCar("SLA5678", 10), new Request(10, 1, 900))$.. ==&gt; $7.20 using SLA5678 (10 mins away) PrivateCar (JustRide)jshell&gt; Booking b1 = new Booking(new PrivateCar("SMA7890", 5), new Request(10, 1, 900))jshell&gt; Booking b2 = new Booking(new PrivateCar("SLA5678", 10), new Request(10, 1, 900))jshell&gt; b1.compareTo(b2) &lt; 0$.. ==&gt; truejshell&gt; /exit</pre></td>

  </tr>

 </tbody>

</table>

<table border="1" width="900" cellpadding="10">

 <tbody>

  <tr>

   <td><h4>Level 5</h4>Now complete the task by defining the <tt>findBestBooking</tt> method to return the best booking given a request, and an array of drivers with their waiting times. Save the method in the file <tt>level5.jsh</tt>.<b>Assume that no two bookings have the same fare and the same waiting time.</b><pre>$ javac your_java_files$ jshell -q your_java_files_in_bottom-up_dependency_order level5.jsh &lt; test5.jshjshell&gt; findBestBooking(new Request(20, 3, 1000),    ...&gt; new Driver[]{new NormalCab("SHA1234", 5), new PrivateCar("SMA7890", 10)})$.. ==&gt; $3.33 using SMA7890 (10 mins away) PrivateCar (ShareARide)jshell&gt; findBestBooking(new Request(10, 1, 900),    ...&gt; new Driver[]{new NormalCab("SHA1234", 5), new PrivateCar("SMA7890", 10)})$.. ==&gt; $5.30 using SHA1234 (5 mins away) NormalCab (TakeACab)</pre></td>

  </tr>

 </tbody>

</table>