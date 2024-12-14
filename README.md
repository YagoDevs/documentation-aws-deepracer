# Guia de Acesso e Treinamento no DeepRacer for Cloud

**Autor:** Yago Phellipe  
**Curso:** Ciência da Computação  

Este guia explica como acessar e treinar o carrinho no ambiente do DeepRacer for Cloud, utilizando o servidor **Shrek2**.

---

## Acesso ao DeepRacer for Cloud

1. **Baixe o MobaXterm:**
   - Acesse o site oficial do MobaXterm e instale a ferramenta.

2. **Conecte-se ao servidor:**
   - Abra o MobaXterm e conecte-se ao servidor via SSH com o comando:
     ```bash
     ssh -L 8888:localhost:8888 deepracer@10.8.8.10
     ```
   - Insira a senha fornecida para o perfil `deepracer`.

3. **Acesse o repositório do DeepRacer:**
   - Verifique o repositório com o comando:
     ```bash
     ls
     ```
   - Entre no diretório:
     ```bash
     cd deepracer-for-cloud
     ```
   - Configure os arquivos customizados para o seu grupo:
     ```bash
     ln -s custom_files4 custom_files
     ln -s system4.env system.env
     ```
   - Ative o ambiente de treinamento:
     ```bash
     source bin/activate.sh run4.env
     ```

---

## Seleção de Pistas

1. Abra o arquivo `run4.env` para editar a variável `DR_WORLD_NAME`:
   ```bash
   nano run4.env
   ```
2. Altere o valor para a pista desejada, salve e reative o ambiente:
   ```bash
   source bin/activate.sh run4.env
   ```

---

## Seleção de Modelos de RL

1. Acesse a pasta de arquivos customizados:
   ```bash
   cd custom_files4
   ```
2. Edite o arquivo `model_metadata.json`:
   ```bash
   nano model_metadata.json
   ```
3. Altere o valor da chave `training_algorithm` para o modelo desejado, salve e atualize os arquivos:
   ```bash
   dr-update && dr-update-env && dr-upload-custom-files
   ```

---

## Ajuste de Hiperparâmetros

1. Edite o arquivo `hyperparameters.json`:
   ```bash
   nano hyperparameters.json
   ```
2. Modifique os hiperparâmetros desejados, salve e atualize os arquivos:
   ```bash
   dr-update && dr-update-env && dr-upload-custom-files
   ```

---

## Seleção de Caixas de Colisão

1. Edite o arquivo `run4.env`:
   ```bash
   nano run4.env
   ```
2. Modifique o campo `DR_RACE_TYPE` para `OBJECT_AVOIDANCE` ou `HEAD_TO_BOT`, conforme necessário, e salve o arquivo.

---

## Visualização de Variáveis de Ambiente

- Utilize o comando `cat` para visualizar diretamente o conteúdo do arquivo:
  ```bash
  cat run4.env
  ```
- Ou use o comando `nano` para abrir e editar o arquivo:
  ```bash
  nano run4.env
  ```
---

## Início do Treinamento

1. Certifique-se de que todas as configurações estão atualizadas:
   ```bash
   dr-update && dr-update-env && dr-upload-custom-files
   ```
2. Inicie o treinamento com o comando:
   ```bash
   dr-start-training -w
   ```
3. Acompanhe o progresso do treinamento no terminal ou nos gráficos disponíveis no painel.

---

## Realização de Evaluation

1. Para realizar uma avaliação, selecione o modelo treinado no painel do DeepRacer.
2. Execute o comando para iniciar a avaliação:
   ```bash
   dr-start-evaluate
   ```
3. Escolha a pista desejada e acompanhe os resultados gerados.

---

## Realização de Deploy

1. **Escolha o modelo treinado:**

   - Para realizar o deploy do modelo treinado no carrinho, escolha  o modelo que foi gerado a partir do evaluate e baixe-o para o seu computador.
   

2. **Realize o deploy:**

   - Após baixar o modelo, basta conectar o carrinho ao computador e realizar o upload do modelo para o carrinho. Com isso, o modelo estará pronto para ser utilizado no carrinho.

---

## Continuidade de Treinamento entre Pistas

Para continuar o treinamento de uma pista A para uma pista B, siga os passos abaixo:

1. Altere a variável `DR_WORLD_NAME` no arquivo `run4.env` para a nova pista.
2. Atualize os arquivos customizados:
   ```bash
   dr-update && dr-update-env && dr-upload-custom-files
   ```
3. Reinicie o treinamento com o comando:
   ```bash
   dr-start-training -w
   ```
Isso permitirá que o modelo aproveite os aprendizados da pista anterior enquanto treina na nova pista.

