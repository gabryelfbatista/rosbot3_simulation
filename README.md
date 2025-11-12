# rosbot3_simulation

Repositório principal desenvolvido durante a disciplina de robótica para consolidar o ambiente de simulação em ROS2.

## Estrutura
- `src/rosbot3_description`: descrição URDF do robô, com sensores e suportes modelados a partir das dimensões reais.
- `src/ros_commons`: macros e utilidades reutilizáveis (sensores, controlador skid-steer, layouts do RQT).
- `src/rosbot3_gazebo`: integração com o Gazebo incluindo launch de simulação, mundos e ajustes específicos.
- `scripts/`: utilitários para configurar o ambiente (`setup.bash`), compilar (`make.sh`) e limpar (`make_clean.sh`), além do `download_gazebo_models.sh`.
- `make/`: diretório gerenciado pelos scripts para builds e artefatos intermediários.

Todos os pacotes são mantidos também como submódulos Git, permitindo versionar cada componente separadamente.

## Destaques da disciplina
- Macro `skid_steer_controller` adicionada em `ros_commons` para controlar as quatro rodas e publicar odometria diretamente no Gazebo.
- Painel `rqt_steering` já conectado ao launch de simulação, acelerando testes manuais.

## Como utilizar
1. Instale `git` e o plugin `git-lfs` antes de clonar o repositório:
   ```bash
   sudo apt install git git-lfs
   ```
2. Clone o projeto já trazendo todos os submódulos:
   ```bash
   git clone --recurse-submodules git@github.com:gabryelfbatista/rosbot3_simulation.git
   ```
3. Ou se quiser atualizar o repositório já clonado:
   ```bash
   git pull --rebase --recurse-submodules
   ```
4. Caso encontre problemas para baixar arquivos armazenados com Git LFS, execute:
   ```bash
   git submodule foreach git lfs pull
   ```
5. Se o repositório já tiver sido clonado sem `--recurse-submodules`, inicialize os submódulos manualmente:
   ```bash
   git submodule update --init --recursive
   ```
6. Antes de rodar a simulação pela primeira vez, faça o download dos modelos do Gazebo:
   ```bash
   ./scripts/download_gazebo_models.sh
   ```
7. Para compilar a workspace, estando na raiz do repositório:
   ```bash
   ./scripts/make.sh
   ```
8. Durante o desenvolvimento pode ser útil usar `--symlink-install` para criar links simbólicos no diretório `install/` sem copiar os arquivos:
   ```bash
   ./scripts/make.sh --symlink-install
   ```
   Isso permite atualizar lançadores, configurações etc. sem reconstruir toda a workspace.
9. Se necessário, limpe a build atual:
    ```bash
    ./scripts/make_clean.sh
    ```
10. Após a compilação, carregue o ambiente para que os pacotes fiquem visíveis às ferramentas ROS:
    ```bash
    source ./scripts/setup.bash
    ```
11. Inicie o ambiente de simulação:
   ```bash
   ros2 launch rosbot3_gazebo start.launch
   ```

