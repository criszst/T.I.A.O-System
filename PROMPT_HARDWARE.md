# 🤖 T.I.A.O. - Guia Técnico de Hardware
**Tecnologia de Interação para Atendimento e Organização**
Este documento serve como um guia de montagem e mentoria para a construção de um robô/totem acadêmico de triagem hospitalar de baixo custo.

## 1. Arquitetura Física Comentada exemplo
O sistema é estruturado em duas camadas principais que operam localmente:
 * **Camada de Hardware:** Gerenciada pelo **Arduino Mega 2560**, responsável pela leitura de sensores, acionamento de LEDs, LCD, áudio e controle de motores.
 * **Camada de Software:** Um programa em **Python** rodando em um PC, que interpreta os dados, aplica a lógica de triagem e gera fichas de atendimento.
 * **Comunicação:** Realizada via cabo USB (Serial), permitindo troca de dados bidirecional sem necessidade de internet ou nuvem.
 * **Conexões:** Baseadas na filosofia "Zero Solda", utilizando protoboards e jumpers para facilitar a modularidade e aprendizado.

## 2. Tabela Master de Pinagem
| Componente | Pino Arduino Mega | Tipo de Sinal | Função no T.I.A.O. |
|---|---|---|---|
| **MLX90614** | 20 (SDA) / 21 (SCL) | I2C | Temperatura corporal infravermelha |
| **MAX30102** | 20 (SDA) / 21 (SCL) | I2C | Oximetria e batimentos cardíacos |
| **LCD 20x4 I2C** | 20 (SDA) / 21 (SCL) | I2C | Interface visual do paciente |
| **HC-SR04 Frontal** | 22 (TRIG) / 23 (ECHO) | Digital | Detecção de presença do paciente |
| **HC-SR04 Inferior** | 24 (TRIG) / 25 (ECHO) | Digital | Proteção anticolisão do chassi |
| **DFPlayer Mini** | 18 (TX1) / 19 (RX1) | Serial UART | Reprodução de áudio e orientações |
| **LED RGB 1** | 44 (R), 45 (G), 46 (B) | PWM | Sinalização visual principal |
| **Ponte H L298N** | 30 a 33 (In) / 11, 12 (EN) | PWM/Digital | Controle de direção e velocidade |

## 3. Esquema de Fluxo Energético Detalhado
O gerenciamento de energia é projetado para isolar ruídos e proteger componentes sensíveis:
 1. **Fonte Primária:** Pack de 3 células **Li-Ion 18650** em série (11.1V nominais).
 2. **Proteção:** Módulo **BMS 3S** que controla sobrecarga, descarga profunda e curto-circuito.
 3. **Ramo de Potência (Motores):** A tensão de 11.1V vai diretamente para a **Ponte H L298N**.
 4. **Ramo de Lógica (Arduino/Sensores):** A tensão passa por um **regulador buck (step-down)** para 5V estabilizados.
 5. **Alimentação Sensível:** O Arduino Mega fornece **3.3V** específicos para os sensores médicos (MLX90614 e MAX30102).
> **Nota de Segurança:** Os motores geram ruído elétrico (EMI). Devem ser usados capacitores de 100µF a 470µF para suavizar picos de corrente e diodos de roda-livre para proteção.
 
## 4. Protocolo de Comunicação JSON
A comunicação é feita por frames terminados em \n (newline) para facilitar a leitura no Python.
### Frame do Arduino para o Python
```json
{
 "distancia_frontal_cm": 45.3,
 "temp_celsius": 36.8,
 "spo2": 98,
 "bpm": 82,
 "presenca": 1,
 "status_bateria": "OK"
}

```
 * **campos:** Coleta todos os sinais vitais e status do hardware.
### Frame de Resposta do Python
```json
{
 "classificacao": "AMARELO",
 "mensagem_lcd_linha1": "Atencao!",
 "led_r": 255,
 "led_g": 165,
 "audio_id": 5
}

```
 * **campos:** Controla a interface do robô com base na lógica de triagem.

## 5. Guia de Montagem em Protoboard
A organização é vital para evitar erros de iniciantes:
 * **Zonificação:** Divida a protoboard em áreas (I2C Central, Sensores de Presença, Áudio, LEDs e Alimentação).
 * **Cores de Jumpers:** Vermelho (5V/3.3V), Preto (GND), Amarelo (Digital), Azul (SDA), Verde (SCL).
 * **GND Unificado:** Todas as terras (bateria, Arduino, motores) devem se encontrar em um único ponto em estrela para minimizar loops de terra.
 * **Isolamento:** Mantenha os fios de potência (motores) longe dos fios de sinal dos sensores médicos.

## 6. Guia de Debug e Testes de Validação
Siga esta ordem antes da integração total:
 1. **Scanner I2C:** Confirme se os endereços 0x5A (MLX), 0x57 (MAX) e 0x27/0x3F (LCD) são detectados.
 2. **Teste de Continuidade:** Use multímetro para garantir que todos os GNDs estão interconectados.
 3. **Teste de Isolamento:** Verifique se os 11.1V da bateria **não** estão encostando na linha de 5V do Arduino.
 4. **Validação Serial:** Envie um JSON fixo para o PC e verifique se o Python recebe e parseia os dados corretamente.

## 7. Disposição Física do Totem
A ergonomia foi planejada para atender adultos e crianças:
 * **160–170 cm:** Sensor MLX90614 (alinhado à testa).
 * **140–150 cm:** Display LCD 20x4 (altura de leitura confortável).
 * **120–130 cm:** Sensor MAX30102 (altura da mão estendida, com apoio para o pulso).
 * **40–60 cm:** Núcleo de processamento (Arduino e Baterias) para manter o centro de gravidade baixo e evitar tombamentos.

## 8. Erros Comuns e Soluções
 1. **LCD sem caracteres:** Ajuste o potenciômetro de contraste no módulo I2C.
 2. **Temperatura errática:** O MLX90614 requer distância de 5-10 cm da pele.
 3. **DFPlayer não toca:** Verifique se o SD está em FAT32 e os arquivos na pasta /mp3/.
 4. **Arduino reiniciando:** Geralmente causado por picos dos motores; use capacitores de 470µF.
 5. **MAX30102 não estabiliza:** Evite luz solar direta e peça para o paciente não mover o dedo.
 6. **Inversão SDA/SCL:** O I2C não funcionará se os fios de dados e clock estiverem trocados.
 7. **Resistor de 1kΩ no DFPlayer:** A falta dele pode queimar o módulo ao receber 5V do Arduino.
 8. **LEDs Queimados:** Nunca conecte LEDs diretamente aos pinos sem resistores de 220Ω ou 330Ω.
