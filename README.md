<div align="center">

# ☸️ GUÍA COMPLETA DE KUBERNETES (K8s) 🚀
### *De Cero a Producción: Orquestación, Despliegue y Gestión de Contenedores*

[![Kubernetes](https://img.shields.io/badge/Kubernetes-v1.37-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)](https://kubernetes.io/)
[![Minikube](https://img.shields.io/badge/Minikube-v1.39-2496ED?style=for-the-badge&logo=kubernetes&logoColor=white)](https://minikube.sigs.k8s.io/)
[![Ubuntu](https://img.shields.io/badge/Ubuntu-26.04-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)](https://ubuntu.com/)
[![Docker](https://img.shields.io/badge/Docker-Driver-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![VirtualBox](https://img.shields.io/badge/VirtualBox-Hypervisor-183A61?style=for-the-badge&logo=virtualbox&logoColor=white)](https://www.virtualbox.org/)

<p align="center">
  <b>Manual práctico, apuntes y laboratorio paso a paso de Kubernetes para administración de sistemas en entornos locales y productivos.</b>
</p>

---

</div>

## 📖 Tabla de Contenidos

A continuación se detalla la estructura y los módulos que componen este repositorio formativo:

| Módulo | Título | Descripción | Estado |
| :---: | :--- | :--- | :---: |
| **01** | [📘 1. Introducción a Kubernetes](1.md) | Fundamentos de la orquestación, evolución (Bare Metal, VM, Contenedores), arquitectura del clúster (Control Plane & Workers) y modelo declarativo. | <kbd>🟢 Completado</kbd> |
| **02** | [⚙️ 2. Instalación y Configuración](2.md) | Despliegue paso a paso de Minikube en Ubuntu con **VirtualBox** y **Docker**, instalación de `kubectl`, autocompletado y ciclo de vida. | <kbd>🟢 Completado</kbd> |
| **03** | [📦 3. Pods](3.md) | Unidad atómica de K8s, anatomía de un manifiesto YAML, ciclo de vida, múltiples contenedores, almacenamiento compartido y sondas de salud. | <kbd>🟡 En progreso</kbd> |
| **04** | [🔄 4. ReplicaSets](4.md) | Escalabilidad horizontal, selectores de etiquetas (*labels* & *selectors*) y mecanismos nativos de auto-recuperación (*self-healing*). | <kbd>⚪ Pendiente</kbd> |
| **05** | [🚀 5. Deployments](5.md) | Gestión de versiones, despliegues continuos sin caída de servicio (*Rolling Updates*), estrategias de actualización y *Rollbacks*. | <kbd>⚪ Pendiente</kbd> |

---

## 🏗️ Arquitectura Básica del Clúster

```
                     🌐 [ Cliente / Administrador (kubectl) ]
                                      │
                                      ▼
             ┌──────────────────────────────────────────────────┐
             │            👑 CONTROL PLANE (Master)             │
             │  ┌─────────────────┐        ┌──────────────────┐ │
             │  │  kube-apiserver │ ◄────► │       etcd       │ │
             │  └────────┬────────┘        └──────────────────┘ │
             │           │                                      │
             │     ┌─────┴──────────────┐                       │
             │     ▼                    ▼                       │
             │ ┌───────────────┐  ┌───────────────────────────┐ │
             │ │ kube-scheduler│  │  kube-controller-manager  │ │
             │ └───────────────┘  └───────────────────────────┘ │
             └─────────────────────────┬────────────────────────┘
                                       │
                 ┌─────────────────────┴─────────────────────┐
                 │                                           │
                 ▼                                           ▼
  ┌───────────────────────────────┐           ┌───────────────────────────────┐
  │       🛠️ WORKER NODE 1        │           │       🛠️ WORKER NODE 2        │
  │ ┌───────────┐   ┌───────────┐ │           │ ┌───────────┐   ┌───────────┐ │
  │ │  kubelet  │   │kube-proxy │ │           │ │  kubelet  │   │kube-proxy │ │
  │ └─────┬─────┘   └─────┬─────┘ │           │ └─────┬─────┘   └─────┬─────┘ │
  │       │               │       │           │       │               │       │
  │ ┌─────▼───────────────▼─────┐ │           │ ┌─────▼───────────────▼─────┐ │
  │ │ Container Runtime (CRI)   │ │           │ │ Container Runtime (CRI)   │ │
  │ │ (containerd / CRI-O)      │ │           │ │ (containerd / CRI-O)      │ │
  │ └───────────────────────────┘ │           │ └───────────────────────────┘ │
  │   📦 [Pod]   📦 [Pod]         │           │   📦 [Pod]   📦 [Pod]         │
  └───────────────────────────────┘           └───────────────────────────────┘
```

---

## 🛠️ Herramientas y Requisitos del Entorno

Para replicar este laboratorio en local se requiere:

* **Sistema Operativo:** Ubuntu Linux (22.04 LTS / 24.04 LTS / posterior).
* **Hipervisor / Motor de Contenedores:**
  * 📦 **Docker Engine:** Para despliegue ultra-rápido mediante `minikube start --driver=docker`.
  * 🖥️ **Oracle VirtualBox:** Para entornos completamente aislados mediante `minikube start --driver=virtualbox`.
* **Herramientas de Control:**
  * 🎛️ **Minikube:** v1.39+
  * ⌨️ **Kubectl:** v1.37+
  * 🐚 **Bash:** Con autocompletado y alias activados.

---

## ⚡ Comandos de Referencia Rápida

```bash
# 🚀 Iniciar clúster
minikube start --driver=docker

# 📊 Comprobar estado y nodos
minikube status
kubectl get nodes -o wide

# 🌐 Abrir Dashboard gráfico interactivo
minikube dashboard

# 🛑 Detener y limpiar clúster
minikube stop
minikube delete --all
```

---

<div align="center">

### 👨‍💻 Autor & Entorno
**Antonio Montaño**  
*Administración de Sistemas Informáticos en Red (2º ASIR)*  

⭐ *¡Si este repositorio te resulta útil para aprender Kubernetes, no olvides dejarle una estrella!* ⭐

</div>
