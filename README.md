**Implementación de Keycloak con Helm y ArgoCD**

Introducción

Este documento describe cómo implementar Keycloak con Helm y ArgoCD. Keycloak es una plataforma de identidad y acceso (IAM) de código abierto que proporciona una variedad de funciones, como la autenticación, la autorización y la gestión de usuarios. ArgoCD es un sistema de entrega continua y despliegue continuo (CD/CI) para Kubernetes.

Requisitos

Para implementar Keycloak con Helm y ArgoCD, necesitará lo siguiente:

    Un cluster de Kubernetes
    Helm instalado
    ArgoCD instalado

Pasos

    Cree un namespace para Keycloak:

kubectl create namespace hbr-keycloak

    Instale el chart de Keycloak:

helm install keycloak hbr-keycloak/keycloak

    Configure ArgoCD para que supervise el chart de Keycloak:

argocd init
argocd app create keycloak

    Implemente el chart de Keycloak:

argocd sync keycloak

Conexión con la base de datos de Postgres

Para conectarse a la base de datos de Postgres desde el exterior, puede utilizar el comando kubectl exec:

POD_NAME=$(kubectl get pods -n hbr-keycloak -l app=postgres -o jsonpath='{.items[0].metadata.name}')
kubectl exec -it $POD_NAME -n hbr-keycloak -- psql -h localhost -U postgres -p 5432 keycloak

Consola de administración de Keycloak

La consola de administración de Keycloak está disponible en la siguiente URL:

https://localhost:8080

Para iniciar sesión, utilice el nombre de usuario admin y la contraseña admin.

Creación de un usuario y una contraseña para la consola de administración

Para crear un usuario y una contraseña para la consola de administración, siga estos pasos:

    Abra la consola de administración de Keycloak en https://localhost:8080.
    Haga clic en "Administradores".
    Haga clic en "Añadir administrador".
    Introduzca un nombre de usuario y una contraseña.
    Haga clic en "Guardar".

Preguntas frecuentes

    ¿Cómo puedo cambiar el puerto de la consola de administración?

Para cambiar el puerto de la consola de administración, edite el archivo values.yaml del chart de Keycloak y establezca el valor de deployments.keycloak.service.ports.containerPort en el puerto deseado.

    ¿Cómo puedo cambiar la contraseña del administrador?

Para cambiar la contraseña del administrador, abra la consola de administración de Keycloak y vaya a "Administradores". Haga clic en el nombre del administrador y luego en "Cambiar contraseña". Introduzca la nueva contraseña y haga clic en "Guardar".

    ¿Cómo puedo añadir un nuevo usuario a la base de datos de Keycloak?

Para añadir un nuevo usuario a la base de datos de Keycloak, abra la consola de administración de Keycloak y vaya a "Usuarios". Haga clic en "Añadir usuario". Introduzca el nombre de usuario, la contraseña y otros datos necesarios. Haga clic en "Guardar".

Glosario

    Helm: Un sistema de gestión de paquetes para Kubernetes.
    ArgoCD: Un sistema de entrega continua y despliegue continuo para Kubernetes.
    Pod: La unidad básica de ejecución en Kubernetes.
    Secret: Un objeto que almacena datos confidenciales, como contraseñas y claves de cifrado.
    Ingress: Un recurso que permite el tráfico entrante a los servicios de Kubernetes.
    Consola de administración: Una interfaz web que se utiliza para administrar Keycloak.
