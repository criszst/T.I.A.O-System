# Tutorial de Software: Robô TIAO (Tecnologia de Interação para Atendimento e Organização)
Este guia foi desenvolvido para estudantes do 1º semestre de Ciência da Computação para a construção do software do robô de triagem hospitalar acadêmico TIAO.
**Aviso Importante:** Uso estritamente pedagógico e de apoio.
## 1. O Papel do Python no Projeto
No sistema do TIAO, o Arduino atua coletando dados físicos (presença e temperatura), enquanto o Python é o responsável pela inteligência do sistema:
 * **Receber** e interpretar dados enviados pelo Arduino.
 * **Organizar** o fluxo de triagem e exibir mensagens ao usuário.
 * **Classificar** o atendimento preliminar e gerar uma ficha simples e anônima.
 * **Privacidade:** O sistema funciona localmente (sem internet) e não coleta dados sensíveis como CPF ou nome completo.
## 2. Preparação do Ambiente
Para começar, você precisará das seguintes ferramentas:
 1. **Python:** Baixe a versão mais recente e, na instalação, marque a opção **"Add Python to PATH"**.
 2. **VS Code:** O editor de código onde escreveremos o software. Instale também a extensão "Python" dentro dele.
 3. **Biblioteca PySerial:** Permite que o Python "converse" com o Arduino via USB. No terminal, instale com:
   ```bash
   pip install pyserial
   
   ```
   *(Resultado esperado: Successfully installed pyserial).*
## 3. Conceitos Básicos de Python
Para este projeto, focaremos apenas no essencial:
 * **print:** Mostra mensagens na tela.
 * **Variáveis:** Guardam dados, como temperatura = 36.8.
 * **Tipos de Dados:** float (decimais), int (inteiros) e string (texto).
 * **if, elif, else:** Tomam decisões baseadas na temperatura para definir a classificação.
 * **try/except:** Trata erros para que o programa não pare de funcionar se receber dados incompletos.
## 4. Lógica de Triagem e Simulação
Antes de conectar o hardware, simulamos a lógica acadêmica:
### Regra Acadêmica de Classificação
 * **VERDE:** Temperatura abaixo de 37.5 °C.
 * **AMARELO:** Temperatura entre 37.5 °C e 38.5 °C.
 * **VERMELHO:** Temperatura acima de 38.5 °C.
**Nota:** Esta classificação é simplificada para fins de estudo e não deve ser usada para decisões médicas reais.
## 5. Integração com Arduino
### O Formato dos Dados
O Arduino envia as informações via texto (string) no seguinte formato:
TEMP:36.8;PRESENCA:1
 * **TEMP:** Temperatura lida pelo sensor.
 * **PRESENCA:** Indica se há alguém próximo (1 = Sim, 0 = Não).
 * **;:** Separador de informações.
### Comunicação Serial
Utilizamos o pyserial para abrir a porta USB (ex: COM3) com a mesma velocidade (**baud rate**) configurada no Arduino, geralmente 9600.
```python
import serial
# Abre a porta COM do Arduino
arduino = serial.Serial("COM3", 9600) 
# Lê e limpa a linha recebida
linha = arduino.readline().decode().strip() 
print(linha)

```
## 6. Organização em Funções
Para manter o código limpo, dividimos o programa em pequenas tarefas:
 1. **Interpretar Dados:** Transforma o texto recebido em números reais (float e int).
 2. **Classificar Risco:** Aplica a regra de cores baseada na temperatura.
 3. **Mostrar Resultado:** Exibe a **Ficha Anônima de Atendimento**.
## 7. Checklist de Teste Final
Antes da apresentação, verifique:
 * [ ] O monitor serial do Arduino está fechado?
 * [ ] A porta COM no Python é a mesma que o Arduino está usando?
 * [ ] O sistema gera o resultado "VERDE" para 36.8 °C?
 * [ ] O erro de "Dado Incompleto" está sendo tratado?
 * [ ] A ficha é totalmente anônima?
## 8. Melhorias Futuras Opcionais
Após o básico funcionar, o projeto pode evoluir com:
 * **Interface Gráfica:** Uso da biblioteca Tkinter para uma tela visual.
 * **QR Code:** Identificação de atendimentos via webcam.
 * **Salvamento Local:** Registro dos atendimentos em arquivos .txt ou .csv.
 * **Integração com Áudio:** Mensagens de voz para tornar o robô mais acessível.
**Objetivo Final:** O foco é entender que o Arduino coleta, o Python interpreta e a lógica classifica, sempre de forma anônima e local.
