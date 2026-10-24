# 🚀 Laboratório Prático: Automação de Infraestrutura com Cloud-init & Multipass

[![Git Status](https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge&logo=git)](https://github.com/Esparta009boy/lab-cloud-init)
[![Cloud-init](https://img.shields.io/badge/Tecnologia-Cloud--init-orange?style=for-the-badge&logo=linux)](https://cloudinit.readthedocs.io/)
[![Docker](https://img.shields.io/badge/Container-Docker-blue?style=for-the-badge&logo=docker)](https://www.docker.com/)

Repositório dedicado ao laboratório prático de automação de provisionamento de servidores e máquinas virtuais utilizando **Cloud-init** e orquestração de containers. O objetivo central é eliminar processos manuais de configuração (*first-boot configuration*), aplicando conceitos modernos de Infraestrutura como Código (IaC) e engenharia de confiabilidade.

---

## 📋 Proposta e Propósito da Atividade

Em ambientes modernos de TI, a configuração manual de servidores é ineficiente, custosa e propensa a falhas humanas (o famoso problema do *"na minha máquina funciona"*). 

O propósito deste laboratório é desenvolver **receitas declarativas em arquivos YAML (Cloud-init)** capazes de instruir uma instância recém-criada a se autoconfigurar instantaneamente no momento do primeiro boot, garantindo padronização, velocidade e reprodutibilidade absoluta.

---

## 🛠️ O que foi Realizado, Configurado e Implementado

O laboratório foi dividido em três níveis progressivos de automação:

### 🌐 Nível 1: Servidor Web Estático (`nivel1.yaml`)
* **Configuração:** Ativação da atualização automática de pacotes do sistema e instalação do servidor web **Nginx**.
* **Implementação:** Utilização do módulo `write_files` para injetar um arquivo HTML customizado (`/var/www/html/index.html`) com uma página de boas-vindas estruturada.
* **Automação:** Uso do bloco `runcmd` para reiniciar o serviço do Nginx e garantir a leitura imediata da nova página no primeiro boot.

### 🐳 Nível 2: O Container Automático (`nivel2.yaml`)
* **Configuração:** Preparação da infraestrutura base para ambientes conteinerizados, atualizando índices e instalando o pacote oficial `docker.io`.
* **Implementação:** Habilitação e inicialização nativa do serviço Docker via systemctl.
* **Automação:** Execução automática (*detached mode*) da imagem oficial de demonstração (`nginxdemos/hello`), realizando o mapeamento de portas (`8080:80`).

### 📊 Nível 3: Ambiente de Observabilidade e Usuários (`nivel3.yaml`)
* **Configuração:** Provisionamento completo de um ambiente de desenvolvimento e monitoramento.
* **Implementação:** 
  * Criação automatizada do usuário `aluno` com shell padrão Bash.
  * Atribuição de privilégios elevados aos grupos `sudo` e `docker` (com acesso `NOPASSWD:ALL`).
  * Injeção de um arquivo de instruções de boas-vindas em `/home/aluno/bem-vindo.txt` com permissões rigorosas de segurança.
  * Ajuste de propriedade de diretórios via `chown`.
* **Automação:** Subida automatizada de um container de monitoramento e visualização de métricas (**Grafana**) mapeado na porta `3000:3000`.

---

## 🏢 Vantagens e Impactos Positivos em Ambiente Corporativo

A adoção de padrões de automação de infraestrutura como o **Cloud-init** traz benefícios estratégicos cruciais para empresas e equipes de **DevOps / SRE**:

1. **Eliminação de Configurações Manuais (*Zero-Touch Provisioning*):** Reduz o tempo de entrega de servidores de horas para segundos, eliminando o erro humano em instalações de pacotes e dependências.
2. **Infraestrutura Imutável e Reprodutível:** Garante que qualquer ambiente (desenvolvimento, homologação ou produção) seja rigorosamente idêntico, pois toda a receita é baseada em código versionado.
3. **Escalabilidade e Agilidade Operacional:** Permite escalar clusters e instâncias em nuvem sob demanda, com cada novo nó já nascendo pronto para uso, integrado aos grupos de segurança e rodando suas respectivas aplicações ou ferramentas de monitoramento.
4. **Segurança e Conformidade Padronizada:** A criação de usuários, chaves SSH, permissões de diretórios e políticas de acesso é aplicada de forma centralizada desde o nascimento do servidor, atendendo a rigorosos padrões de governança e segurança da informação.

---

## 📂 Estrutura do Repositório

```text
lab-cloud-init/
├── README.md         # Documentação detalhada do projeto
├── nivel1.yaml       # Configuração do Servidor Web Nginx
├── nivel2.yaml       # Automação de Container Docker básico
└── nivel3.yaml       # Ambiente completo com usuário dedicado e Grafana
