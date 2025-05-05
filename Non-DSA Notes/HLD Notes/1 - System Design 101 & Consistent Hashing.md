1
---
title: Module Introduction
description: A brief definition of system design.
duration: 300 
card_type: cue_card
---

## Module introduction

Before we begin the classes, let me share some resources and ground rules for this module. 

- **Tentative curriculum:** https://docs.google.com/spreadsheets/d/1VYizqsjlbcurqAMtDsDaCBIIZuTjqH_w3cJfTUNaejw/edit#gid=0 (please go through after the class)
    - If you are a beginner, it is important that you quickly browse through the notes before the class happens. Will make it easier for you to understand the classes. 
    - This also has some pre-requisite reading material. All of you should go through it. 
- All of you should be a part of the **HLD whatsapp group**. Please check your messages for the link. If not, can someone in the class post the link to join the group?
    - We will keep sharing resources here. Also, we will keep discussing various scenarios / problems here. I will also be part of the group. 
- **What is system design:** Till now, we focussed heavily on LLD. Which means that for a given project, how should we design schema, API, or structure the code. System design is the study of how to design the architecture of software, what database to use, what kind of caching, how does information flow and how do you make your system reliable / fast / fault tolerant. 
    - If some of the above terms don't make sense right now, do not worry. We will discover these one by one. 

- **What is not going to happen in system design:** System design is not about knowledge. It's more about developing the problem solving skill of being able to make right design choices. You won't be judged on your knowledge of what Twitter uses, but rather if asked to design twitter news feed, are you able to rationalise and explain how you'd design it and why? 
    - Implementation of what we teach is done in the backend project section. All HLD classes are going to focus on the above problem solving skill. 

---
title: Why do we need distributed system
description: An example highlighting the need of distributed systems.
duration: 300 
card_type: cue_card
---

## Why do we need distributed systems?

