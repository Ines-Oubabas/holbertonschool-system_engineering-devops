# Task 0: Simple Web Stack

This project involves designing a simple web infrastructure using a single server that hosts a website accessible via the domain **www.foobar.com**. The infrastructure relies on an **Nginx** web server, an application server, and a **MySQL** database.

## Objective

Create a web infrastructure that allows a user to access a website via the domain **www.foobar.com** and explain the role of each component in the architecture.

## Components Used

- **1 Server**: A physical or virtual machine that hosts all the services.
- **1 Web Server (Nginx)**: Handles HTTP requests and forwards them to the application server.
- **1 Application Server**: Executes the business logic of the application.
- **1 Database (MySQL)**: Stores the website's persistent data.
- **Domain Name**: **foobar.com** configured with a DNS record pointing to the IP address **8.8.8.8**.

## How the Infrastructure Works

1. **User**: The user tries to access the website through a browser by typing **www.foobar.com**.
2. **DNS Resolution**: The DNS server resolves the domain name **www.foobar.com** by returning the associated IP address **8.8.8.8**.
3. **Web Server (Nginx)**: The Nginx web server receives the user’s request and forwards it to the application server.
4. **Application Server**: This server processes the business logic of the application (for example, with PHP or Python code) and interacts with the database if necessary.
5. **Database (MySQL)**: The database stores and returns the requested information to the application server.
6. **Response to the User**: The web server sends the response back to the user's browser as a web page.

## Component Explanations

- **Server**: A machine that hosts all the necessary services for the web infrastructure.
- **Domain Name**: Allows users to access the server via an easy-to-remember URL rather than an IP address.
- **DNS Record (www)**: The **www** record is a type of DNS record that points to an IP address (here **8.8.8.8**).
- **Web Server (Nginx)**: Intercepts HTTP/HTTPS requests from users and forwards the information to the application server.
- **Application Server**: Processes the business logic of the application, runs scripts, and interacts with the database.
- **Database (MySQL)**: Stores the website’s data (users, content, etc.).

## Potential Issues

1. **Single Point of Failure (SPOF)**: If the server goes down, the website becomes inaccessible.
2. **Maintenance**: Any maintenance operation (such as updating the code) usually requires restarting the server, causing downtime.
3. **Scalability**: This simple infrastructure cannot handle heavy traffic, which may slow down the site or cause outages.

## Infrastructure Diagram

![Infrastructure Diagram](link_to_image)

## Conclusion

This infrastructure represents a simple solution to host a website using a single server. While this architecture works for small-scale projects, it has limitations in terms of scalability and fault tolerance.
