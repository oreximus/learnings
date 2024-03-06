# Kerberos

## What is Kerberos?

- **Kerberos** is an authentication protocol, not authorization. In other words, it allows to identify each user, who provides a secret password, however, it does not validates to which resources or services can this user access.

- Kerberos is used in Active Directory. In this platform, Kerberos provides information about the privileges of each user, but it is responsibility of each service to determine if the user has access to its resources.

## Kerberos Items

### Trasport layer

- Kerberos uses either UDP or TCP as transport protocol, which sends data in cleartext. Due to this Kerberos is responsible for providing encryption.

- Ports used by Kerberos are UDP/88 and TCP/88, which should be listen in KDC.

### Agents

- Several agents work together to provide authentication in Kerberos. These are the following:

    - **Client or user** who wants to access to the service.
    - **AP** (Appliation Security) which offers the service required by the user.
    - **KDC** (Key Distribution Center), the main service of Kerberos, responsible of issuing the tickets, installed on the DC (Domain Controller). It is supported by the **AS** (Authentication Service), which issues the TGTs.

### Encryption keys

- There are several structures handled by Kerberos, as tickets. Many of those structures are encrypted or signed in order to prevent being tampered by third parties. These keys are the following:

    - **KDC or krbtgt key** which is derivate from **krbtgt** account NTLM hash.
    - **User key** which is derivate from user NTLM.
    - **Service key** which is derivate from the NTLM hash of service owner, which can be an user or computer account.
    - **Session key** which is negotiated between the user and KDC.
    - **Service session key** to be use between user and service.

### Tickets

- The main structures handled by Kerberos are the tickets. These ticket are delivered to the users in order to be used by them to perform several actions in the Kerberos realm. There are 2 types:
    - The **TGS**(Ticket Granting Service) is the ticket which user can use to autheticate against a service. It is encrypted with the service key.
    - The **TGT**(Ticket Granting Ticket) is the ticket presented to the KDC to request for TGSs. It is encrypted with the KDC key.

### PAC

- The **PAC** (Privilege Attribute Certificate) is an Structure included in almost every ticket. This structure contains the priviliges of the user and it is signed with the KDC key.

- It is possible to services to verify the PAC by communicating with the KDC, although this does not happens often. Nevertheless, the PAC verification consists of checking only its signature, without inspecting if privileges inside of PAC are correct.

- Furthermore, a client can avoid the inclusion of the PAC inside the ticket by specifying in KERB-PA-PAC-REQUEST field of ticket request.

### Messages

- Kerberos uses differents kinds of messages. The most interesting are the following:
    - **KRB_AS_REQ**: Used to request the TGT or KDC.

