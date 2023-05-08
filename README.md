# Kubernetes: Resource-management

En Kubernetes, los límites de recursos para los pods se establecen en términos de CPU y memoria. Estos límites se definen usando abreviaciones para indicar la cantidad de recursos asignados a un pod.

`CPU`: La unidad básica para la asignación de CPU en Kubernetes es el milicore (m). Un milicore es igual a una milésima parte de un core de CPU. Por lo tanto, si quieres asignar 1 core de CPU a un pod, debes establecer el límite de CPU en 1000m. Si deseas asignar medio core, puedes establecer el límite de CPU en 500m.

`Memoria`: La unidad básica para la asignación de memoria en Kubernetes es el byte (B), pero se utilizan múltiplos de bytes para expresar cantidades más grandes. Algunas de las abreviaciones comunes son:

- Gi: Gigabyte (1024 megabytes).
- Mi: Megabyte (1024 kilobytes).
- Ki: Kilobyte (1024 bytes).

## Example

En el siguiente manifiesto de kubernetes tenemos 3 pods de nginx cada uno com 3000m => 3 core de CPU, así mismo contamos con una cantidad de 1G de memoria ram por cada tipo de unidad de medida de almacenamiento:

- 1Gi       => 1G de memoria ram.
- 1024Mi    => 1G de memoria ram.
- 2097152Ki => 1G de memoria ram.

```
apiVersion: v1
kind: Pod
metadata:
  name: example-1
spec:
  containers:
  - name: app
    image: nginx:latest
    resources:
      requests:
        memory: "1Gi"
        cpu: "3000m"
      limits:
        memory: "2Gi"
        cpu: "4000m"
---
apiVersion: v1
kind: Pod
metadata:
  name: example-2
spec:
  containers:
  - name: app
    image: nginx:latest
    resources:
      requests:
        memory: "1024Mi"
        cpu: "3000m"
      limits:
        memory: "2048Mi"
        cpu: "4000m"
---
apiVersion: v1
kind: Pod
metadata:
  name: example-3
spec:
  containers:
  - name: app
    image: nginx:latest
    resources:
      requests:
        memory: "1048576Ki"
        cpu: "3000m"
      limits:
        memory: "2097152Ki"
        cpu: "4000m"
```

Para poder visualizar la cantidad total en porcentajes de recursos utilizados dentro de cada nodo utilizamos el siguiente comando:

    kubectl describe node <Nombre del nodo>
    
Y de esta manera podremos repartir la cantidad de recursos que tengamos en nuestros clusters de Kubernetes.

### Referencias

- https://www.info-computer.com/blog/mb-gb-y-tb/
- https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/
