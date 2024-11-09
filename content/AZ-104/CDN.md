---
title: What are CDNs?
aliases:
  - CDN
draft: false
tags:
  - AZ-104
  - Cloud
  - Microsoft
author:
  - Sarthak Chandajkar
---
A **Content Delivery Network (CDN)** is a network of servers distributed across various geographical locations that work together to deliver content to users more quickly and efficiently. The primary purpose of a CDN is to reduce latency (the time it takes for data to travel from the server to the user's device) and improve the performance of websites, especially for users who are far from the original server.

### **How CDNs Work**

- **Geographically Distributed Servers:** CDNs have multiple servers located in different regions around the world, often called "edge servers." When a user requests content (like a webpage, image, or video), the CDN serves that content from the server closest to the user's location, reducing the distance the data must travel.
    
- **Caching:** CDNs cache (store) copies of content on these edge servers. When a user requests a piece of content, the CDN checks if it has a cached copy on the nearest edge server. If it does, the content is delivered directly from that server, speeding up the delivery process. If not, the content is retrieved from the origin server, then cached for future requests.
    
- **Load Balancing:** CDNs distribute incoming traffic across multiple servers, which helps prevent any single server from becoming overloaded. This leads to better performance and reliability, especially during traffic spikes.
    

### **Benefits of Using CDNs**

1. **Faster Load Times:** By serving content from a server closer to the user, CDNs significantly reduce the time it takes for web pages to load.
    
2. **Improved Reliability:** CDNs ensure that even if one server fails, others can take over, making websites more resilient to downtime.
    
3. **Scalability:** CDNs can handle large amounts of traffic by distributing the load across many servers, which is particularly useful during high-traffic events like sales or streaming large live events.
    
4. **Better Security:** CDNs can provide enhanced security features, such as Distributed Denial of Service (DDoS) protection, by distributing and absorbing malicious traffic.
    
5. **Global Reach:** CDNs make it easier for users around the world to access content quickly, helping websites serve a global audience effectively.
    

### **Common Use Cases**

- **Media Streaming:** CDNs are commonly used for delivering video and audio streams to ensure smooth playback without buffering.
- **Websites and Blogs:** Popular websites and blogs use CDNs to serve static content like images, CSS, and JavaScript files quickly.
- **E-commerce:** Online stores use CDNs to deliver product images and assets to customers worldwide, improving the shopping experience.
- **Software Distribution:** CDNs are used to distribute software updates and downloads efficiently.

### **Popular CDN Providers**

- **Akamai**
- **Cloudflare**
- **Amazon CloudFront**
- **Google Cloud CDN**
- **Microsoft Azure CDN**

In summary, CDNs play a crucial role in modern web infrastructure by improving the speed, reliability, and security of content delivery across the globe.