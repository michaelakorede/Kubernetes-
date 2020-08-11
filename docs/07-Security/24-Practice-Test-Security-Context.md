# Practice Test - Security Context
  - Take me to [Video Tutorial](https://kodekloud.com/courses/539883/lectures/9816674)
  
Solutions to practice test - security context
- Run the command 'kubectl exec ubuntu-sleeper whoami' and count the number of pods.
  ```
  $ kubectl exec ubuntu-sleeper whoami
  ```
- Set a security context to run as user 1010.
  ```
  $ kubectl get pods ubuntu-sleeper -o yaml > ubuntu.yaml
  $ kubectl delete pod ubuntu-sleeper
  $ vi ubuntu.yaml ( add securityContext Section)
    securityContext:
      runAsUser: 1010
  $ kubectl create -f ubuntu.yaml
  ```
- The User ID defined in the securityContext of the container overrides the User ID in the POD.
 
- The User ID defined in the securityContext of the POD is carried over to all the PODs in the container.

- Run kubectl exec -it ubuntu-sleeper -- date -s '19 APR 2012 11:14:00'
  ```
  $ kubectl exec -it ubuntu-sleeper -- date -s '19 APR 2012 11:14:00'
  ```
- Add SYS_TIME capability to the container's securityContext
  ```
  $ kubectl get pods ubuntu-sleeper -o yaml > ubuntu.yaml
  $ kubectl delete pod ubuntu-sleeper
  $ vi ubuntu.yaml
  
  Under container section add the below
  
  securityContext:
      capabilities:
        add: ["SYS_TIME"]
        
  $ kubectl create -f ubuntu.yaml
  ```
  
 - Now try to run the below command in the pod to set the date. If the security capability was added correctly, it should work. If it doesn't make sure you changed the user back to root.
   ```
   $ kubectl exec -it ubuntu-sleeper -- date -s '19 APR 2012 11:14:00'
   ```
   
   