# Azure-PV-PVC-fileshare


# Azure-File-Share-In-AKS
Azure File Share in AKS
```
kubectl create secret generic azure-secret --from-literal=azurestorageaccountname=$AKS_PERS_STORAGE_ACCOUNT_NAME --from-literal=azurestorageaccountkey=$STORAGE_KEY
```

```
IF NOT USING AKS : iNSTALL THE CSI DRIVER FOR AZURE SPECIFICALLY

1. Install Helm (if you haven’t yet)

Run on your control node:

curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
helm version


You should see Helm v3+.

2. Add the Helm repo for Azure File CSI Driver
helm repo add azurefile-csi-driver https://raw.githubusercontent.com/kubernetes-sigs/azurefile-csi-driver/master/charts
helm repo update

3. Install the driver into kube-system namespace
helm install azurefile-csi azurefile-csi-driver/azurefile-csi-driver \
  --namespace kube-system \
  --create-namespace \
  --set controller.nodeSelector."kubernetes\.io/os"=linux \
  --set node.nodeSelector."kubernetes\.io/os"=linux


(You may need additional --set values depending on your Azure version, but this is a good start.)

4. Verify installation
kubectl -n kube-system get pods -l app.kubernetes.io/name=azurefile-csi-driver
kubectl get csidrivers | grep file.csi.azure.com
```


```
kubectl apply -f pv-fileshare.yaml
```
```
kubectl apply -f pvc-fileshare.yaml
```
```
kubectl apply -f test-deployment.yaml
```
