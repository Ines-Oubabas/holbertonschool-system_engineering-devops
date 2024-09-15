# Web Infrastructure Design

## Project Overview

This project involves the design and documentation of multiple web infrastructure scenarios, ranging from a simple single-server setup to a more complex secured and monitored multi-server environment. Each task demonstrates different architectural decisions, from scaling and redundancy to security and monitoring.

---

## Task 0: Simple Web Infrastructure (One Server with LAMP Stack)

### Overview:
The first setup demonstrates a single server infrastructure using the LAMP stack (Linux, Apache/Nginx, MySQL, and PHP). The server hosts a website accessible via `www.foobar.com`.

### Components:
- **1 Server**: The central component that hosts the entire web application.
- **1 Web Server (Nginx)**: Handles incoming HTTP requests.
- **1 Application Server**: Manages the application logic and interaction with the database.
- **1 Database (MySQL)**: Stores and retrieves application data.
- **Domain Name**: `foobar.com` is mapped to the server IP using a `www` record.

### Key Explanations:
1. **What is a server?**
   - A server is a machine that provides data or services to other computers, allowing users to access hosted websites or applications.
   
2. **Role of the domain name?**
   - The domain name makes it easy for users to access a website by typing a human-readable address instead of an IP address.

3. **What is the `www` DNS record?**
   - The `www` DNS record is an `A` record, which maps the domain name to an IP address, such as `8.8.8.8`.

4. **Role of the Web Server?**
   - The web server (Nginx) processes incoming HTTP requests and serves the necessary content (either static files or dynamic requests forwarded to the application server).

5. **Role of the Application Server?**
   - The application server processes the core logic of the website and interacts with the database to fetch and store data.

6. **Role of the Database?**
   - The MySQL database stores structured data, such as user profiles, orders, or content.

7. **Issues with this infrastructure (SPOF)**:
   - **Single Point of Failure (SPOF)**: Since all services run on one server, if it fails, the entire infrastructure goes down.
   - **Scalability**: This infrastructure cannot scale efficiently if traffic increases.

---

## Task 1: Distributed Web Infrastructure (Three Servers)

### Overview:
This task demonstrates a more advanced infrastructure using multiple servers. A load balancer distributes traffic between two application/web servers, while the database is configured in a Primary-Replica (Master-Slave) setup.

### Components:
- **2 Servers**: One for each web and application service.
- **1 Load Balancer (HAProxy)**: Distributes traffic between the two servers.
- **1 Application Server**: Handles application logic and processes requests.
- **1 Database (MySQL, Master-Slave)**: The primary database handles writes, and the replica handles read operations.
- **Domain Name**: `foobar.com` still points to the load balancer.

### Key Explanations:
1. **Why add each additional element?**
   - The second server and load balancer allow for improved availability and redundancy by distributing traffic and minimizing the risk of a single point of failure.
   
2. **Load Balancer Algorithm?**
   - The load balancer can use **round-robin** or **least-connections** algorithms to distribute traffic evenly.

3. **Active-Active vs. Active-Passive Load Balancer?**
   - In **Active-Active**, both servers handle traffic simultaneously, while **Active-Passive** involves one server in a standby mode in case the other fails.

4. **Primary-Replica Cluster:**
   - The **Primary** server handles writes, while the **Replica** handles read-only requests, improving performance and availability.

5. **Issues with this infrastructure:**
   - **SPOF**: While the servers are redundant, the load balancer or database server could become single points of failure.
   - **Security concerns**: Without firewalls or HTTPS, this infrastructure is vulnerable to attacks.
   - **No monitoring**: There's no system in place to detect issues or failures automatically.

---

## Task 2: Secured and Monitored Web Infrastructure

### Overview:
This task adds additional security and monitoring components to the existing distributed infrastructure. Firewalls protect the servers, traffic is encrypted over HTTPS, and monitoring tools keep track of performance and detect failures.

### Components:
- **3 Firewalls**: Protect the servers by filtering incoming and outgoing traffic.
- **1 SSL Certificate**: Encrypts data exchanged between the user and the website using HTTPS.
- **3 Monitoring Clients**: Tools like Sumologic are used to collect metrics and alert administrators of any issues.

### Key Explanations:
1. **Why add each additional element?**
   - Firewalls secure the servers by blocking unauthorized traffic, while HTTPS encrypts communication between users and the web servers.
   
2. **What are firewalls for?**
   - Firewalls prevent unauthorized access to the servers, acting as a gatekeeper between trusted internal networks and untrusted external networks.

3. **Why is the traffic served over HTTPS?**
   - HTTPS ensures that all data transferred between the user and the server is encrypted, providing confidentiality and integrity.

4. **How does the monitoring tool work?**
   - Monitoring tools collect data like server load, error rates, and user activity to alert administrators if performance thresholds are crossed.

5. **Monitoring web server QPS (Queries Per Second)?**
   - Monitoring QPS can be done using tools like **Prometheus** or **Grafana**, which track server metrics in real-time.

6. **Issues with this infrastructure:**
   - **SPOF**: The load balancer or database can still be a single point of failure.
   - **SSL termination**: Handling SSL at the load balancer level can complicate the traffic flow and adds processing overhead.
   - **Only one MySQL server for writes**: If the primary MySQL server fails, the entire system loses the ability to write data.

---

## Task 3: Scaling Up

### Overview:
This final task demonstrates how to scale up the infrastructure by adding additional servers to separate the web, application, and database components, ensuring that each part can scale independently.

### Components:
- **1 Additional Server**: For either the web or application layer.
- **1 Load Balancer (HAProxy)**: Configured in cluster mode to provide failover and distribute traffic across multiple servers.

### Key Explanations:
1. **Why split components?**
   - By separating the web server, application server, and database onto their own machines, each can scale independently based on load. For example, more web servers can be added to handle traffic spikes without affecting the database or application logic.

2. **Why use a load balancer in cluster mode?**
   - Using a clustered load balancer ensures failover, so if one load balancer fails, another takes over, maintaining service continuity.

3. **Issues with this infrastructure:**
   - While the system is highly scalable, it introduces more complexity, especially in ensuring synchronization between components (e.g., databases) and managing multiple servers.

---

## Conclusion:
Each task represents a more complex and robust infrastructure, focusing on scalability, security, and monitoring. The final architecture ensures high availability, redundancy, and fault tolerance, making it ideal for production-grade web applications.