Let’s take a real story of a website that started on a single laptop in a dorm room (Exactly how we write code today). Back in 2003, there was a website that went by the name of Del.icio.us (https://en.wikipedia.org/wiki/Delicious_(website)). 

Browsing the internet was completely based on bookmarks and you would lose bookmarks the moment you changed browser / machine. So, delicious built a bookmarking website. You login, and then bookmark websites using delicious tool. That way, when you go to any other machine/browser, all you need to do is to login into delicious with your account to get access to all your bookmarks. Basically, largely delicious implemented following 2 functions:

```sql
addBookmark(userId, site_url)
getAllBookmarks(userId)
```
If you were to code those 2 functions on your laptop, would you be able to? Assume you store entries in MySQL database which is also on your laptop. 
If yes, congratulations. Your version of delicious is almost ready. 

---
title: DNS and ICANN
description: How internet works
duration: 300 
card_type: cue_card
---

## DNS and ICANN

**Problem 1**: How do I ensure that when people type del.icio.us in their browsers, they reach my laptop? 

The internet world only understands IP Address. How do people know the IP address of my laptop when they type del.icio.us? 

> How many of you have ever built a personal website? 

How do you setup your personal website today? 
* You go to GoDaddy (or similar websites) to buy a domain. 

Ok, but how does GoDaddy know which domain name is available? People can buy domains from GoDaddy / NameCheap / domains.google and tons of other websites.

There must be a central place maintaining domain names and their owners. And yes, there is. It’s called ICANN (The Internet Corporation for Assigned Names and Numbers). It’s non profit and has a directory of all registered domain names along with their owner details and the date validity. 


---
title: How can people globally and uniquely identify a domain name
description: Example of a bookmarking website Del.icio.us highlighting how IP addresses are tied to domain names
duration: 300 
card_type: cue_card
---

## How can people globally and uniquely identify a domain name?

Alright. But that still does not solve my problem. If I go to GoDaddy and buy delicious domain name, is my issue solved? A random user’s browser still does not know how to reach my laptop. 

So, that means I should be able to associate my domain name to my laptop’s IP address. That is exactly what happens. You can create “A” record in GoDaddy / Namecheap that is then registered centrally. 
* Further reading:
    * https://www.namecheap.com/support/knowledgebase/article.aspx/319/2237/how-can-i-set-up-an-a-address-record-for-my-domain/
    * https://support.dnsimple.com/articles/differences-between-a-cname-alias-url/ 

Ok, so now ICANN knows IP address of my laptop tied to delicious domain name that I bought. 
Which means theoretically, when someone types delicious in their browser, they can get the IP address they need to go to from ICANN. But is that a good design? 

Not really. All internet traffic will need to go to ICANN first. That's more than the traffic of Google/FB, etc. combined. ICANN becomes the single point of failure for the entire internet. 

---
title: Need of DNS, and how it works
description: A brief description of what DNS is and how it works.
duration: 300 
card_type: cue_card
---

## Need of DNS

Ok, then what do we do? Imagine if there were thousands of machines all around the internet that had a **copy of the information** there on ICANN. Then my problem could have been solved. Because now people typing delicious on their browser, could find out the IP address from these machines. 

Very simplistically, these machines are called DNS machines (Domain Name Servers). While the DNS architecture is decently complicated (You can read https://support.dnsimple.com/articles/differences-between-a-cname-alias-url/ if interested), in simple words, DNS machines maintain a copy of information present centrally and they keep pinging every few hours to get any recent updates from the central machines. 
[Not spending time on DNS architecture since the class is not on DNS. We did the discussion to give an insight into how internet works]. 

---
title: DNS questions
description: who maintains DNS
duration: 300 
card_type: cue_card
---

## DNS questions

Ok, you might have the following questions:
 - Who owns these DNS machines? 
 - How do DNS machines stay updated as entries change in ICANN? 

Let's go one by one. 
On who owns DNS, who benefits from maintaining these machines:
 - One is your Internet Service Provider (ISPs like Airtel, Tata, etc.). If your Domain Name -> IP resolution is slow, your entire internet will feel slow. So, they would want to maintain these machines to make IP lookup faster. This is the default DNS setup. If you don't change anything manually, your machine is most probably talking to a DNS machine from your ISP. 
 - There are other companies who benefit from more people using the internet. For example, Google or CDN providers. Hence, Google owns some DNS machines, and so do companies like CloudFlare. 

Q2. How do DNS machines stay updated? 
Ofcourse, if they keep asking ICANN for the entire dump, it's going to make ICANN machines crash. So, they ask for the change after a particular timestamp. 
And they do it infrequently. 
General direction given is that if you change your A / cname records, it takes up to 24 hours for every DNS machine to catch up. 

---
title: Static vs dynamic IP
description: Ensuring Host IP does not keep changing
duration: 300 
card_type: cue_card
---

## Static vs dynamic IP

Ok, let's come back to our Delicious example. 

How does a machine get an IP address? When you connect to the internet, your ISP assigns one of the available IP addresses (IP address not assigned to any active machine on the internet) to you. 

Ok, how does ISP find such an address? Typically, ISPs own a range of IP addresses to assign. They get one from there. 

In our delicious example, let's say when my laptop connects to the internet, it gets an IP address 10.20.30.40. 
And hence, what IP address should I feed in ICANN? Correct, 10.20.30.40. 

But imagine if my laptop disconnects. When it reconnects, is it guaranteed to get the same IP again? No. What if it gets 10.21.31.41? 
Then, all requests to delicious will fail. Because users would be trying to connect to 10.20.30.40. 

That's a problem. How do we solve it? 
The IP address stated above is a dynamic IP address. 
You can also reserve an IP address for yourself by paying more money. It's called static IP address. Sort of like paying more money to get a custom number plate for your bike. 

---
title: Distribution of load
description: A brief discussion of why load balancing is required and how it helps in increasing availability of the system.
duration: 300 
card_type: cue_card
---

## Distribution of load

Ok, so now we are live. Delicious is now serving users. 
There is a small problem though. Everytime I want to add new features and re-deploy and re-start my laptop with new code, delicious is unavailable for a few seconds. That’s not good. So, what do I do? 

Infact, if my laptop reboots or disconnects from the internet, again website is down. Not good, right? 

Maybe instead of one laptop, I have multiple laptops with same code and same information (We will figure out how to keep this information in sync). However, when my code is being deployed to a laptop X, how do I ensure no traffic is coming to X? 
We need a Load Balancer which keeps track of laptops, which ones are running and is responsible to split the load equally. 

How does Load balancer do that? 
* Which machines are alive? - Heartbeat / Health Check
* Splitting load? - Round robin / Weighted Round Robin / Ip Hash 

> Note: Please spend time here explaining Round robin / Weighted Round robin. Very similarily, explain heartbat and health check mechanisms. Important to land the message that Load Balancer knows about machines and tracks their live/dead status. 

https://docs.nginx.com/nginx/admin-guide/load-balancer/http-load-balancer/ has example of a config setup of a load balancer. 

---
title: What is sharding and why do we need it
description: An example highlighting the need of splitting the information you have between machines.
duration: 300 
card_type: cue_card
---

## What is sharding and why do we need it?

Imagine, Del.icio.us becomes majorly popular. It starts getting massive traffic. It starts getting a million new bookmarks every day. 
Now, remember this is 2004. Best machines had 40GB hard disk. If you were getting 1 Million new bookmarks every day, and every bookmark is 200 bytes roughly, then you are adding 200MB of new bookmarks every day. Which means you will run out of space in 6 months. What do you do? 

We can get better machines. Maybe machines with higher storage, better CPU. They'd be expensive but will buy us more time. 
This is called **vertical scaling**. 

However, vertical scaling will not solve the problem for me permanently. 

So, that means I need some way of splitting data between the machines. Then, if I have 100 such machines, my total storage becomes 
   $40GB * 100 = 4TB$
That is called **horizontal scaling**. 

How do I split data though? 


You will have to consider splitting the information you have between machines. This is called sharding. 

---
title: How sharding works
description: A sneak peek into detailed working of sharding.
duration: 300 
card_type: cue_card
---

## How sharding works?

**Step 1**: Choose sharding key. Basically what information should not get split between machines, and should reside in the same machine. 
Show what happens if you choose site_url as the sharding key. getAllBookmarks has to go to all machines. 
We choose user_id to be the sharding key, which means a user and all their bookmarks go to one shard. 

**Step 2**: Build out an algo for userId -> shard mapping. 

Following constraints:
* Finding shard given userID should be extremely lightweight. Can’t add a lot of load to LB. 
* Load should be somewhat equally distributed (no load skew)
* Addition of new shards should be easy and should not cause major downtime. 
* Same for removal of shards. 

---
title: Various approaches to sharding.
description: A brief discussion of the various approaches of sharding.
duration: 300 
card_type: cue_card
---

## Approaches to Sharding

Let’s check certain approach for sharding. 

**Approach 1:** Assign userId to userId % number_of_shards. While this approach is great, it fails when number of shards change, as it causes almost every user’s data to be copied to another machine. Massive downtime when shard is added.(Modulo based distribution of load)

**Approach 2:** Range based assignment. Load skew - first adopters more likely to be busier users. Also, every range’s total storage usage will only increase as they add more bookmarks. Addition of new shard does not help existing shards.(Range based distrtibution of load) 

Let’s look at the real approach used in most cases - Consistent Hashing. 


---
title: Introduction to consistent hashing.
description: Demonstration of how consistent hashing works using an example.
duration: 300 
card_type: cue_card
---


## Consistent Hashing 

Imagine a circle with points from $[0, 10^{18}]$. Imagine there is a hash function H1, which maps every machineId to a number in $[0, 10^{18}]$, which you then mark on the circle. Similarly, there is another hash function H which maps userId to $[0, 10^{18}]$. 

Let’s assume we assign a user to be present on the first machine in the cyclic order from the hash of the user. 



![](https://d2beiqkhq929f0.cloudfront.net/public_assets/assets/000/049/547/original/Screenshot_2023-09-20_184255.png?1695215796)

For example, in the diagram above, Deyan and Affrica are assigned to Node 2, Freddie and Srushtika on Node 5 and so on. 
In implementation, if you have a sorted array with hashes of nodes, then for every user, you calculate the hash, and then binary search for the first number bigger than the given hash. That machine is what the user will be assigned to. 

However, this design suffers from an issue. What happens when you remove a shard. Let’s say Node 2 is down. All load of Node 2 (Deyan + Africa) get assigned to Node 5 and Node5’s load basically doubles. At such high load, there is a good probability that Node 5 dies which will triple the load for Node 4. Node4 can also die and it will trigger cascading failure. 

---
title: Optimizing the consistent hashing.
description: Discussion the modification in consistent hashing algorithm to minimise chances of cascading failure.
duration: 300 
card_type: cue_card
---

## Optimizing the consistent hashing

So, we modify the consistent hashing a little bit. Instead of one hash per machine, you use multiple hashing functions per machine (the more, the better). So, Node 1 is present at multiple places, Node 2 at multiple places and so forth. 


![](https://d2beiqkhq929f0.cloudfront.net/public_assets/assets/000/049/548/original/Screenshot_2023-09-20_184304.png?1695215817)


In the above example, if node A dies, some range of users is assigned to B, some to D and some to C. That is the ideal behavior. 


---
title: Data transfer
description: How will data be transferred when shards are added or removed. 
duration: 300 
card_type: cue_card
---

## Data transfer

Typically, when you add a shard, if you immediately make it active, then it will have no data. Queries will fail. 
That's bad. 

So, we typically folllow a process of warming up the shard before making it active. 

 - **Timestamp T1:**<br> Start the transfer of relevant users to the new shard. Relevant users are the users who would have been on this shard if it was added. Note the shard is not added yet, and hence is not getting any traffic. 

 - **Timestamp T2:**<br> Transfer is complete. We now add the new shard, and it starts getting traffic. Only problem is that there might be new entries added for these users between T1 and T2 (very small number of entries, but non zero). 
     - So, we start the copy process of incremental data for users between T1 and T2. This should be very quick. For those few seconds, following 2 options:
         - I reject the incoming requests on new shard and compromise availability.
         - Or I return response which might be inconsistent (compromise consistency). 

See you in the next lecture! 

----------------------------------------------------------------------------------------------------------------------------

___


Vertical Scaling :   
    * hardware limitations  
    * high cost  
    * single point of failure  
    
Horizontal Scaling :  
    * No spof  
    * No h/w limitations  
    * can be expanded infinitely but system becomes more complex  

    

__Load Balancer__ :  
Balances the load equally to all servers. in large applications we have multiple load balancers.  

* To avoid spof, we ususally have multiple LB assigned at different IPs, it also reduces latency.  
  
* we have different mechanisms for LB to check if servers are up or not.  
    * heartbeat - every server is configured in such a way that it send a heartbeat every 1 second to LB, if LB misses 3 or more beats from                   any server it assumes, the server is down.  
    * Health check - every 1 second, LB will keep pinging the servers, if it recieves the acknowledgement, it assumes servers are up.

* Routing Algorithms:  
      * fast 
      * easy to implement  
      * llight  
      * easy addition/removal of servers  
      * less data transfer should take place if server is added or removed.  

* __stateless vs statefull load balancing__.
      
    * Stateless systems do not retain any session data. Requests are distributed randomly or using simple algorithms like round-robin, where each request is sent to the next server in a cyclic order.
Benefits include easier scaling as there's no need for synchronization of state between servers【8:4†source】【8:3†source】.

    * Stateful Load Balancing:
Involves maintaining session information or state about the user's requests. This is essential in applications where each request depends on prior interactions (e.g., chatbots like ChatGPT).
The load balancer ensures that requests from the same user go to the same server to maintain continuity


* __Stateless LB algo__:  
      1) Round Robin :  
          * easy n light to implement  
          * equal distribution of load  
          * stateless LB  
          * CON : RR algo redirects the same traffic to all machines irrespective of their capacity.  
      2) Based on response time  
      3) Based on the no of requests for each server(weighted RR)  


* __Statefull LB algo__:  
      1) Maintain key,value pair at LB - easy but disadvantage is the size of the rows for key,value pair.  
      2) Range based distribution - like 1-1000 -> m1  
                                         1k-2k -> m2....  
          It solves the previous issue of size. if any machine goes down, redistribute the load. but it wil lead to lot of data transfer if           any machine goes down and resditribution happens. so not a very good algo  
      3) Modulo based : user_id % N. but if no of machines(N) change, all other gets reshuffled.
                        there is lof of data transfer, shuffling in the above algo. Consistent hashing solves most for these issues.  

      4) __CONSISTENT HASHING__ :  
          It provides flexibility in scaling as it provides minimal data movement during shard changes or if a machine goes down. divides             the laod equally.  



