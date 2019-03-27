# Camada de Transporte

## Sum�rio
- [Camada de Transporte](#camada-de-transporte)

Os servi�os oferecidos pelo protocolo IP n�o oferecem confiabilidade. Problemas relacionados � congestionamento, perda e ordena��o de pacotes n�o s�o tratados. Esse � um grande problema pois a camada de aplica��o necessita prover um servi�o confi�vel na entrega de dados para os usu�rios. Para tal, a camada de transporte tem diversos protocolos e fun��es para melhorar e corrigir erros das camadas abaixo da mesma - como a de redes.

## Protocolos e servi�os de transporte

* Fornecem comunica��o l�gica entre processos de aplica��o em diferentes hospedeiros
*	Os protocolos de transporte s�o executados nos sistemas finais 
  *	**Lado emissor**: quebra as mensagens da aplica��o em segmentos e envia para a camada de rede
  *	**Lado receptor**: remonta os 3 segmentos em mensagens e passa para a camada de aplica��o 
*	H� mais de um protocolo de transporte dispon�vel para as aplica��es e nem todas implementam o mesmo conjunto de servi�os:
  *	Internet: TCP e UDP
  *	TCP
    *	Confi�vel: garante ordem de entrega
    *	Controle de Congestionamento
    *	Controle de Fluxo
    *	Orientado � conex�o
*	UDP
  *	N�o confi�vel: n�o garante ordem na entrega
  *	Extens�o do melhor esfor�o do IP
  *	Apenas multiplexa��o

## Identifica��o da aplica��o no host

A camada de transporte oferece � camada de aplica��o a fun��o de endere�amento, onde os servi�os s�o identificados pela sua porta (HTTP-80, FTP-20/21�) e uma conex�o entre sua esta��o e outro host � feita atrav�s de um socket (IP+PORTA).

1.	**Como cada m�quina � identificada unicamente na Internet?** <br/> > *N�mero IP*.
2.	**Como a entidade de rede (IP) identifica qual o protocolo de transporte est� sendo utilizado?** <br/> > *Tipo de protocolo est� indicado no cabe�alho IP*.
3.	**Dentro do host, como a entidade de transporte identifica qual aplica��o est� sendo utilizada?** <br/> > *Cada aplica��o tem uma �Porta� �nica no host. Porta � identificada no pacote IP*.
4.	**Como uma aplica��o cliente sabe qual a porta de uma aplica��o servidora para poder enviar pacotes?** <br/> > *Alguns servi�os t�m n�meros de portas j� convencionadas (portas �bem conhecidas�)*.

**N�meros de portas**

**1-255**		  Reservadas para servi�os padr�o portas �bem conhecidas�.
**256-1023** 	Reservado para servi�os Unix. 
**1-1023** 		Somente podem ser usadas por super-usu�rio.
**1024-4999** Usadas por processos de sistema e de usu�rio.
**5000-** 		Usadas somente por processos de usu�rio.

## Demultiplexa��o/Multiplexa��o

*	**Demultiplexa��o no hospedeiro receptor**:
  *	Entrega os segmentos recebidos ao socket correto
*	**Multiplexa��o no hospedeiro receptor**:
  *	Coleta dados de m�ltiplos sockets, envelopa os dado com cabe�alho (usado depois para demultiplexa��o). 

*	**Computador recebe datagramas IP**
  *	Cada datagrama possui endere�o IP de origem e IP de destino 
  *	Cada datagrama carrega 1 segmento da camada de transporte
  *	Cada segmento possui n�meros de porta de origem e destino (lembre-se: n�meros de porta bem conhecidos para aplica��es espec�ficas)
  *	O hospedeiro usa endere�os IP e n�meros de porta para direcionar o segmento ao socket apropriado.

*	**UDP**:
*	**Socket UDP** identificado por dois valores: (endere�o IP de destino, n�mero da porta de destino)
  *	Quando o hospedeiro recebe o segmento UDP: 
    *	Verifica o n�mero da porta de destino no segmento
    *	Direciona o segmento UDP para o socket com este n�mero de porta 
  *	Datagramas com IP de origem diferentes e/ou portas de origem diferentes s�o direcionados para o mesmo socket.

*	**TCP**:
*	**Socket TCP** identificado por 4 valores: 
  *	Endere�o IP de origem
  *	Endere�o porta de origem 
  *	Endere�o IP de destino
  *	Endere�o porta de destino
* Hospedeiro receptor usa os quatro valores para direcionar o segmento ao socket apropriado 
* Hospedeiro servidor pode suportar v�rios sockets TCP simult�neos:
  *	Cada socket � identificado pelos seus pr�prios 4 valores
  *	Servidores possuem sockets diferentes para cada cliente conectado.

## UDP: User Datagram Protocol

O UDP � um protocolo da camada de transporte n�o confi�vel e n�o-orientado � conex�o. Fornece apenas os servi�os de endere�amento e fragmenta��o, n�o provendo confiabilidade (controle de fluxo, erro, congestionamento). Isso indica que o UDP n�o adiciona servi�os ao protocolo IP. O que nos leva ent�o a utilizar o UDP?

O UDP por ser mais simples possui um cabe�alho menor gerando um menor overhead. Ideal para algumas aplica��es onde a velocidade � mais �til que a confiabilidade como aplica��es multim�dia. Afinal n�o faz sentido algum receber um trecho de um arquivo m�sica que j� passou.

Al�m de aplica��es multim�dia, o UDP � utilizado tamb�m pelo TFTP (Trivial File Transfer Protocol), RIP (Routing Information Protocol), SNMP (Simple Network Management Protocol) e DNS (Domain Name System).

*	Servi�o �best effort�, segmentos **UDP** podem ser:
  *	**Perdidos** ou **Entregues** fora de ordem para a aplica��o
*	Sem conex�o:
  *	N�o h� apresenta��o entre o **UDP** transmissor e o receptor.
  *	Cada segmento UDP � tratado de forma independente dos outros.
*	Por que existe um **UDP**?
  *	N�o h� estabelecimento de conex�o (que possa resultar em atrasos).
  *	Simples: n�o h� estado de conex�o nem no transmissor, nem no receptor.
  *	Cabe�alho de segmento reduzido.
  *	N�o h� controle de congestionamento: **UDP** pode enviar segmentos t�o r�pido quanto desejado (e poss�vel).
  *	Muito usado por aplica��es de multim�dia cont�nua (streaming) **UDP**:
  *	Tolerantes � perda.
  *	Sens�veis � taxa.
  *	Transfer�ncia confi�vel sobre **UDP**: acrescentar confiabilidade na camada de aplica��o
  *	Recupera��o de erro espec�fica de cada aplica��o.

### UDP Checksum

Objetivo: detectar �erros� (ex.: bits trocados) no segmento transmitido

*	**Transmissor**:
  *	Trata o conte�do do segmento como sequ�ncia de inteiros de 16 bits 
  *	Checksum: soma (complemento de 1 da soma) do conte�do do segmento 
  *	Transmissor coloca o valor do checksum no campo de checksum do UDP 
*	**Receptor**:
  *	Computa o checksum do segmento recebido
  *	Verifica se o checksum calculado � igual ao valor do campo checksum:
  * N�O - erro detectado
  *	SIM - n�o h� erros. Mas talvez haja erros apesar disso? Mas depois�

## Princ�pios de transfer�ncia confi�vel de dados

Importante nas camadas de aplica��o, transporte e enlace. Caracter�sticas dos canais n�o confi�veis determinar�o a complexidade dos protocolos confi�veis de transfer�ncia de dados (rdt).

### Transfer�ncia confi�vel usando um canal com erro de bits
*	Canal subjacente pode trocar valores dos bits num pacote
  *	Checksum para detectar erros de bits
*	A quest�o: como recuperar esses erros:
  *	**Reconhecimentos** (**ACKs**): receptor avisa explicitamente ao transmissor que o pacote foi recebido corretamente 
  *	**Reconhecimentos negativos** (**NAKs**): receptor avisa explicitamente ao transmissor que o pacote tem erros 
  *	Transmissor reenvia o pacote quando da recep��o de um NAK
*	Mecanismos necess�rios: 
  *	Detec��o de erros
  *	Retorno do receptor: mensagens de controle 
  *	(ACK, NAK) rcvr->sender

### Transfer�ncia confi�vel usando um canal com erro de bits e perdas

O que acontece se o **ACK/NAK** � corrompido ou perdido? 

*	Transmissor n�o sabe o que aconteceu no receptor!
*	Transmissor deve esperar durante um tempo razo�vel pelo ACK e se n�o receb�-lo deve retransmitir a informa��o
*	N�o pode apenas retransmitir: poss�vel duplicata 

Tratando duplicatas: 

*	Transmissor acrescenta n�mero de seq��ncia em cada pacote
*	Transmissor reenvia o �ltimo pacote se ACK/NAK for perdido
*	Receptor descarta (n�o passa para a aplica��o) pacotes duplicados.
	
###	Estrat�gias de Retransmiss�o

*	Conhecidos como algoritmos ou protocolos Automatic Repeat Request (**ARQ**)
*	Quest�es de projeto:
  *	Como o receptor requisita uma retransmiss�o?
  *	Como a fonte sabe quando retransmitir?
*	Desempenho e exatid�o
*	Para simplificar as explica��es assumimos comunica��es do tipo ponto-a-ponto
*	Mesmas solu��es adotadas pela camada de enlace:
  *	Verifica��o de erros (checksum)
  *	Retransmiss�o
  *	Temporiza��o
  *	N�mero de sequ�ncia
  *	Pipelining
  *	Janela deslizante

## O Protocolo TCP

O TCP � o protocolo da camada de transporte da arquitetura Internet respons�vel em oferecer confiabilidade na transmiss�o. O TCP fornece um **servi�o orientado � conex�o, confi�vel e full-duplex** para os servi�os de aplica��o. 

O TCP � **orientado a conex�o** � Para ter o controle dos pacotes enviados e conseguir efetuar a fragmenta��o, o TCP precisa que os usu�rios finais tenham o controle do que est� sendo enviado. O protocolo TCP especifica tr�s fases durante uma conex�o: estabelecimento da liga��o, transfer�ncia e t�rmino de liga��o. Para estabelecimento da conex�o o TCP necessita que:

> *�O cliente inicia a liga��o enviando um pacote TCP com a flag SYN activa e espera-se que o servidor aceite a liga��o enviando um pacote SYN+ACK. Se, durante um determinado espa�o de tempo, esse pacote n�o for recebido ocorre um timeout e o pacote SYN � reenviado. O estabelecimento da liga��o � conclu�do por parte do cliente, confirmando a aceita��o do servidor respondendo-lhe com um pacote ACK�.*

Efetua desconex�o �suave� (**Graceful Connection Shutdown**) � O TCP s� encerra a conex�o depois de entregar os dados ao receptor.

O **TCP � Full-duplex** - � poss�vel a transfer�ncia simult�nea nas duas dire��es durante a sess�o.

Utiliza o conceito de stream � O TCP envia uma **sequ�ncia limitada e cont�nua de bytes** sem no��o dos registros ou quantidade de pacotes que ser�o recebidos.

Enxerga a rede como uma conex�o **ponto-a-ponto** � O protocolo TCP fornece uma conex�o diretamente entre aplicativos dos hosts. Tal conex�o � denominada conex�o virtual ponto-a-ponto, entre o transmissor e receptor, os dispositivos de rede (roteadores) n�o enxergam a camada de transporte.

O TCP permite a camada de aplica��o enxergar a rede como uma conex�o virtual.

### Estrutura do Segmento TCP

![Segmento TCP]()

### N�mero de Sequ�ncia e ACKs no TCP

*	N�meros de seq��ncia:
  *	N�mero do primeiro byte nos segmentos de dados 
*	ACKs: 
  *	N�mero do pr�ximo byte esperado do outro lado
  *	ACK cumulativo 

![Sequ�ncia ACKs]()

1.	**Como o receptor trata segmentos fora de ordem?** <br/> > *A especifica��o do TCP n�o define, fica a crit�rio do implementador*.

### TCP Round Trip Time e temporiza��o

1.	**Como escolher o valor da temporiza��o do TCP?**

* **Maior que o RTT**
  *	*Nota: RTT varia*
*	**Muito curto**: *temporiza��o prematura*
  *	*Retransmiss�es desnecess�rias*
*	**Muito longo**: *a rea��o � perda de segmento fica lenta*

2.	**Como estimar o RTT?**

*	**SampleRTT**: *tempo medido da transmiss�o de um segmento at� a respectiva confirma��o*
  *	*Ignora retransmiss�es e segmentos reconhecidos de forma cumulativa**
*	**SampleRTT** varia de forma r�pida, � desej�vel um amortecedor para a estimativa do RTT
  *	*Usar v�rias medidas recentes, n�o apenas o �ltimo SampleRTT obtido*

![TCP Round Trip]()




**** | **** 
:---: | :---: 
 | 
 | 
 | 
 |
 

![Modelo TCP/IP](https://i.imgur.com/F7A7wmr.png)
