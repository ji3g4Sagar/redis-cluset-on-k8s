# 如何在k8s中建立redis cluster 紀錄

## yaml建立順序
1. redis-pv.yaml (只有PV一定要先建立)
2. redis-storageclass.yaml
3. redis-sts.yaml
4. redis-svc.yaml

## 建立完成後，利用下面這句把redis cluster建立起來
### __如果原本就有pv 記得要清空__
* cluster reset
* flushdb

### kubectl exec -it redis-app-0 -- redis-cli -h localhost -a <your own password if had> --cluster create --cluster-replicas 1 $(kubectl get pods -l app=redis-cluster -o jsonpath='{range.items[*]}{.status.podIP}:6379 ')



### 其中 app=redis-cluster 要對應statefulset的值