* __SHARDING__ :  
    Sharding is a database partitioning technique crucial for horizontal scaling. It involves distributing a large dataset across multiple      databases or shards.  

    __Vertical Scaling__: Upgrading resources in a single server.  
    __Horizontal Scaling__: Distributing data across multiple servers.  
  
    How Sharding Works  
    1) Choosing a Sharding Key:  
    The sharding key determines how data is distributed across shards. A good key ensures even distribution and easy access.
    Example: Using user_id as a sharding key to keep all data for one user together on the same shard】.  
    
    3) User to Shard Mapping:  
    Mapping algorithms must ensure minimal load skew and easy addition/removal of shards.
    
    Approaches to Sharding  
    * Modulo-based Sharding: Uses the modulo operation to determine the shard. Simple but fails during shard scaling as it causes data     
      redistribution.  
    * Range-based Sharding: Assigns shards based on predefined data ranges.  
    * Consistent Hashing: Provides flexibility in scaling as it requires minimal data movement during shard changes.  
      
    Optimizing Sharding  
    Data Transfer: When adding or removing shards, data transfer should be optimized to occur with minimal impact on availability  

* __Replication__ : it is creating and maintaing duplicate copies of Database in different servers. it is also a scaling technique but it create only multiple copies of same data in multiple nodes.  

