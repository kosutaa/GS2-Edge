# 💡 Gestor de Pausas Inteligentes (Pomodoro Ergonômico)
![Badge da Global Solution](https://img.shields.io/badge/Global_Solution-FIAP_2025-blue) ![Badge do Tema](https://img.shields.io/badge/Tema-Sa%C3%BAde_e_Bem_Estar-green)

Projeto de Edge Computing para a Global Solution 2025, focado no tema **Saúde e bem-estar no trabalho**. Esta solução utiliza um ESP32 e IoT para criar um dispositivo de mesa que gerencia os ciclos de trabalho e pausa (Método Pomodoro) de forma inteligente.

---

## 📋 Índice

* [🎯 O Desafio](#-o-desafio)
* [💡 A Solução](#-a-solução)
* [🛠️ Hardware e Montagem](#-hardware-e-montagem)
* [📡 Detalhes Técnicos: MQTT](#-detalhes-técnicos-mqtt)
* [🚀 Como Usar (Wokwi)](#-como-usar-wokwi)
* [🎥 Demonstração](#-demonstração)
* [👥 Integrantes](#-integrantes)

---

## 🎯 O Desafio

No futuro do trabalho, especialmente em modelos híbridos ou remotos, os profissionais passam longos períodos em trabalho focado. A ausência de pausas regulares leva à fadiga mental, estresse, LER (Lesão por Esforço Repetitivo) e a uma queda geral na produtividade e bem-estar.

## 💡 A Solução

Propomos um dispositivo físico de baixo custo, baseado em ESP32, que automatiza o controle dos ciclos de trabalho e descanso.

O usuário inicia um ciclo de "foco" (25 minutos) ao pressionar um botão. O dispositivo sinaliza visualmente (LED verde) que o tempo de foco está ativo. Ao final do ciclo, um alarme sonoro (buzzer) é disparado e o dispositivo entra automaticamente em modo "pausa" (5 minutos), sinalizado por um LED vermelho.

Simultaneamente, o status do dispositivo ("foco", "pausa", "ocioso") é publicado em um tópico MQTT, permitindo que esses dados sejam consumidos por dashboards de produtividade ou plataformas de bem-estar corporativo.

---

## 🛠️ Hardware e Montagem

Para replicar o projeto, são necessários os seguintes componentes:

* 1x ESP32
* 1x LED Verde
* 1x LED Vermelho
* 1x Buzzer
* 1x Botão (Pushbutton)
* 2x Resistores de 220 Ohm (para os LEDs)
* Protoboard e Jumpers

### Diagrama do Circuito

A montagem do circuito pode ser visualizada na simulação do Wokwi.

https://imgur.com/w1i4vJc
``

### Tabela de Pinagem

| Componente | Pino no ESP32 |
| :--- | :--- |
| Botão | `GPIO 15` |
| LED Verde (Foco) | `GPIO 12` |
| LED Vermelho (Pausa) | `GPIO 14` |
| Buzzer (Alerta) | `GPIO 27` |
| (GND) | `GND` |

---

## 📡 Detalhes Técnicos: MQTT

A comunicação com o servidor IoT é feita via protocolo MQTT.

* **Broker MQTT:** `44.223.0.185` (Broker disponibilizado pelo professor)
* **Tópico de Publicação:** `fiap/gs/pomodoro/user1`

### Explicação dos Payloads

O ESP32 publica mensagens em formato JSON neste tópico para reportar a mudança de estado:

1.  **Início do Foco:**
    ```json
    {"status": "foco"}
    ```

2.  **Início da Pausa:**
    ```json
    {"status": "pausa"}
    ```

3.  **Fim da Pausa (Ocioso):**
    ```json
    {"status": "ocioso"}
    ```

---

## 🚀 Como Usar (Wokwi)

Instruções para replicar e testar a simulação:

1.  **Acesse o Wokwi:** Abra o link da simulação [disponível na seção Demonstração](#-demonstração).
2.  **Código-Fonte:** O arquivo `sketch.ino` (disponível neste repositório) já está carregado no simulador.
3.  **Configuração de Rede:** O Wokwi simula a conexão Wi-Fi com a rede "FIAP-IOT" (SSID) com a senha (F!@p25.IOT), que já está configurada no código.
4.  **Inicie a Simulação:** Clique no botão verde "Start Simulation".
5.  **Monitore:** Aguarde o "Serial Monitor" exibir a mensagem "WiFi conectado!" e "MQTT conectado!".
6.  **Teste:** Pressione o botão (pushbutton) no simulador. O LED verde acenderá, e o status "foco" será publicado (visível no monitor). Após o tempo de demonstração (10s), ele mudará para "pausa" (LED vermelho) e, por fim, "ocioso".

---

## 🎥 Demonstração

* **Link da Simulação Wokwi:** `https://wokwi.com/projects/447878016430607361`
* **Link do Vídeo Explicativo:** `https://youtu.be/zl3ACW83EBY`

---

## 👥 Integrantes

* Guilherme Moura Gama - RM: 562162
* Guilherme Ruiz Costa - RM: 563236
