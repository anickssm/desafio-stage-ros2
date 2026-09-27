# Desafio Stage ROS2

## Objetivo

Desenvolver um controlador autônomo em ROS 2 capaz de conduzir um robô móvel no simulador Stage até um ponto objetivo, utilizando informações de posição e dados do sensor LiDAR para evitar obstáculos.

O objetivo utilizado no cenário é aproximadamente:

- X = 5.0
- Y = 4.0

## Funcionamento

O controlador utiliza os seguintes tópicos ROS 2:

- `/base_scan` - dados do sensor LiDAR.
- `/ground_truth` - posição e orientação do robô no ambiente.
- `/cmd_vel` - comandos de velocidade linear e angular enviados ao robô.

A orientação do robô é obtida através da conversão da orientação em quaternion para o ângulo yaw.

O sensor LiDAR é dividido em três regiões:

- frente;
- esquerda;
- direita.

Quando não existem obstáculos próximos, o robô calcula a direção do objetivo e se desloca até ele.

Quando um obstáculo é detectado, o controlador seleciona uma direção de desvio utilizando as distâncias medidas pelo LiDAR.

Ao atingir a região definida como objetivo, o robô para automaticamente.

Caso o robô seja posteriormente deslocado para longe do objetivo, a missão é reativada e o robô retorna autonomamente ao destino.

## Compilação

Na raiz do workspace:

```bash
cd ~/stage_ros2_ws
colcon build --packages-select stage_controller
source install/setup.bash
