# Agenda de desenvolvimento Indicador de Pesagem

## SEMANA 01
* Testes com indicadores de pesagem.
### Atividades:
* Leitura de manuais;
* Calibração e comparação de resultados.

## SEMANA 02
* Testes da placa de desenvolvimento microcontrolador/circuito ADC
### Atividades:
* Leitura direta do circuito ADC pelo microcontrolador com debug através da saída serial.

## SEMANA 03 a 06
* Implementação do filtro Kalman ao processo de pesagem.
### Atividades:
* Implementação da lógica de filtro em linguagem C e Python;
* Integração do filtro ao microcontrolador stm32 utilizado na placa de desenvolvimento;
* Implementação de lógica simples de debug serial.

## SEMANA 07 a 11
* Implementação do filtro do processo ao processo de pesagem 2.
### Atividades:
* Criação de variáveis de controle do filtro Kalman;
* Integração da lógica filtro + freeRTOS.

## SEMANA 12 a 15
* Criação/Integração IHM do sistema + FreeRTOS
### Atividades:
* Criação da interface IHM do sistema com integração do FreeRTOS.
* Testes de integração.

## SEMANA 16 a 20
* Logica Modbus + integração FreeRTOS
### Atividades:
* Desenvolvimento da lógica de comunicação serial;
	* BaudRates: 9600, 19200, 38400, 57600 e 115200 (verificar disponibilidade);
	* StopBit: 8N1 e 8N2;
* Modbus;
	* Integração FreeRTOS.

## SEMANA 21 a 28
* Testes de lógica e integração FreeRTOS
### Atividades:
* Testes e debug das lógicas de filtro aplicados ao processo;
* Testes e debug das lógicas de IHM;
* Testes e debug das lógicas de comunicação serial;
* Testes e debug das lógicas Modbus;
* Testes e debug das lógicas FreeRTOS;

## OBSERVAÇÃO DE DESENVOLVIMENTO
* Os prazos estipulados acima são deduzidos a partir de dedicação exclusiva ao mesmo;
* A última semana de desenvolvimento pode sofrer retração em virtude das semanas anteriores de desenvolvimento necessitarem de um maior prazo.

