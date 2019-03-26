# Camada De Enlace

## Sum�rio
- [Camada De Enlace](#camada-de-enlace)
  - [Sum�rio](#sum�rio)
  - [Introdu��o](#introdu��o)
  - [Servi�os](#servi�os)


## Introdu��o

A camada de enlace tem como responsabilidade de transferir um datagrama de um n� para o n� adjacente sobre um enlace. Os protocolos e padr�es desta camada, diferente das camadas superiores que s�o baseados em RFCs, estes geralmente s�o definidos por empresas de comunica��es ou organiza��es de engenharias (Como ANSI, IEEE e ITU). Os servi�os e especifica��es desta camada s�o geridos por m�ltiplos padr�es de acordo com a tecnologia e o meio f�sico utilizado e integrado por tais protocolos, sendo alguns deles utilizados para ligar os servi�os da camada de enlace com a camada f�sica.

## Servi�os

* **Enquadramento de dados**
  * **Encapsula datagramas em quadros acrescentando cabe�alhos e trailer**;
  * **Delimita��o dos quadros:**
    *	Contador de caracteres;
    *	Caracteres de inicializa��o e finaliza��o, com car�cter de preenchimento;
    *	Flags de inicializa��o e finaliza��o, com car�cter de enchimento.
*	**Transfer�ncia dados da camada de rede da m�quina de origem para a camada de rede do destino**
  *	**N�o orientados a conex�es e sem reconhecimento**
    *	Quadros independentes
    *	Indicado para taxa de erros muito baixa ou tr�fego em tempo real
  *	**N�o orientados a conex�es e com reconhecimento**
    *	Quadros confirmados individualmente
    *	�til em canais n�o confi�veis (ex.: sistemas sem fio)
  *	**Orientados a conex�es e com reconhecimento**
    *	Estabelecimento de conex�o antes da transfer�ncia de dados
	  * Quadros confirmados individualmente
	  * Garante que cada quadro ser� recebido uma �nica vez e na ordem correta
*	**Detec��o e Corre��o de erros**
  * **Verifica��o de Paridade**
    *	Paridade com bit �nico: Detecta erro de um �nico bit
    *	Paridade bidimensional: Detecta e corrige erro de um �nico bit
  * **C�digo de hamming:**
    *	Dada uma palavra c�digo: n = m + r
    *	Os r bits de verifica��o ocupam as posi��es que s�o pot�ncias de 2
    *	Os outros (3, 5, 6, 7, 9, etc.) s�o preenchidos com os m bits de dados.
    *	Os bits de verifica��o resultam de um XOR das posi��es de influ�ncia
  * **C�digo Polinomial ou C�digo de Redund�ncia C�clica (CRC)**
    *	Transmissor e receptor devem concordar em rela��o a um polin�mio gerador, G(x), antecipadamente. E tanto o bit de mais alta ordem quanto o de mais baixa ordem do polin�mio gerador devem ser iguais a 1.
    *	G(x) � usado junto a informa��o no transmissor gerando uma nova sequ�ncia de dados a ser enviado, M(x)
    *	Se M(x) ao chegar no receptor, n�o for divis�vel pelo polin�mio gerador, significa que houve erro de transmiss�o.
    *	Algoritmo
      *	Seja G(x) o gerador polinomial de grau r. 
      *	Acrescente r bits 0 ao quadro que ser� transmitido
      *	Divida o novo quadro pelo gerador G(x)
      *	Subtraia do quadro original o resto da divis�o
*	**Controle de fluxo**
  * Limita��o da transmiss�o entre transmissor e receptor
  * O receptor avisa quando o transmissor pode enviar um quadro

## Procolos para controle de fluxo:

### Simplex sem restri��es:
* Transmiss�o de dados em um �nico sentido;
* Camada de redes sempre pronta;
* Buffer infinito no qual poder�o ser armazenados todos os quadros recebidos enquanto eles aguardam para serem processados;
* N�o h� perda de quadros.

### Simplex Stop-and-wait:
* Os buffers n�o s�o infinitos;
* O tempo de processamento n�o � ignorado;
* O transmissor n�o envia outra mensagem at� que a anterior tenha sido aceita como correta pelo receptor;
* Embora o tr�fego de dados seja simplex, h� fluxo de quadros em ambos os sentidos.
* **Problema:** impedir que o transmissor inunde o receptor com dados, mais rapidamente do que este � capaz de process�-los.
* **Solu��o:** fazer o receptor enviar uma resposta para o transmissor, autorizando o envio do pr�ximo quadro.

### Simplex para um Canal com Ru�do:
* O transmissor transmite um quadro que � numerado sequencialmente;
* O receptor envia um quadro de reconhecimento se o quadro for recebido corretamente, caso contr�rio, h� um descarte e � aguardada uma retransmiss�o;
* Quadros n�o reconhecidos s�o retransmitidos (timer).

### Protocolos de Janela Deslizante:
* **Piggybacking:** t�cnica de retardar temporariamente as confirma��es de recebimento de um quadro e envi�-las junto com o pr�ximo quadro de dados. 
  * **Como funciona?**
    *	Quando um quadro de dados chega a seu destino, em vez de enviar imediatamente um quadro de controle separado, o receptor se cont�m e espera at� a camada de rede enviar o pr�ximo quadro. A confirma��o � acrescentada ao quadro de dados que est� sendo enviado (por meio do campo ack do cabe�alho de quadro). Na verdade, a confirma��o pega carona no pr�ximo quadro de dados que estiver sendo enviado. 
  * **Vantagens:** 
    *	Melhor utiliza��o da largura de banda dispon�vel para o canal
    *	Menor n�mero de quadros enviados, que implica em menor quantidade de buffers no receptor, dependendo da forma como o software do receptor est� organizado
  * **Desvantagem:**
    *	A camada de enlace n�o sabe quanto tempo deve esperar por um quadro para enviar a confirma��o. Se esperar por um tempo maior que o timeout do transmissor, o quadro ser� transmitido novamente, o que invalidar� todo o processo de confirma��o.

### Janela Deslizante:
� um protocolo bidirecional, no qual cada quadro enviado cont�m um n�mero de sequ�ncia, variando desde 0 at� algum valor m�ximo. Em geral, o valor m�ximo e 2n �1, de forma que o n�mero de sequ�ncia caiba exatamente em um campo de n bits. 

> ### Janela deslizante de 1 bit:
> Esse tipo de protocolo utiliza o stop-and-wait, pois o transmissor envia um quadro e aguarda sua confirma��o antes de enviar o quadro seguinte. 
> O campo de confirma��o no quadro cont�m o n�mero do �ltimo quadro recebido sem erro. Se esse n�mero estiver de acordo com o n�mero de sequ�ncia do quadro que o transmissor est� tentando enviar, o transmissor saber� que j� cuidou do quadro armazenado em buffer e poder� buscar o pacote seguinte em sua camada de rede. Se o n�mero de sequ�ncia for discordante, o transmissor deve continuar tentando enviar o mesmo quadro. Sempre que um quadro � recebido, um outro quadro tamb�m � enviado de volta.

### Pipeline:
T�cnica baseada em permitir que o transmissor envie at� w quadros antes do bloqueio, e n�o apenas 1. Com uma escolha apropriada de w, o transmissor ser� capaz de transmitir quadros continuamente durante um tempo igual ao tempo de tr�nsito da viagem de ida e volta, sem ocupar a janela toda. 

> �O que fazer se um quadro no meio da janela for danificado ou perdido? �

> **Estrat�gias b�sicas para lidar com erros na presen�a do pipelining**:
> **Go Back N**
>   * O destino descarta qualquer pacote fora de ordem; portanto, n�o necessita de um buffer.