# infrastructure-automatis-e-ansible-docker
Projet SAÉ 5.02 - Infrastructure réseau automatisée avec Ansible, Docker, Prometheus et Grafana
# Infrastructure réseau automatisée avec Ansible & Docker (SAÉ 5.02)

Projet de mise en place d’une petite infrastructure réseau entièrement déployée par **Ansible** et basée sur des **conteneurs Docker**.

Services déployés :

- Un serveur **NGINX** de test (client web)
- Un serveur **DHCP** (ISC DHCP en conteneur)
- Un conteneur **client DHCP** de test
- Un serveur **DNS** (**Bind9**) avec zone interne `infra.local`
- Un couple **Prometheus + Grafana** pour la supervision
- Un Portainer déjà présent sur la VM (facultatif pour le projet)

Toute la configuration (rôles, playbooks, fichiers de config) est versionnée dans ce dépôt.

---

## 1. Architecture générale

### 1.1. Composants

- **Ansible**
  - Installation de Docker
  - Création des réseaux Docker
  - Déploiement des conteneurs (NGINX, DHCP, DNS, Prometheus, Grafana, client DHCP)
- **Docker**
  - Un conteneur par service afin d’isoler les rôles réseau
- **Réseaux Docker**
  - `sae502-net` : réseau pour le NGINX de test
  - `dhcp-net` : réseau 10.5.0.0/24 pour le serveur DHCP + client DHCP + DNS
  - `dns-net` : réseau 10.6.0.0/24 pour le serveur DNS
  - `monitor-net` : réseau commun à **Prometheus** et **Grafana**

### 1.2. Arborescence du dépôt

```text
.
├── ansible/
│   ├── inventories/
│   │   └── dev.ini
│   ├── playbooks/
│   │   ├── ping.yml
│   │   ├── install_docker.yml
│   │   ├── deploy_nginx_test.yml
│   │   ├── deploy_dhcp.yml
│   │   ├── test_dhcp_client.yml
│   │   ├── deploy_dns.yml
│   │   ├── deploy_prometheus.yml
│   │   └── deploy_grafana.yml
│   └── roles/
│       ├── docker/
│       ├── nginx_test/
│       ├── dhcp_server/
│       ├── dhcp_client_test/
│       ├── dns_server/
│       ├── prometheus_server/
│       └── grafana_server/
├── docs/
│   └── cahier_des_charges.md
├── ansible.cfg
└── README.md
