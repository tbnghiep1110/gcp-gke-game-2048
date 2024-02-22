## CREATE VPC

    gcloud compute networks create game-2048-vpc --project=game-2048-415105 --description=game\ \ 2048\ vpc --subnet-mode=custom --mtu=1460 --bgp-routing-mode=regional


## CREATE SUBNET

PUBLIC  SUBNET 

    gcloud compute networks subnets create subnet-1 --project=game-2048-415105 --description=public\ subnet --range=10.1.0.0/24 --stack-type=IPV4_ONLY --network=game-2048-vpc --region=asia-southeast1
PRIVATE SUBNET

    gcloud compute networks subnets create subnet-2 --project=game-2048-415105 --description=private-subnet --range=10.2.0.0/24 --stack-type=IPV4_ONLY --network=game-2048-vpc --region=asia-southeast1

## SET FIREWALL RULE
### Open port  22  to ssh
    
>   gcloud compute firewall-rules create game-2048-vpc-allow-ssh   
> --project=game-2048-415105    --network=projects/game-2048-   415105/global/networks/game-2048-vpc   --description=Allows\ TCP\
> connections\    from\ any\ source\ to\ any\  instance\ on\ the\
> network\ using\ port\ 22. --   direction=INGRESS --priority=65534
> --source-ranges=0.0.0.0/0 --action=ALLOW rules=tcp:22



###  Open port 8080

>      gcloud compute firewall-rules create game-2048-vpc-allow-custom
>      --project=game-2048-415105 --network=projects/game-2048-
>      415105/global/networks/game-2048-vpc --description=Allows\ 
>      connection\ from\ any\ source\ to\ any\ instance\ on\ the\ network\  
>      using\ custom\ protocols.
>      --direction=INGRESS --priority=65534 --source-
>      ranges=10.1.0.0/24,10.1.0.0/24 --action=ALLOW --rules=tcp:8080

