<table align="center">
  <tr>
    <td>
      <img height="150" src="./assets/girafa.png" alt="Giraffe Kubernetes">
    </td>
    <td>
      <h1 align="center">Desafio Jack Experts</h1>
    </td>
    <td>
      <img height="150" src="./assets/girafa.png" alt="Giraffe Kubernetes">
    </td>
  </tr>
</table>
---

## Sobre o Projeto

Este projeto faz parte do **Desafio Jack Experts**, no qual o objetivo é desenvolver uma aplicação simples utilizando Docker, Helm e Kubernetes. A aplicação serve uma página HTML que pode ser customizada via ConfigMap no Kubernetes. Além disso, a aplicação é gerenciada através de Helm Charts, garantindo uma fácil instalação e manutenção. A imagem Docker é construída sem privilégios de root, aumentando a segurança da aplicação.

---

## Requisitos Atendidos no Desafio

1. **Uso de repositório Git** com Dockerfile e Helm.
2. **Imagem Docker** construída e publicada no Docker Hub: `laynon/desafio`.
3. A imagem **não roda como root**.
4. A página HTML é **configurável via ConfigMap**.
5. O **Helm** define todos os objetos Kubernetes necessários (Deployment, Service, Ingress, ConfigMap).
6. Todos os objetos possuem a **label** `desafio=jackexperts`.

---

## Como Rodar o Projeto na Sua Máquina

### Requisitos

- **Docker** instalado.
- Um **cluster Kubernetes** local ou remoto:
  - Você pode usar **Minikube**, **K3s** ou **K3d** para rodar o Kubernetes localmente.
- **Helm** instalado para gerenciamento dos charts Kubernetes.
- **Kubectl** para interagir com o cluster.

### Passo a Passo

1. **Clone o Repositório**:
   ```bash
   git clone https://github.com/DI-NS/desafio_jack.git
   cd desafio_jack
   ```

2. **Subir o Cluster Kubernetes** (utilizando Minikube como exemplo):
   ```bash
   minikube start
   ```

3. **Construir a Imagem Docker**:
   Se você deseja construir a imagem localmente:
   ```bash
   docker build -t laynon/desafio .
   ```

   Caso queira utilizar a imagem já publicada no Docker Hub:
   ```bash
   docker pull laynon/desafio
   ```

4. **Instalar a Aplicação com Helm**:
   ```bash
   helm install desafio ./desafio
   ```

5. **Rodar o Minikube Tunnel** (necessário para acessar o Ingress):
   
   Se você estiver utilizando Minikube, execute o comando abaixo para expor os serviços do Kubernetes externamente. Isso irá criar rotas que permitem o acesso à aplicação pelo domínio configurado no Ingress.
   ```bash
   minikube tunnel
   ```

6. **Acessar a Aplicação**:
   Verifique se o Ingress está configurado corretamente. Use o seguinte comando para obter os detalhes de acesso:
   ```bash
   kubectl get ingress
   ```

---

## Estrutura do Projeto

O projeto é dividido nas seguintes partes principais:

- **Dockerfile**: Define como a imagem Docker é construída, utilizando NGINX para servir a aplicação.
- **custom_nginx.conf**: Arquivo de configuração customizada do NGINX.
- **Helm Charts**: Gerenciam o deploy da aplicação no Kubernetes, incluindo templates para **Deployment**, **Service**, **Ingress** e **ConfigMap**.
- **ConfigMap**: Define o conteúdo customizável da página HTML servida pela aplicação.

---

## Pipeline CI/CD

O projeto inclui um pipeline CI/CD configurado via **GitHub Actions**. Esse pipeline realiza as seguintes etapas:

1. **Build da Imagem Docker**: A imagem é construída e testada.
2. **Push para o Docker Hub**: Após a validação, a imagem é enviada para o Docker Hub.

O pipeline automatiza o processo de build e deploy, garantindo que a versão mais recente da aplicação esteja sempre disponível.

---

## Como Navegar no Projeto

Aqui está um rápido guia de como se localizar no projeto:

- **Raiz do projeto**:
  - **Dockerfile**: Definição da imagem Docker.
  - **custom_nginx.conf**: Configuração do NGINX.
  - **desafio/**: Diretório contendo o Helm Chart e templates Kubernetes.

- **desafio/templates/**:
  - **deployment.yaml**: Template para o Deployment Kubernetes.
  - **service.yaml**: Template para o Service.
  - **ingress.yaml**: Template para o Ingress.
  - **configmap.yaml**: Template para o ConfigMap (customização da página HTML).

Utilize esses arquivos como ponto de partida para entender e modificar a aplicação.
