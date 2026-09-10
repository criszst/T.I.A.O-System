# 🤖 T.I.A.O — Tecnologia de Interação para Atendimento e Organização
> **Status do Projeto**: Protótipo Funcional (Feira Acadêmica)  
> **Tema**: Saúde Digital e Robótica Educacional  
> **Uso**: Estritamente pedagógico e de apoio.

---

## 1. Introdução
O T.I.A.O é um projeto desenvolvido por estudantes do 1º semestre na disciplina de **Engenharia de Prompt e Aplicações em IA**. O sistema combina a robustez física do **Arduino** com a capacidade analítica do **Python** para criar uma experiência de pré-atendimento hospitalar simulada, focada na organização e no acolhimento humano.

---

## 2. O Problema
Identificamos que a chegada a uma unidade de saúde é frequentemente marcada por confusão e ansiedade. A falta de uma triagem inicial rápida impede que o fluxo de pacientes seja organizado de forma eficiente, sobrecarregando profissionais e gerando desconforto nos usuários.

---

## 3. A Proposta T.I.A.O
O T.I.A.O atua como um assistente de triagem que:
* **Acolhe**: Inicia a interação de forma amigável e visual.
* **Organiza**: Coleta sinais vitais (temperatura) e sintomas básicos.
* **Informa**: Gera uma ficha anônima e categoriza o atendimento por cores acadêmicas.
* **Educa**: Demonstra os limites e benefícios da tecnologia na saúde.

---

## 4. Funcionamento Técnico
O robô funciona através de uma arquitetura híbrida:
1. **Detecção**: Um sensor ultrassônico identifica a aproximação do visitante.
2. **Medição**: O sensor de temperatura infravermelho realiza a leitura sem contato.
3. **Processamento (Arduino)**: O Arduino Mega funciona como o "cérebro físico", enviando os dados brutos via Serial para o PC.
4. **Interpretação (Python)**: O Python processa o JSON recebido, integra os sintomas e define a classificação.
5. **Feedback**: O sistema exibe o resultado na tela e acende o **LED RGB** no robô na cor correspondente (Verde, Amarelo ou Vermelho).

### 🛠️ Componentes de Hardware e Orçamento

| Item | Descrição Técnica | Qtd. | Valor Unit. (Médio) | Total Estimado |
| :--- | :--- | :---: | :---: | :---: |
| **Microcontrolador** | Arduino Mega 2560 R3 | 1 | R$ 130,11 | R$ 130,11 |
| **Leitor QR Code** | Webcam HD Logitech C270 com Microfone | 1 | R$ 135,00 | R$ 135,00 |
| **Sensor Temp.** | MLX90614 (Infravermelho sem contato) | 1 | R$ 103,91 | R$ 103,91 |
| **Sensor Oximetria** | MAX30102 (SPO2 e Batimentos) | 1 | R$ 28,78 | R$ 28,78 |
| **Módulo Áudio** | DFPlayer Mini MP3 | 1 | R$ 30,57 | R$ 30,57 |
| **Alto-falante** | Alto-falante 3W 8 Ohms | 1 | R$ 42,47 | R$ 42,47 |
| **Display** | LCD 20x4 com Módulo I2C | 1 | R$ 57,90 | R$ 57,90 |
| **Sensor Distância** | Ultrassônico HC-SR04 | 2 | R$ 19,00 | R$ 38,00 |
| **Driver Motores** | Ponte H L298N | 1 | R$ 27,99 | R$ 27,99 |
| **Motores** | Kit Chassi 2WD Duas Rodas Smart Carro Robô | 1 | R$ 78,90 | R$ 78,90 |
| **Baterias** | Célula Li-Ion 18650 (2500mAh) | 3 | R$ 23,67 | R$ 71,01 |
| **Módulo BMS** | Circuito de Proteção BMS 3S | 1 | R$ 14,00 | R$ 14,00 |
| **Status Visual** | LED RGB Difuso | 3 | R$ 1,25 | R$ 3,75 |
| **Conectividade** | Cabo USB AB (Arduino-PC) | 1 | R$ 19,00 | R$ 19,00 |
| **Diversos** | Jumpers, Chave Liga/Desliga, Protoboard | 1 | R$ 40,00 | R$ 40,00 |
| **TOTAL** | | | | **R$ 808,02** |

---

## 5. Dinâmicas do Stand (2 Minutos cada)
### 🟢 Dinâmica 1: Atendimento Real
O visitante interage com o robô. O T.I.A.O detecta sua presença, mede sua temperatura e gera uma **Ficha Anônima** em tempo real. É a prova de conceito do hardware funcionando com o software.

### 🟡 Dinâmica 2: Você organizaria esse atendimento?
O visitante recebe cards de 4 pacientes fictícios com sintomas diferentes. Ele deve decidir a ordem de prioridade. Ao final, comparamos com a lógica de triagem do T.I.A.O, discutindo a importância da organização automatizada.

### 🔴 Dinâmica 3: Verdadeiro ou Falso
Um quiz rápido focado na ética e tecnologia:
* *"O T.I.A.O substitui um médico?"* (**Falso**)
* *"O sistema deve coletar CPF?"* (**Falso**)

---

## 6. Classificação Acadêmica de Temperatura
Utilizamos uma régua simbólica para fins educacionais:
* **Hipotermia**: < 35 °C (Vermelho)
* **Normotermia**: 36 °C – 37,2 °C (Verde)
* **Febrícula/Febre**: 37,3 °C – 38,9 °C (Amarelo)
* **Hipertermia**: > 39 °C (Vermelho)

---

## 7. Estrutura do Stand
* **Cores**: Amarelo (Acolhimento), Preto (Tecnologia), Branco (Saúde).
* **Elementos**: Mesa com painel explicativo, robô físico decorado, notebook rodando Python e área de brindes.
* **Acessibilidade**: QR Code para acesso ao folder digital e ficha técnica.

---

## 8. Organização da Equipe (16 Integrantes)
| Subequipe | Função Principal |
|---|---|
| **Recepção/Fluxo** | Gestão de filas e boas-vindas. |
| **Técnica** | Supervisão do Arduino, sensores e código Python. |
| **Dinâmicas** | Condução dos desafios e quiz com visitantes. |
| **Avaliadores** | Apresentação formal e entrega dos kits especiais. |
| **Apoio/Brindes** | Logística de reposição e organização do espaço. |

---

## 9. Brindes
* **Visitantes**: Tic Tac personalizado ou seringa decorativa ("Dose de Cuidado").
* **Avaliadores**: Sacola exclusiva com folder técnico, QR Code, cartão de agradecimento e mimos personalizados.

---

## 10. Cuidados Éticos e LGPD
1. **Anonimato**: Nenhuma informação identificável (Nome, CPF, Rosto) é coletada.
2. **Segurança**: O sistema opera **Offline**, sem tráfego de dados sensíveis na rede.
