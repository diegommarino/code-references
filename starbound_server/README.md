# EC2 Starbound server
This document show how you can create your own starbound server using Amazon EC2.

## Pre-requisites
- Have an AWS account

## Costs
I tried to use free tier elegible instances T2.micro, but without luck, because of its low memory and storage. Looks like a Starbound server requires at least 1gb of
memory and 50gb space. I could run the server ok creating a T2.medium instance this instance cost $0.05 hour. I'm also taking a look on Digital Ocean that have the
same instance but with lower cost $0.02 hour.

