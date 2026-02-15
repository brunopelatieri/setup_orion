Este é um modelo de **README.md** profissional, estruturado para o GitHub, focado na implementação técnica do MinIO com Docker/Portainer e automação via CLI.

---

# 🛡️ MinIO S3 Self-Hosted: Infraestrutura & Automação

Este repositório contém as diretrizes para implantação do **MinIO (Object Storage S3)** utilizando Docker, com foco em performance, limites de recursos e automação via linha de comando para contornar as limitações da interface gráfica nas versões recentes.

---

## 🚀 Configuração de Infraestrutura (Portainer/Docker)

Para garantir que o serviço não consuma recursos excessivos do servidor, utilizamos limites de hardware via `deploy resources`.

### Adicionar Docker Compose Exemplo

```yaml
version: '3.8'

services:
  minio:
    .
    .
    .
    deploy:
      resources:
        limits:
          memory: 1G    # Teto máximo de RAM
        reservations:
          memory: 512M  # Reserva mínima garantida
.
.
.

```

---

## 🛠️ Automação via Terminal (SetupOrion `mc`)

Como as novas versões do MinIO Community limitam o gerenciamento via UI, utilizamos o **MinIO Client (`mc`)** para operações administrativas rápidas.

### 1. Configurar Conexão (Alias)

Crie um atalho para o seu servidor local:

```bash
mc alias set local http://localhost:9000 SEU_USUARIO SUA_SENHA

```

### 2. Criação de Buckets (Comandos "Ocultos")

Crie buckets instantaneamente sem abrir o navegador:

```bash
# Criar o bucket
mc mb local/nome-do-bucket

# Listar buckets existentes
mc ls local/

```

### 3. Gestão de Permissões

Defina o acesso ao bucket (ex: para uso em sites ou apps que precisam de link direto):

```bash
# Tornar o bucket público (Somente leitura)
mc anonymous set download local/nome-do-bucket

```
> **Dica:** Se precisar migrar dados entre buckets ou servidores, use o comando `mc mirror`. É a forma mais rápida de sincronizar arquivos em alta performance.
---

## 📈 Melhores Práticas de Monitoramento

* **Logs:** Verifique a integridade com `docker logs -f minio_server`.
* **Portainer:** Utilize a aba **Stats** no Portainer para validar se o container está respeitando o limite de `1GB` definido no Compose.
* **n8n Integration:** Utilize o nó de S3 no n8n apontando para a porta `9000` para automatizar o upload de arquivos gerados pelo **DiretorIA App**.

---

## 🤝 Créditos e Atribuições

Este projeto utiliza ferramentas e scripts de instalação baseados no **SetupOrion**, otimizando o fluxo de trabalho de desenvolvedores que buscam agilidade no deploy de ferramentas Open Source.

---

## 🖋️ Autor

**Bruno Pelatieri Goulart** 🌐 [brunogoulart.com.br](https://brunogoulart.com.br)



