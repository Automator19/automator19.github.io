---
layout: post
title: How Kerberos and NTLM authentication works ?
category: [Windows]
---

# How does Kerberos authentication work?

To help understand how Kerberos authentication works, we'll break it down into its core components. Here are the main components involved in a typical Kerberos workflow:

- **Client:** The client acts ‘on behalf’ of the user and initiates communication when a service request is made.

- **Hosting server:** This is the server that hosts the service that the user wants to access.

- **Authentication Server (AS):** The AS performs the desired client authentication. If the authentication is successful, the AS issues a ticket to the client, the TGT (Ticket Granting Ticket). This ticket assures the other servers that the client is authenticated.

- **Ticket Granting Server (TGS):** The TGS is an application server that issues service tickets.
Key Distribution Center (KDC): The KDC consists of the Authentication Server (AS) and the Ticket Granting Server (TGS).

Now let's move on to the protocol flow, which is shown in the diagram

**Step 1:** The client makes an encrypted request to the authentication server. When the AS receives the request, it searches the Kerberos database for the password based on the user ID. If the user has entered the correct password, the AS decrypts the request.

**Step 2:** After verifying the user, the AS issues a Ticket Granting Ticket (TGT), which is sent back to the client.

**Step 3:** The client now sends the TGT to the TGS. Together with the TGT, the client ‘explains’ the reason for accessing the hosting server. The TGS decrypts the ticket using the secret key shared between the AS and the TGS.

**Step 4:** If the TGT is valid, the TGS issues a service ticket for the client.

**Step 5:** The client sends the service ticket to the hosting server. The server decrypts the ticket using the secret key shared between the server and TGB.

**Step 6:** If the secret keys match, the hosting server allows the client to access the service. The service ticket determines how long the user is allowed to use the service. Once the access expires, it can be renewed with the Kinit command by going through the entire Kerberos authentication protocol again.

![Kerberos Authentication Process](/assets/images/kerberos-authentication-process.JPG)

NTLM uses a challenge-response protocol to check a network user’s authenticity. To do so, the client and host go through several steps:

1. The client sends a **username** to the host.
2. The host responds with a **random number** (i.e. the challenge).
3. The client then generates a **hashed password** value from this number and the user’s password, and then sends this back as a response.
4. The host knows the user’s password and generates a hashed password value which it can then **compare to the client’s response**.
5. If both **values match**, the authenticity of the client is confirmed, and network access is granted. If there is no match between the values, the client will be denied access.

![NTLM Authentication Process](/assets/images/ntlm-authentication-process.JPG)