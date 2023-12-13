# Terminologies in Networking

1. **Webhooks**:

    **Source of Information**:https://www.youtube.com/watch?v=mrkQ5iLb4DM

    - taking stripe and ec2 server instance communication as an example:
    ![img01](imgs/img01.png)
    - when you buy any subscription on stripe website, on the payment page when we click on pay button and your transanction is successful, then stripe sends the request to the lambda(graphql backend) with some metadata, and at the backend the metadata get decoded and you get the subscription.
    - Now at the payment page the subscription paying can be cancelled manually (synchronous way of telling backend server that nothing has been bought) or it could accidently get closed by closing our browser or loosing the internet connection (synchronous way of telling backend server that nothing has been bought).
    - How Server will know that the request is coming from a stripe not from an attacker; we can validate whether that message is coming from stripe server or not, because stripe will attach a hash with the message and the server at the backend can verify the message with the hash which is created by using same the secret key used by the stripe.
    - A server calling a server in a secure manner is a webhook.
    ![img02](imgs/img02.png)


## Common Networking Protocols

### SCTP (Stream Control Transmission Protocol)
#### source: https://www.juniper.net/documentation/us/en/software/junos/gtp-sctp/topics/topic-map/security-gprs-sctp.html#:~:text=Stream%20Control%20Transmission%20Protocol%20(SCTP)%20is%20a%20transport%2Dlayer,failover%20between%20redundant%20network%20paths.

- Stream Control Transmission Protocol (SCTP) is a transport-layer protocol that ensures reliable, in-sequence transport of data, SCTP provides multihoming support where one or both endpoints of a connection can consist of more than one IP address. This enables transparent failover between redundant network paths.
