## fluxcd demo

### 与ArgoCD的差异
1. Flux2 のほうが後発なだけあって、よく使うオプション機能をうまくCRD設計に溶け込ませている感じがします。
2. ArgoCD ユーザーの権限を制御するために独自 RBAC や OIDC プロバイダを用意しなければならないのは大げさだなと思っていたので、
3. Flux2 の K8s RBAC で権限管理を行うという設計は個人的に好みです。
4. ただし Flux2 には、GUIダッシュボードや App Diff に相当する機能が無いので、その辺りが重要になる場合はFlux2ではなくArgoCDを選択することになります。

### 相关command
1. 检查配置是否生效 `kubectl get gitrepository`
2. 检查配置是否生效 `kubectl get kustomization`
3. 查看触发重新部署 `kubectl describe kustomization hello-world-flask`

### 步骤
1. 为 FluxCD 创建仓库连接信息 `fluxcd-repo.yaml`
2. 将 GitRepository 对象部署到集群内 `kubectl apply -f fluxcd-repo.yaml`
3. 为 FluxCD 创建部署策略 `fluxcd-kustomize.yaml`
4. 将 Kustomization 对象部署到集群内 `kubectl apply -f fluxcd-kustomize.yaml`

### 直观感受
本地修改`deployment.yaml` 并且推送到代码仓库后，集群会监听Git仓库变化，自动进行部署