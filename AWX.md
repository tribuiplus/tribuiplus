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

Create Org/Teams/Users
add Credentials > Projects > Templates (job/workflow)
create Schedules

Noti for AWX
Name + Org + Type Slack
Channel + Token and Custom
Slack > New app > Create app from manifest > OAuth & Permissions (Scope chat:write)
Get Bot Token and add AWX app into Slack
integrate slack on awx how to
```