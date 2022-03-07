# OBSERVAÇÕES DE DESENVOLVIMENTO

## Março
- Dia 07
    - Inicio dos testes do filtro em tempo real com debug na interface serial (RS485), com output da resposta do adc filtrado

- Dias 01 a 04
    - Continuação do desenvolvimento do filtro de pesagem 

## Fevereiro
- Dias 24 a 28
    - Continuação do desenvolvimento do filtro de pesagem 
- Dias 15 a 23
    - Informações Filtro de Pesagem:
    - Os conceitos abaixo foram obtidos através do empirismo e teoria sobre estudos de sinais. O relatório abaixo não expressará dados matemáticos a não ser que sejam estritamente necessários para a interpretação nos tópicos seguintes;
    - Conceitos obtidos através da observação do indicador Matrix:
        - O processo célula-indicador (Matrix) funciona da seguinte maneira: 
            - (1-A) célula é alimentada com um sinal DC teoricamente de 5V. Teoricamente pela célula ser um composto de resistores, a aplicação de um sinal DC geraria um sinal DC (0 – 10mV). Na prática a célula é alimentada com um sinal DC que varia no tempo, isso se deve ao fato de que a fonte não consegue manter a tensão constante de 5V, isso foi observado em um número alto de fontes, tanto em quantidade como em tipos, informação obtida através de análise. Através deste comportamento características tanto da célula como de parâmetros do ADC são alterados constantemente. É de total conhecimento que é tecnicamente impossível ser cravado 5V constantes sem nenhuma variação, entretanto a variação apresentada, altera significativamente o comportamento do sistema. É possível resolver este problema através de 3 possibilidades, a primeira alterando o projeto da fonte, para uma fonte mais estabilizada, a segunda através de um processo de filtragem do sinal via software (opção adotada), por fim a terceira opção se baseia na mescla entre uma atualização do projeto da fonte e a filtragem via software(recomendada).
            - (1-B) Em uma situação ideal de ambiente, não havendo interferências externas a “estabilização” total do sistema é uma situação impossível, o processo a ser adotado é a atenuação do sinal obtido e através deste sinal serão utilizados processos de analise e mascaras para o valor peso/força exercido sobre a célula, gerando um valor de peso “virtual”. 
    - Conceito obtidos através do estudo de sinais:
        - Sinais obtidos através de células de carga são como demais sinais analógicos, ou seja, somatória de senoides;
        - Através da análise do sinal lido pelo componente ADC é possível aplicar um estudo dos “sinais” lidos naquele “sinal” entregue. Através deste estudo é possível separar o sinal de ruido do sinal desejado para o processo;
        - Como o sinal desejado é um sinal DC variável em virtude da alimentação do sistema (sensor e sinal de referência do componente ADC) conforme descrito em 1-B, são necessários outros processos além do processo de filtragem do sinal chamados de “máscara”;

- Dia 14
    - Solicitação de leitura do manual Onix EtherNet/IP para análise do mesmo 
    - Estudo de instabilidade do filtro;
- Dias 07 a 11
    - Ensaios de aquisição de dados e filtragem;
- Dias 01 a 04
    - Ensaios de aquisição de dados e filtragem;

## Janeiro

- Dia 31
    - Solicitação de documentos INMETRO para desenvolvimento;
    - Solicitação de calibração de multimetro;
- Dia 24 a 28
    - Testes em filtro (calibração do filtro);
        - Dados armazenados offline;
    - Elaboração de script python para automatização de testes sobre filtro
    - Solicitação de calibração de multimetro.
- Dia 24
    - Criado nova branch corrigir_Convert para ser mesclado com a anterior assim que a correção for finalizada
    - Correção da parte negativa de leitura; 
    - Continuação da elaboração da função de calibração de divisões, seguindo a lógica para uso em sistemas de tempo real (FreeRTOS)
        - A função necessita de um cuidado em especial pois não pode ser uma função com caracteristicas "bloqueantes" para comprometer a ciclicidade do sistema;
        - A função visa corrigir problemas encontrados nos testes realizados anteriormente.

- Dia 21
    - Para padronizar a escala é necessário efetuar a calibração do processo, saber o seu pico e seu ponto de "zero" (que não será zero propriamente dito), para que desta forma torne-se possivel efetuar esse procedimento;
    - Novo brach(github) para criar a função de calibração;

