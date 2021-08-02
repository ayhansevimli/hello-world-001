# Helm Chart Installation for Example

        C:\Utils\DevOps\Containerisation\helm

        helm create hello-world-001
        
        dir hello-world-001

--------------------------------------------------------------------------------------------------        
        Directory of C:\Utils\DevOps\Containerisation\helm\hello-world-001
        
        02/08/2021  12:39    <DIR>          .
        02/08/2021  12:39    <DIR>          ..
        02/08/2021  12:39               349 .helmignore
        02/08/2021  12:39             1,151 Chart.yaml
        02/08/2021  12:39    <DIR>          charts
        02/08/2021  12:39    <DIR>          templates
        02/08/2021  12:39             1,882 values.yaml
               3 File(s)          3,382 bytes
               4 Dir(s)  219,102,937,088 bytes free
--------------------------------------------------------------------------------------------------        
* Understanding helm files

        Chart.yaml: This is the main file that contains the description of our chart
        values.yaml: this is the file that contains the default values for our chart
        templates: This is the directory where Kubernetes resources are defined as templates
        charts: This is an optional directory that may contain sub-charts
        .helmignore: This is where we can define patterns to ignore when packaging (similar in concept to .gitignore)
--------------------------------------------------------------------------------------------------
* Verify that the chart is well-formed
        
        helm lint ./hello-world-001

        ==> Linting ./hello-world-001
        [INFO] Chart.yaml: icon is recommended
        1 chart(s) linted, 0 chart(s) failed
--------------------------------------------------------------------------------------------------
* Render chart templates locally and display the output.
        
        helm template hello-world-001
        
--------------------------------------------------------------------------------------------------
* Helm Install
        
        helm install hello-world-001 ./hello-world-001

--------------------------------------------------------------------------------------------------
* Check Installation

        helm list --all 

        kubectl get deployment

        kubectl get pod

        kubectl get replicaset

        kubectl get service
        
        kubectl get pv
        
        minikube service list
--------------------------------------------------------------------------------------------------
* Access Application

        minikube service list

        minikube service hello-world-001
        
----------------------------------------------------------------------------------------------------------------------
* Upgrades a release to a new version of a chart.

//Before running this command let's change replica count to 5 into the values.yaml

        helm upgrade hello-world-001 ./hello-world-001
        
        Release "hello-world-001" has been upgraded. Happy Helming!
        NAME: hello-world-001
        LAST DEPLOYED: Mon Aug  2 13:13:07 2021
        NAMESPACE: default
        STATUS: deployed
        REVISION: 2

----------------------------------------------------------------------------------------------------------------------
* Helm Rollback

        helm rollback hello-world-001 1
        Rollback was a success! Happy Helming!

----------------------------------------------------------------------------------------------------------------------
* To show you a list of all deployed releases.
        
        helm list --all 
        # or
        helm ls
----------------------------------------------------------------------------------------------------------------------
* Uninstall chart & Cleanup

        helm uninstall hello-world-001
        
        kubectl delete pvc --all
        
        helm list --all
        
        kubectl get deployment

        kubectl get pod -o wide

        kubectl get replicaset

        kubectl get service

        kubectl get pv
        
        minikube service list

----------------------------------------------------------------------------------------------------------------------
* Packaging Chart
// To package a chart into a versioned chart archive file.

        helm package hello-world-001

        Successfully packaged chart and saved it to: C:\Utils\DevOps\Containerisation\helm\hello-world-001-0.1.0.tgz
----------------------------------------------------------------------------------------------------------------------
* Helm Repo
// Create index.yaml for chart repo:.

        helm repo index hello-world-001/ --url https://github.com/ayhansevimli/helm-hello-world-001
        
// Push the chart to remote repo:.
        
        helm repo index hello-world-001/ --url https://github.com/ayhansevimli/helm-hello-world-001

----------------------------------------------------------------------------------------------------------------------
----------------------------------------------------------------------------------------------------------------------

