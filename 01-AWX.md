# AWX

```
Setup AWX
https://www.server-world.info/en/note?os=CentOS_Stream_9&p=ansible&f=9
git clone https://github.com/ansible/awx-operator.git
cd awx-operator
git checkout 2.19.0
export NAMESPACE=awx-app
make deploy
kubectl get pods -n $NAMESPACE
cp awx-demo.yml ansible-awx.yml
kubectl config set-context --current --namespace=$NAMESPACE
kubectl apply -f ansible-awx.yml
kubectl logs -f deployments/awx-operator-controller-manager -c awx-manager
kubectl get secret awx-app-admin-password -o jsonpath="{.data.password}" | base64 --decode; echo

---
apiVersion: awx.ansible.com/v1beta1
kind: AWX
metadata:
  name: awx-app
  annotations:
    networking.gke.io/load-balancer-type: "External"
spec:
  service_type: LoadBalancer
  postgres_data_volume_init: true
  postgres_configuration_secret: external-postgres-secret

---
apiVersion: v1
kind: Secret
metadata:
  name: external-postgres-secret
  namespace: awx-nprd
stringData:
  host: "10.83.192.2"
  port: "5432"
  database: "awx"
  username: "awx"
  password: "awx"
  sslmode: prefer
  target_session_attrs: read-write
  type: unmanaged
type: Opaque


Create Org/Teams/Users
add Credentials > Projects > Templates (job/workflow)
create Schedules

---
- name: Hello World Playbook
  hosts: all
  tasks:
    - name: Print a message
      ansible.builtin.debug:
        msg: "Hi! AWX is working, Hello World!"
    
    - name: Hello
      shell: echo test


Noti for AWX
Name + Org + Type Slack
Channel + Token and Custom
Slack > New app > Create app from manifest > OAuth & Permissions (Scope chat:write)
Get Bot Token and add AWX app into Slack
integrate slack on awx how to

Destroy AWX
kubectl delete namespace awx-app
```