- Dias 18, 19 e 20
    - Por questões de desenvolvimento, foi optado pelo trabalho do desenvolvimento deixando em segundo plano a documentação. Os dados espresso representam os dias de desenvolvimento do dia 18, 19 e 20;

    - Alguns estudos foram feitos com o propósito de dar mais precisão ao processo de leitura de dados do ADC, a precisão de variaveis do tipo float apresentam precisão muito baixa, optou-se a alteração para variaveis do tipo double que apresentam uma precisão maior;

    - Testes efetuados de medição com pesos padrões 
        - Teste 01:
        ![](/img/teste_01_10_bits.png)
        ![](/img/teste_01_11_bits.png)
        ![](/img/teste_01_12_bits.png)
        ![](/img/teste_01_13_bits.png)
        ![](/img/teste_01_14_bits.png)
        ![](/img/teste_01_15_bits.png)
        ![](/img/teste_01_16_bits.png)
        ![](/img/teste_01_17_bits.png)
        ![](/img/teste_01_18_bits.png)

        - Teste 02:
        ![](/img/teste_02_10_bits.png)
        ![](/img/teste_02_11_bits.png)
        ![](/img/teste_02_12_bits.png)
        ![](/img/teste_02_13_bits.png)
        ![](/img/teste_02_14_bits.png)
        ![](/img/teste_02_15_bits.png)
        ![](/img/teste_02_16_bits.png)
        ![](/img/teste_02_17_bits.png)
        ![](/img/teste_02_18_bits.png)

    - Teste feito de conversão de peso 

        ![](/img/teste_peso_01.png)

    - Estudo com célula de carga:
        
        ![](/img/teste_celula_carga_01.png)

        - Células de carga não apresenta um comportamento ideal conforme a reta vermelha, podendo ter seu zero deslocado a direita em "d1" posições ou "d2" posições, como consequencia a milivoltagem máxima e minima torna-se alterada, consequentemente altera o valor de máximo e mínimo.

- Dia 17:
    - Uma saída hipotética para esta situação seria trabalhar com um PGA de alto valor aceitando o ruido proveniente deste PGA e tratar esse problema com o uso de mascaras via software com lógica "E". O Número de divisões informado na tabela abaixo refere-se ao componente ADC e não ao processo (célula de carga). A máscara de bits é utilizada após a rotação a direita em 5 posições do valor recebido pelo adc. A máscara se refere a uma variável do tipo uint32_t.
    ![](/img/mascara_dados_1.png)
    ![](/img/mascara_dados_2.png)
    - Foi averiguado a possivel necessidade de se trabalhar com outras faixas de ganho de PGA como forma de se amenizar problemas oriundos de ruidos. Na hipótese de se trabalhar desta forma cada ganho PGA estaria associado a uma faixa de trabalho de abertura de número de divisões conforme mostrado abaixo 
    ![](/img/tabelaPGA.png)


- Dia 14:
    - Os dados obtidos não foram obtidos com a calibração atual do equipamento mais sim com aquela adquira na empresa durante o desenvolvimento
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

## Problemas

### Fevereiro
- Dia 23
    - O desenvolvimento efetuado do dia 15 ao dia 23 se resumiu a compreensão do sinal do sistema e a elaboração de uma nova abordagem para a filtragem do sinal lido pelo adc
- Dia 11
    - Filtro utilizado no processo de aquisição de dados encontra-se com uma instabilidade na região final de leitura será feito um estudo deste problema, enquanto isso será dado prosseguimento em outras parte do projeto 
- Dia 08
    - Aguardando calibração equipamento multimetro 
- Dia 07
    - Aguardando posicionamento do setor de qualidade a respeito da solicitação de cotação de calibração de multimetros;
    - Documentação a respeito de requisitos do INMETRO enviado é o incorreto

### Janeiro

- Dia 21: 
    - Foi solicitado a gravação de dois produtos "Detector de Pico", os firmwares não foram encontrados na pasta respectiva ao seu armazenamento. Foi encaminhado uma nova cópia juntamente com um tutorial de instalação
- Dia 17:
    -  Foi solicitação ao Walyson em conversa averiguar a possibilidade de calibração dos multimetros true RMS da empresa como forma de se obter as calibrações dos demais PGA a serem testados bem como a possibilidade de um novo circuito gerador de sinal 

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

