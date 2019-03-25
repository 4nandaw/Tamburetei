# Camada F�sica

## Sum�rio
- [Camada F�sica](#camada-f�sica)
  - [Sum�rio](#sum�rio)
  - [Hist�rico](#hist�rico)
    - [Evolu��o na Comunica��o e Processamento](#evolu��o-na-comunica��o-e-processamento)
  - [Defini��es e Conceitos](#defini��es-e-conceitos)
    - [O que � Internet?](#o-que-�-internet-?)
    - [O que s�o RFCs e a IETF?](#o-que-s�o-rfcs-e-a-ietf-?)
    - [Conceito de Redes de Computadores](#conceito-de-edes-de-computadores)
    - [O que � Protocolo?](#o-que-�-protocolo-?)
    - [Servi�o Orientado a Conex�o](#servi�o-orientado-a-conex�o)
  - [TCP/IP](#tcp/ip)
    - [Modelo TCP/IP](#modelo-tcp/ip)    


## Hist�rico

### Evolu��o na Comunica��o e Processamento

A necessidade de comunica��o, assim como o instinto de sobreviv�ncia, � inerente aos seres humanos desde seu surgimento. Das pinturas rupestres, pombo-correio, at� a populariza��o da Internet, s�o mais de 30.000 anos de hist�ria evolutiva dos meios de comunica��o.

> *�Cada um dos tr�s s�culos anteriores foi dominado por um a �nica tecnologia. O S�culo XVIII foi a �poca dos grandes sistemas mec�nicos que acompanharam a Revolu��o Industrial. O S�culo XIX foi a era das m�quinas a vapor. As principais conquistas tecnol�gicas do S�culo XX se deram no campo da aquisi��o, do processamento e da distribui��o de informa��es. Entre outros desenvolvimentos, vimos a instala��o das redes de telefonia em escala mundial, a inven��o do r�dio e da televis�o, o nascimento e o crescimento sem precedentes da ind�stria de inform�tica e o lan�amento dos sat�lites de comunica��o.�* (TANENBAUM)

No caso espec�fico do surgimento da Internet, o contexto hist�rico � o seguinte - Guerra Fria. O mundo ainda est� se recuperando dos destro�os remanescentes da segunda guerra mundial e o clima de paz � mais falso que a amizade entre USA e a antiga URSS. 

A comunica��o entre as bases militares tornou-se algo crucial e assunto de primeira ordem - quem tem mais informa��o consequentemente ganha a guerra. Assim, fica evidente a necessidade da cria��o de algo novo, uma nova forma de inter-comunicar essas bases� a internet! Ou pelo menos os primeiros passos dela. A internet surge ent�o, bem como outras incont�veis tecnologias, de forma n�o-exatamente-intencional. 

Em 1969, a empresa de ARPA (Advanced Research and Projects Agency), resolveu criar a famosa e saudosa (n�o pelos sovi�ticos, claro) ARPANet. Ela tinha como principal objetivo interligar as bases militares e os departamentos de pesquisas do governo americano. O projeto nasce com a guerra, mas chegado o seu fim e o sucesso dos americanos, qual o futuro da ARPANet? Depois de ser amplamente utilizada durante os embates, os militares decidiram �passar a guarda� para os cientistas, depois para as grandes universidades e assim foi sendo aprimorada e difundida (dando um grande pulo hist�rico). 

A tabela abaixo explica um pouco da evolu��o dos computadores e processamento.

**Gera��o** | **Computadores** | **Processamento** 
:---: | :---: | :---:
**Primeira Gera��o (1940-1959)** | Exemplo: ENIAC. V�lvulas e circuitos. Ocupava o espa�o de um pr�dio. | Processamento batch: ocorre atrav�s de um lote de tarefas enfileiradas. Feito manualmente por uma equipe.
**Segunda Gera��o (1959-1965)** | Exemplo: IBM 7094. V�lvulas foram substitu�das por transistores, o que diminuiu o tamanho dos computadores, permitindo o in�cio de seu uso comercial. | Os primeiros terminais interativos surgiram, onde os usu�rios poderiam acessar o computador central pelas linhas de comunica��o.
**Terceira Gera��o (1965-1975)** | A populariza��o dos circuitos integrados contribuiu para, al�m de baratear o custo dos computadores, diminuir ainda mais seu tamanho, sendo agora poss�vel a ideia de computadores pessoais. | Come�o da descentraliza��o e individualiza��o no processamento e servi�os, a partir da d�cada de 70.
**Quarta Gera��o (1975-hoje)** | Populariza��o e crescente dos computadores pessoais. | Sistemas distribu�dos e redes locais.

## Defini��es e Conceitos

### O que � Internet?

Kurose-Ross, no livro Redes de Computadores e a Internet, fala que podemos definir a Internet como �uma infraestrutura de rede que prov� servi�os para aplica��es distribu�das. � Claro que essa defini��o � bastante rasa, mas por meio dela � poss�vel entender a ponta do iceberg.

Na Internet, existem dois conceitos essenciais para sua forma de comunica��o: hospedeiros e sistemas finais. Um sistema final s�o todos os computadores interligados na periferia da Internet. Hospedeiros (ou hosts) � um sistema final que, como o nome j� adianta, hospeda uma aplica��o/servi�o.

Segundo Kurose-Ross (vai ter muito ele aqui mesmo), �Sistemas finais n�o s�o interligados diretamente por um �nico enlace de comunica��o. Em vez disso, s�o interconectados indiretamente por equipamentos intermedi�rios de comuta��o conhecidos como comutadores de pacotes.� Um exemplo de comutador de pacotes s�o roteadores, que encaminham pacotes (bloco de dados) para seus destinos finais.

Os sistemas finais s�o conectados entre si por enlaces de comunica��o, como por exemplo: fibra �ptica (cabeada) e ondas de r�dio (sem fio), e acessam a Internet atrav�s de ISPs (Internet Service Providers). Cada ISP � uma rede de comutadores de pacotes e enlaces de comunica��o.

### O que s�o RFCs e a IETF?

IETF - Internet Engineering Task Force. Trata-se de um grupo respons�vel por desenvolver documentos padr�es para tecnologias que cercam a Internet, os RFCs.

RFC - Request  for Comments. Elas come�aram como solicita��es gerais em coment�rios para resolver problemas que a Internet enfrentava no in�cio. Tendem a ser detalhados e t�cnicos e existem mais de 7.000.

### Conceito de Redes de Computadores

Segundo Tanenbaum, Redes de Computadores podem ser definidas como **�um conjunto de computadores aut�nomos interconectados por uma �nica tecnologia.�**

> *Dois computadores est�o interconectados quando podem trocar informa��es. A conex�o n�o precisa ser feita por um fio de cobre; tamb�m podem ser usadas fibras �pticas, micro-ondas, ondas de infravermelho e sat�lite de comunica��es. Existem redes em muitos tamanhos, modelos e formas(...). Embora possa parecer estranho para algumas pessoas, nem a Internet nem a World Wide Web � uma rede de computadores. (...) A resposta simples � que a Internet n�o � uma �nica rede, mas uma rede de redes, e a Web � um sistema distribu�do que funciona na Internet.�*

### O que � Protocolo?

Protocolo, no �mbito de redes de computadores, pode ser definido como um conjunto de padr�es e regras utilizados a fim de possibilitar a comunica��o entre dispositivos. Eles controlam o envio e a recep��o de mensagens.

Existem diversos tipos de protocolos, cada um focado em um aspecto e funcionalidade diferente. Por exemplo, o protocolo IP (Internet Protocol), que especifica o formato dos pacotes que s�o enviados e recebidos entre roteadores e sistemas finais; o SMTP (Simple Mail Transfer Protocol) para envio de e-mails e tantos outros.

* Caracter�sticas de Protocolos:
  * Especifica��o de protocolo: a descri��o do protocolo � completa e acurada.
  * Safety: um protocolo faz o que deve fazer sempre.
  *	Liveness: um protocolo � livre de deadlock.
  *	Efici�ncia: um protocolo utiliza os recursos dispon�veis de forma eficiente.
  *	Justi�a (fairness): utiliza��o justa ou contratual dos recursos.
  * Simplicidade: � desej�vel, mas n�o necess�ria.
* Desempenho de Protocolos:
  *	Atraso m�dio: tempo entre a transmiss�o do primeiro bit e a recep��o do mesmo pelo destino.
  *	Vaz�o ou Capacidade: n�mero total de bits transmitidos dividido pelo tempo total de transmiss�o.


### Servi�o Orientado a Conex�o

Trata-se de um modo de comunica��o no qual a m�quina emissora envia dados sem prevenir a m�quina receptora, e a m�quina receptora recebe os dados sem avisos de recep��o � primeira. Os dados s�o assim enviados sob a forma de blocos (datagramas). O UDP � um exemplo de protocolo n�o orientado para a conex�o. No caso do UDP, a transfer�ncia de dados n�o � confi�vel, n�o tem controle de fluxo e nem controle de congest�o. Aplica��es que utilizam UDP: Streaming media, teleconfer�ncia, DNS, telefonia IP.

## TCP/IP

### Modelo TCP/IP

TCP/IP (Transmission Control Protocol - Protocolo de Controle de Transmiss�o/ Internet Protocol - Protocolo da Internet), criado em 1969 pela U.S. Department of Defense Advanced Research Projects Agency � um conjunto de protocolos de comunica��o em camadas entre computadores em redes. Cada uma dessas camadas � respons�vel por um determinado grupo de fun��es e servi�os, sendo as camadas mais altas (aplica��o) logicamente mais perto dos usu�rios, e as mais baixas (f�sica) tendo tarefas de menor n�vel de abstra��o.

![Modelo OSI / Modelo TCP/IP](https://drive.google.com/open?id=1CDUDR7V5potF-v6NuYLXIgqg6tcUp5Vu)

Apesar de ser considerado um protocolo pesado, o TCP/IP hoje � indispens�vel. Dentre os seus muitos benef�cios est�o:
*	Padroniza��o: um padr�o, um protocolo rote�vel que � o mais completo e aceito protocolo dispon�vel atualmente. Todos os sistemas operacionais modernos oferecem suporte para o TCP/IP e a maioria das grandes redes se baseia em TCP/IP para a maior parte de seu tr�fego.
*	Interconectividade: uma tecnologia para conectar sistemas n�o similares. Muitos utilit�rios padr�es de conectividade est�o dispon�veis para acessar e transferir dados entre esses sistemas n�o similares, incluindo FTP (File Transfer Protocol) e Telnet (Terminal Emulation Protocol).
*	Roteamento: permite e habilita as tecnologias mais antigas e as novas a se conectarem � Internet. Trabalha com protocolos de linha como PPP (Point to Point Protocol) permitindo conex�o remota a partir de linha discada ou dedicada. Trabalha como os mecanismos IPCs e interfaces mais utilizados pelos sistemas operacionais, como sockets do Windows e NetBIOS.
*	Protocolo Robusto: escal�vel, multiplataforma, com estrutura para ser utilizada em sistemas operacionais cliente/servidor, permitindo a utiliza��o de aplica��es desse porte entre dois pontos distantes.
*	Internet: � atrav�s da su�te de protocolos TCP/IP que obtemos acesso a Internet. As redes locais distribuem servidores de acesso a Internet (proxy servers) e os hostslocais se conectam a esses servidores para obter o acesso a Internet. Este acesso s� pode ser conseguido se os computadores estiverem configurados para utilizar TCP/IP.

O protocolo TCP/IP se divide em quatro grandes camadas com as seguintes fun��es principais:

**Camada** | **Exemplos** | **Fun��o** 
:---: | :---: | :---:
**Aplica��o** | **HTTP, HTTPS, FTP, DNS.** <br/> �Como um web browser deve se comunicar com um servidor da web.� | Faz a comunica��o entre os programas e os protocolos de transporte. Cont�m todos os protocolos para um servi�o espec�fico de comunica��o de dados em um n�vel de processo-a-processo.
**Transporte** | **TCP, UDP, SCTP.** | Essa camada tem como fun��o controlar a comunica��o host-a-host. Ela recebe os dados enviados pela camada de aplica��o, transforma-os em pacotes menores e garante que chegar�o sem erros e na ordem certa.
**Internet** | **IP:** endere�amento IP, fragmenta��o e montagem dos pacotes. <br/> **ARP:** resolu��o do endere�o da camada de internet para o endere�o da camada de interface de rede, tais como um endere�o de hardware. | Ela � respons�vel pelo endere�amento e roteamento do pacote, fazendo a conex�o entre as redes locais. Adiciona ao pacote o endere�o IP de origem e o de destino, para que ele saiba qual o caminho deve percorrer.
**Enlace (Com interface de rede)** | **LLC, MAC.** | Essa camada � respons�vel pelo envio do datagrama recebido da camada de internet em forma de quadros atrav�s da rede f�sica.

![Modelo TCP/IP](https://drive.google.com/open?id=1jU9a0x1KNwelRvM9ZIjWHIq1piIl9Q4M)