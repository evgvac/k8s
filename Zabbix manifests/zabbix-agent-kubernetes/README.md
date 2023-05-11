# zabbix-agent-kubernetes
Zabbix agent pod for kubernetes with node pool autoscaling support

This yaml file creates a kubernetes DaemonSet with zabbix-agent. It can be also used for node pools which scale up/down. It automatically disables the kubernetes node in zabbix after it scales down, so you will have no alerts and it will keep the history for the node (lines 52-55 in zabbix-agent-kubernetes.yaml, you can delete them if you don't want this feature).

install: 

  1. edit <br>
    >>>EDIT_ZABBIX_SERVER_HOSTNAME<<<< <br>
    >>>EDIT_ZABBIX_SERVER_IP<<<<<br>
    >>>>EDIT_KUBERNETES_NAMESPACE<<<<<br>
    in `zabbix-agent-kubernetes.yaml`
  2. create user "api" in zabbix for API access
  3. create file with zabbix "api" user password: <br>
        `echo "ZABBIX_API_PASSWORD=YOUR_API_PASSWORD" > YOUR_API_PASSWORD_FILE`
  4. `kubectl -n $NAMESPACE create secret generic zabbix-api-secret --from-env-file=YOUR_API_PASSWORD_FILE`
  5. `kubectl apply -f zabbix-agent-kubernetes.yaml`
