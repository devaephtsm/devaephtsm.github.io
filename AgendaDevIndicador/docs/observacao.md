# OBSERVAÇÕES DE DESENVOLVIMENTO

## Janeiro
### Semana 01
#### Atividades 

- Dia 14:
    - Comparação entre dados obtidos da leitura;
    ![](/img/comparacao_medicoes.png)
    ![](/img/comparacao_medicoes2.png)
    ![](/img/adc.png)

    - Criação da biblioteca de conversão dos dados lidos para dados do tipo float 
        - Para valores negativos é necessário efetuar correção pois esta apresentando erros;
    - Alteração de retorno de bibliotecas
    - Alteração do nome de bibliotecas 

- Dia 13:
    - Criado biblioteca vERROR_CHECK() para tratativa de erros (Início)
    - Criação da função de inicialização do adc com comparação e tratativa de erro (ainda não implementado)
    ![](/img/adc_start_01.png)
    ![](/img/adc_start_02.png)
    ![](/img/adc_start_03.png)
    ![](/img/adc_start_04.png)
    ![](/img/adc_start_05.png)
    ![](/img/adc_start_06.png)
    ![](/img/adc_start_07.png)

    - Testes com a configuração do indicador antigo (Configuração de registradores);
    - Função de leitura do adc (testado)
    ![](/img/func_leitura_data_adc.png)
    - Verificações a respeito dos processos ocorridos no atual indicador de pesagem:
        - Não é feito nenhuma escrita nos registradores de calibração;
        - Ao iniciar o atual indicador efetua um comando de reset;
        - São configurados alguns registradores 0x00, 0x01 e 0x02
            - Ganho em 128
            - Escrita de configuração defaut no registrador 1
            - Escrita no registrador MUX com o valor1 
            - Escrita no Registrador 0x02 do valor 0x04m ativando o registrador
    - "u8WriteCS1180()" -> testado 
        
    - "u8_ResetCS1180()" -> testado

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

- Dia 14:

- Dia 13:
    - As funções "u8WriteCS1180()" e "u8_ResetCS1180()" não apresenta gráfico devido ao dado ter sido perdido

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

