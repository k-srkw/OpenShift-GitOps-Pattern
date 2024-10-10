# OpenShift GitOps Pattern

## [Configuration Management](/configuration-management/)

対象リソース : ConfigMap  
対象となる OCP クラスタ、Namespace が複数ある想定で、各環境ごとの ConfigMap を管理する

- Namespace  
    Kustomize を導入し、マニフェストの差分をディレクトリ構成により管理
- OCP クラスタ  
    ディレクトリ構成 / Kustomize Component により管理

### [Direcotry Path Pettern](/configuration-management/dir-path/)

- マニフェストの差分を OCP クラスタ x Namespace ごとのパスで管理
- クラスタレベルの設定変更は各 Namespace ごとに設定が必要 

### [Component Pettern](/configuration-management/components/)

- 各クラスタ固有の設定を Kustomize Component で管理
- 各クラスタ固有の設定と Namespace の設定を分離できる

## [App Deploy with OpenShift Template](/app-deploy-with-template/)

対象リソース : Template  
GitOps で OpenShift Template によるマニフェスト生成を行う

### 通常のデプロイ方法

[Getting Started with JBoss EAP for OpenShift Container Platform](https://docs.redhat.com/ja/documentation/red_hat_jboss_enterprise_application_platform/7.4/html/getting_started_with_jboss_eap_for_openshift_container_platform/build_run_java_app_s2i)

```
$ oc new-project ns-env1
$ oc apply -k overlays/cluster-pt/ns-env-1
$ oc apply -f base/jboss-eap74-openjdk8-openshift-is.yaml
$ oc apply -f base/jboss-eap74-openjdk8-runtime-openshift-is.yaml
$ oc process -f base/eap74-basic-s2i-template.yaml --param-file overlays/cluster-pt/ns-env-1/configs/eap74-basic-s2i-template-param.txt | oc apply -f -
```

### [ArgoCD Config Management Plugin Pettern](/app-deploy-with-template/argocd-cmp/)

ArgoCD の Config Management Plugin により OpenShift Template によるマニフェスト生成処理を追加

### [ArgoCD Config Management Plugin Pettern with Kustomize](/app-deploy-with-template/argocd-cmp-kustomize-template-integration/)

ArgoCD の Config Management Plugin を用いて Kustomize と OpenShift Template を統合しデプロイする

### [Kustomize Plugin Pettern](/app-deploy-with-template/kustomize-plugin/)

kustomize generator plugin により OpenShift Template によるマニフェスト生成処理を追加
