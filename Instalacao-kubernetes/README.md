# Kong + Konga

## 🚀 Começando

Essas instruções permitirão que você fazer o deploy desse ambiente no Kubernetes.

#### Arquitetura
![Diagrama](/images/Diagrama-kong.png)

### 📋 Pré-requisitos

De que coisas você precisa para instalar o software e como instalá-lo?

```
Cluster Kubernetes 
Helm 3
```

### 🔧 Instalação Kong

Para execução do projeto é necessario os seguintes passos para ter o ambiente de desenvolvimento em execução.

Faça:

```
helm repo add bitnami https://charts.bitnami.com/bitnami
```
```
helm repo update
```

```
kubectl create namespace kong-dev
```

Criar secret para o ACR Azure
```
kubectl create namespace kong-dev \
kubectl create secret docker-registry kong-acr \
--namespace kong-dev \
--docker-server=<Registry>.azurecr.io \
--docker-username=user \
--docker-password=pass
```

```
helm install -n kong-dev kong bitnami/kong \
--set service.type=LoadBalancer \
--set image.registry=atqipp.azurecr.io \
--set image.repository=kong-infra \
--set image.tag=2.8.0 \
--set image.pullSecrets='{"name","kong-acr"}' -f values.yaml \
-f values.yaml 

<!-- --set postgresql.image.tag= \ -->

helm template bitnami/kong
```
### 🔧 Instalação Konga
```
kubectl apply -f konga.yaml

```

## 📦 Desenvolvimento

Adicione notas adicionais sobre como implantar isso em um sistema ativo

## 🛠️ Construído com

Mencione as ferramentas que você usou para criar seu projeto

* [docker](http://www.dropwizard.io/1.0.2/docs/) - O framework web usado
* [helm](https://rometools.github.io/rome/) - Usada para gerar RSS
* [kubernetes](https://rometools.github.io/rome/) - Usada para gerar RSS


## ✒️ Autores

Mencione todos aqueles que ajudaram a levantar o projeto desde o seu início

* **THIAGO DOS SANTOS** - *Documentação* - [fulanodetal](https://github.com/linkParaPerfil)

Você também pode ver a lista de todos os [colaboradores](https://github.com/usuario/projeto/colaboradores) que participaram deste projeto.

## 📄 Licença

Este projeto está sob a licença (sua licença) - veja o arquivo [LICENSE.md](https://github.com/usuario/projeto/licenca) para detalhes.

## 🎁 Expressões de gratidão

* Conte a outras pessoas sobre este projeto 📢
* Convide alguém da equipe para uma cerveja 🍺 
* Obrigado publicamente 🤓.
* etc.


---
⌨️ com ❤️ por [Thiago dos Santos](https://gist.github.com/Thiagosnts) 😊
