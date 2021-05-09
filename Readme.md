# **Deploying Ghost on Do-K8s**
## Prequistes
1. Install do command line tool (doctl) to acces your k8s cluster.<br/>
   Steps can be found here https://docs.digitalocean.com/reference/doctl/
2. Make sure you have helm installed in your system.</br>
   Steps can be found here https://helm.sh/docs/intro/install/
### Deployment Begins 
- Deploy volume.yml</br>
      `kubectl apply -f volume.yml`


- Run helm.sh</br>
      `chmod +x helm.sh`
      `./heml.sh`


- After running helm.sh you will see that your nginx ingress controller
  and cert manager has been installed.
  `kubectl get pods`

- Deploy deply.yaml which deploys ghost on k8s.
  make sure to change this </br> 
  `value: <---url-of-website--->` </br>
  url of website should be the domain name for ghost


- `kubectl get pods`</br>
   You will see blog pod coming up /</br>
   `kubectl get svc`</br>
   Take the external ip from load balancer service and add it to dns
   to map it to domain name used above.

-   make sure to change this </br> 
   `host: <---domain-of-website--->` </br>
    domain name for ghost </br>
    Once its done run </br>
    `kubectl apply -f ingress.yml`

-  https certificate setup </br>
   make sure to change this </br> 
   `email: <---issuer-email-id--->`</br> 
   email id to which the letsencrypt certificate will be issued.</br>
   `kubectl apply -f  cert-issuer.yml`</br>
   This apply https to your domain name.

