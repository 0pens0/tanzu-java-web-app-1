k8s_custom_deploy(
    'tanzu-java-web-app',
    apply_cmd="tanzu apps workload apply -f config/workload.yaml --debug --live-update" +
               " --local-path ." + 
               " --source-image harbor.tanzuworld.com/tap-packages/tanzu-java-web-app" +
               " --namespace apps" + 
               " --yes " +
               "> /dev/null" +
               " && kubectl get workload tanzu-java-web-app --namespace apps -o yaml",
    delete_cmd="tanzu apps workload delete -f config/workload.yaml --namespace apps --yes",
    deps=['pom.xml', './target/classes'],
    container_selector='workload',
    live_update=[
      sync('./target/classes', '/workspace/BOOT-INF/classes')
    ]
)

k8s_resource('tanzu-java-web-app', port_forwards=["8080:8080"],
            extra_pod_selectors=[{'serving.knative.dev/service': 'tanzu-java-web-app'}])
allow_k8s_contexts('tap-cnapp-demo')
