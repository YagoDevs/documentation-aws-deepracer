# Guia de Acesso e Treinamento no DeepRacer for Cloud

**Autor:** Yago Phellipe  
**Curso:** Ciência da Computação  

Este é um guia para compreendermos como acessar e treinar no ambiente do DeepRacer-for-Cloud o nosso carrinho no servidor Shrek2.

---

## Acesso ao DeepRacer for Cloud

Para acessar o DeepRacer for Cloud, siga os passos abaixo:

1. **Baixe o MobaXterm:**

   - Acesse o site oficial do MobaXterm e instale a ferramenta em sua máquina.

2. **Abra o terminal e conecte-se ao servidor:**

   - Execute o comando abaixo no terminal do MobaXterm para conectar-se ao servidor via SSH:
     ```bash
     ssh -L 8888:localhost:8888 deepracer@10.8.8.10
     ```
   - Insira a senha fornecida para o perfil `deepracer`.

3. **Acesse o ambiente de treinamento:**

   - Após conectar-se, verifique onde está o repositório do DeepRacer:
     ```bash
     ls
     ```
   - Entre no diretório do DeepRacer:
     ```bash
     cd deepracer-for-cloud
     ```
   - Existe uma pasta customizada para cada grupo, em que podemos colocar e mudar as variáveis de ambiente do modo que queremos. Para isso, precisamos linkar as nossas variáveis de ambiente e os arquivos customizados:
     ```bash
     ln -s custom_files4 custom_files
     ln -s system4.env system.env
     ```
   - Agora, selecione a configuração do ambiente que será utilizada com o comando abaixo:
     ```bash
     source bin/activate.sh run4.env
     ```

---

## Seleção de Pistas

Existem dois arquivos principais para configurar o ambiente: o `run4.env` e o `system4.env`. Para alterar a pista, modifique a variável `WORLD_NAME` no arquivo `run4.env`. Após a alteração, salve o arquivo e execute novamente o comando:
   ```bash
   source bin/activate.sh run4.env
   ```

---

## Seleção de Modelos de RL

Para selecionar o modelo de RL utilizado no treinamento, siga os passos abaixo:

1. Entre na pasta `custom_files4`:
   ```bash
   cd custom_files4
   ```
2. Edite o arquivo `model_metadata.json`:
   ```bash
   nano model_metadata.json
   ```
3. Altere o valor da chave `training_algorithm` para o modelo desejado (PPO, DQN, SARSA, etc.).
4. Salve o arquivo e atualize os arquivos customizados com o comando:
   ```bash
   dr-update && dr-update-env && dr-upload-custom-files
   ```

---

## Ajuste de Hiperparâmetros

Para ajustar os hiperparâmetros utilizados no treinamento, siga os passos abaixo:

1. Entre na pasta `custom_files4`:
   ```bash
   cd custom_files4
   ```
2. Edite o arquivo `hyperparameters.json`:
   ```bash
   nano hyperparameters.json
   ```
3. Altere os parâmetros desejados, como taxa de aprendizado, taxa de exploração, etc.
4. Salve o arquivo e atualize os arquivos customizados com o comando:
   ```bash
   dr-update && dr-update-env && dr-upload-custom-files
   ```

---

## Seleção de Caixas de Colisão

Para adicionar caixas de colisão, edite o arquivo `run4.env`:
   ```bash
   nano run4.env
   ```
Altere o campo `DR_RACE_TYPE` para `OBJECT_AVOIDANCE` ou `HEAD_TO_BOT`. Salve o arquivo e reative o ambiente com:
   ```bash
   source bin/activate.sh run4.env
   ```

---

## Visualização de Variáveis de Ambiente

Para visualizar as variáveis de ambiente, utilize o comando `nano` ou `cat`. Por exemplo:
   ```bash
   cat run4.env
   ```
Isso exibirá as variáveis diretamente no terminal. Para editar, use:
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
   dr-train
   ```
3. Acompanhe o progresso do treinamento no terminal ou nos gráficos disponíveis no painel.

---

## Realização de Evaluation

1. Para realizar uma avaliação, selecione o modelo treinado no painel do DeepRacer.
2. Execute o comando para iniciar a avaliação:
   ```bash
   dr-evaluate
   ```
3. Escolha a pista desejada e acompanhe os resultados gerados.

---

## Realização de Deploy

1. Após treinar e avaliar o modelo, inicie o processo de deploy com o comando:
   ```bash
   dr-deploy
   ```
2. Certifique-se de que o modelo está configurado corretamente para o ambiente de produção.

---

## Continuidade de Treinamento entre Pistas

Para continuar o treinamento de uma pista A para uma pista B, siga os passos abaixo:

1. Altere a variável `WORLD_NAME` no arquivo `run4.env` para a nova pista.
2. Atualize os arquivos customizados:
   ```bash
   dr-update && dr-update-env && dr-upload-custom-files
   ```
3. Reinicie o treinamento com o comando:
   ```bash
   dr-train
   ```
Isso permitirá que o modelo aproveite os aprendizados da pista anterior enquanto treina na nova pista.

