DESAFÍO 15 – Miriam Romitelli | HELM CHART & GITOPS

HELM.
Se convierten los distintos archivos de manifiesto creados del desafío 14 –KUBERNETES, en un paquete de Helm.
Tomando en cuenta el archivo de manifiesto values.yaml.

El archivo values.yaml = deployment.yaml (cambia nombre / mismo contenido)
y en la carpeta templates se colocó el archivo my-app-config.yaml del desafio 14.

$ helm package /directorio      para la creación del paquete HelmChart


ARGO:
$ microk8s kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml      para correr argocd
$ micork8s kubectl get all -n argocd 
Se toma la IP del argocd-server para abrir en el navegador.

Creación de una APPS OF APPS, que apunte a la aplicación convertida en un Helm chart; con la siguiente configuración:
Self healing: habilitado
Autosync: habilitado.

Logueo aplicación cli Argo: $ argocd login ipserver.

Creacion de la aplicación apps of apps desde argo cli
argocd app create demo-app --repo https://github.com/mromitelli/Desafio15.git --path . --dest-server https://kubernetes.default.svc --dest-namespace default
utilizando los archivos de manifiesto del desafio 15 (helm):https://github.com/mromitelli/Desafio15.git

Comprobación en consola: $ micork8s kubectl get all

Crear una APPS OF APPS, que apunte a los archivos de manifiesto normales (sin Helm); con la siguiente configuración:
Self healing: deshabilitado.
Autosync: manual.
utilizando los archivos de manifiesto del desafio 14: https://github.com/mromitelli/Desafio14.git

Comprobación en consola: $ micork8s kubectl get all


