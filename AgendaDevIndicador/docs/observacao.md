# OBSERVAÇÕES DE DESENVOLVIMENTO

## Janeiro
### Semana 01
#### Atividades 

- Dia 12: 
    - Teste da função "u8ReadCS1180()". Efetuado teste sobre o ad seguido da requisição de todos os registradores do ADC
    ![](/img/u8ReadCS1180.png)
    - Criação da função "u8ReadCS1180()" (Não Testada)
    - Criação da função "u8WriteCS1180()" (Não Testado)
    - Criação da função "u8_ResetCS1180()" (Não Testado)
    - Teste da função "u8_TestCS1180()"
    ![](/img/func_u8_TestADC.png)


    
- Dia 11:
    - Inicio construção biblioteca cs1180
    - Leitura de Byte em SPI em 16.16us e frequencia de clock em 545.45KHz
    ![](/img/time_byte_spi_write5.png)
    <br> 
    ![](/img/time_byte_spi_write6.png)
    <br> 
    - Cristal externo de 16MHz(desenvolvimento) inserido no lugar do anterior, alteração do tem de tráfego de 8bits em spi em +0.2us 
    ![](/img/time_byte_spi_write4.png)
    - Criação da leitura SPI (inicio) 
    - Criação de "semaforo" para possivel multipla utilização do canal SPI "software", com retorno 0x00 para sucesso e 0x01 para falha na solicitação de escrita, indicando que o canal já estar em utilização
    - A comunicação SPI foi atualizada tendo um ganho na frequencia. Motivo, cristal utilizado anteriormente (24.594MHz).
    ![](/img/time_byte_spi_write3.png)
    <br>        
    ![](/img/time_byte_spi_write2.png)
    <br>
    - Foi diagnosticado um erro com relação ao cristal utilizado na placa de 24.594MHz para o de 25MHz. Para desenvolvimento será utilizado cristal de 16MHz
    ![](/img/alteracao_cristal.png)

- Dia 10:
    - Inicio de testes adc;
    - A comunicação serial será feita via software, o teste inicial será feita via polling e no futuro a biblioteca deve ser convertida para freeRTOS não bloqueante; 
    - Solicitação de insumos para teste barra de pinos fêmea;
    - Criação da biblioteca de leitura SPI (Software - Não Bloqueante) 
        - Escrita (OK)
            - Tempo de escrita de byte: 88.875us
            ![](/img/time_byte_spi_write.png)
            <br>            
            ![](/img/info_bit_spi.png)
            <br>
        - Leitura (Pendente).

- Dia 07:
    - Teste de gravação realizado, com adaptação dos pinos CN7;
    - Inicio do projeto New Matrix (STM32 Cube IDE); 
    - Adaptação dos pinos CN5 (UART) debug de desenvolvimento da SEMANA2;
    - Estudos Implementação FreeRTOS.
- Dia 06:
    - Organização da bancada de desenvolvimento e testes iniciais da placa de desenvolvimento;
- Dia 05: 
    - Organização de documentação e material;
- Dia 04: 
    - Leitura de manuais de indicadores de terceiros;

#### Observações

- Dia 12: 
    - Foi necessário efetuar alterações na placa com o objetivode se obter um canal de debug para o circuito adc-spi de comunicação, a alteração teve duração de 2horas. A duração se deu em virtude de problemas encontrados durante a alteração;
    - Foi observado através do teste realizado no dia de trabalho que é possivel através do firmware em desenvolvimento auxiliar nos processos de manutenção de equipamentos;
        - Atravez da certeza que os sinais CS, SDI, SDO, CLK e READ estão chegando no componente AD através de equipamentos como osciloscópio ou analisador lógico, o microcontrolador pode enviar o comando de teste da função "u8_TestADC()". A função pode verificar se o componente ADC esta funcionando corretamente. (Deve-se ter a certeza que as trilas, indutores estão em perfeito funcionamento)
- Dia 11:
    - Solicitações de componentes apresentam um atraso na entrega o que pode impactar no tempo de desenvolvimento;
- Dia 06: 
    - Em conversas com Walyson, as atividades da semana 1 que compete a ele foram passadas para a proxima semana de trabalho. Para evitar a espera, as atividades da semana seguinte serão adiantadas evitando assim algum possivel atraso nos trabalhos.

- Dia 05: 
    - ausencia por 1h30minutos por motivo de saúde (3ª dose vacina covid);
    - saída do trabalho com quatro horas de antecedencia por motivos pessoais e justificados a chefia e ao RH, com solicitação de reposição das horas;