* __Sharding VS Partitioning__ :  
      Sharding vs Partitioning: What’s the Difference ?  

    When scaling databases, two key strategies emerge -- Partitioning and Sharding. While they seem similar, but in reality they serves     
    different purposes.  
    
    🔹 __Partitioning__ (Logical Separation)  
     👉 Think of partitioning like dividing a library into sections—Fiction, Non-fiction, Science, History. The data still resides in a 
        single database but is split logically (based on a column like date, region, etc.).  
    
    🔹 __Sharding__ (Physical Separation)  
     👉 Sharding is like having multiple branch libraries across different cities, each storing books for specific categories. Data is 
        distributed across multiple databases (shards), reducing load on a single system.  
    
    💡 Key Difference?  
    • Partitioning optimizes query performance within one DB.  
    • Sharding enables horizontal scaling across multiple DBs.  
    
    💡 Real-World Use Cases:  
     ✅ Partitioning – Storing financial transactions by month/year in a banking app for faster retrieval.  
     ✅ Sharding – A global social media platform where user data is stored in different databases based on geolocation.






***


   [lecture 2 notes] (https://airlock-on-edge.woolf.university/?url=https%3A%2F%2Fscaler-production-new.s3.ap-southeast-1.amazonaws.com%2Fattachments%2Fattachments%2F000%2F251%2F855%2Foriginal%2FSystem_Design___Load_Balancing_and_Consistent_Hashing___3rd_March.pdf%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Credential%3DAKIAIDNNIRGHAQUQRWYA%252F20250505%252Fap-southeast-1%252Fs3%252Faws4_request%26X-Amz-Date%3D20250505T222851Z%26X-Amz-Expires%3D561600%26X-Amz-SignedHeaders%3Dhost%26X-Amz-Signature%3Dff1daf33c34fe1204650f51bd1e56d913e89f0917077212d1e39401cc0b0aa62&resourceId=974b6aff-f986-4584-92a9-ded3df3097c8&studentId=b3ffae78-376c-40f6-a686-a1eb6560b82d&token=eyJhbGciOiJIUzI1NiJ9.eyJpZCI6ImIzZmZhZTc4LTM3NmMtNDBmNi1hNjg2LWExZWI2NTYwYjgyZCIsImlzcyI6InVybjpXb29sZlVuaXZlcnNpdHk6c2VydmVyL3NlcnZpY2UvYWNjZXNzIiwiaXNWZXJpZmllZCI6dHJ1ZSwia2luZCI6Im9hdXRoIiwib3JnIjp7Imdyb3VwcyI6W10sImlkIjoiOWIxN2Y1Y2UtMTA3OC00ZmRmLWFlYzAtMDJiZjRlY2ZiMGE2In0sInNjb3BlIjoiKiJ9.-RiUerqfMZz_f13n9wInEAS9DOgfb35uxZabX25SqBs)

[lecture 3 notes] (https://airlock-on-edge.woolf.university/?url=https%3A%2F%2Fscaler-production-new.s3.ap-southeast-1.amazonaws.com%2Fattachments%2Fattachments%2F000%2F252%2F401%2Foriginal%2FSystem_Design____Caching__5th_March_.pdf%3FX-Amz-Algorithm%3DAWS4-HMAC-SHA256%26X-Amz-Credential%3DAKIAIDNNIRGHAQUQRWYA%252F20250505%252Fap-southeast-1%252Fs3%252Faws4_request%26X-Amz-Date%3D20250505T222853Z%26X-Amz-Expires%3D561600%26X-Amz-SignedHeaders%3Dhost%26X-Amz-Signature%3D01db7cee2ad67868471a26bb157cc370eccd239dd250cb932467d8b13e9d0bc7&resourceId=6a700bb9-0d2d-49db-b0dc-c3782407f4b4&studentId=b3ffae78-376c-40f6-a686-a1eb6560b82d&token=eyJhbGciOiJIUzI1NiJ9.eyJpZCI6ImIzZmZhZTc4LTM3NmMtNDBmNi1hNjg2LWExZWI2NTYwYjgyZCIsImlzcyI6InVybjpXb29sZlVuaXZlcnNpdHk6c2VydmVyL3NlcnZpY2UvYWNjZXNzIiwiaXNWZXJpZmllZCI6dHJ1ZSwia2luZCI6Im9hdXRoIiwib3JnIjp7Imdyb3VwcyI6W10sImlkIjoiOWIxN2Y1Y2UtMTA3OC00ZmRmLWFlYzAtMDJiZjRlY2ZiMGE2In0sInNjb3BlIjoiKiJ9.-RiUerqfMZz_f13n9wInEAS9DOgfb35uxZabX25SqBs)
