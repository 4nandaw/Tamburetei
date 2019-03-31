# Camada de Aplica��o

## Sum�rio
- [Camada de Aplica��o](#camada-de-aplica��o)
  - [Sum�rio](#sum�rio)
  - [Arquiteturas de Aplica��o](#arquiteturas-de-aplica��o)
  - [Servi�os dos protocolos de transporte da Internet](#servi�os-dos-protocolos-de-transporte-da-internet)
  - [HTTP - Hypertext Transfer Protocol](#http---hypertext-transfer-protocol)
    - [Vis�o geral](#vis�o-geral)
    - [Modelagem do Tempo de Resposta](#modelagem-do-tempo-de-resposta)
    - [Conex�o HTTP](#conex�o-http)

A camada de aplica��o � uma camada de abstra��o que engloba protocolos que realizam a comunica��o fim-a-fim entre aplica��es. � respons�vel por prover servi�os para aplica��es de modo a separar a exist�ncia de comunica��o em rede entre processos de diferentes computadores. 

Ela, basicamente, cria as especifica��es de como ser� a comunica��o entre duas aplica��es entre hosts. 

**O protocolo da camada de aplica��o define**:

*	Tipo das mensagens trocadas, mensagens de requisi��o e resposta;
*	Sintaxe dos tipos de mensagem: os campos nas mensagens e como s�o delineados ;
*	Sem�ntica dos campos, ou seja, significado da informa��o nos campos; 
*	Regras para quando e como os processos enviam e respondem �s mensagens.

**De qual servi�o de transporte uma aplica��o necessita?**

*	Perda de dados  
  *	Algumas aplica��es (ex.: �udio) podem tolerar alguma perda
  *	Outras aplica��es (ex.: transfer�ncia de arquivos, sess�o remota) exigem transfer�ncia de dados 100% confi�vel
*	Temporiza��o
  *	Algumas aplica��es (ex.: telefonia IP, jogos interativos) exigem baixos atrasos para serem �efetivos�
*	Banda passante
  *	Algumas aplica��es (ex.: multim�dia) exigem uma banda m�nima para serem �efetivas�
  *	Outras aplica��es (�aplica��es el�sticas�) melhoram quando a banda dispon�vel aumenta

## Arquiteturas de Aplica��o:

*	**Cliente-Servidor**.
  *	Servidor: 
    *	Hospedeiro sempre ativo
    *	Endere�o IP permanente
    *	Fornece servi�os solicitados pelo cliente
  *	Clientes:  
    *	Comunicam-se com o servidor  
    *	Pode ser conectado intermitentemente
    *	Pode ter endere�o IP din�mico
    *	N�o se comunicam diretamente uns com os outros
* **P2P**
  *	Nem sempre no servidor 
  *	 Sistemas finais arbitr�rios comunicam-se diretamente
  *	Pares s�o intermitentemente conectados e trocam endere�os IP
    *	Ex.: Gnutella
  *	Altamente escal�veis, mas dif�ceis de gerenciar
* **H�brida**
  *	Napster  
    *	Transfer�ncia de arquivo P2P
    *	Busca centralizada de arquivos:  
      *	Conte�do de registro dos pares no servidor central  
      *	Consulta de pares no mesmo servidor central para localizar o conte�do
  *	Instant messaging
    *	Bate-papo entre dois usu�rios � P2P
    *	Detec��o/localiza��o de presen�a � centralizada:  
      *	Usu�rio registra seu endere�o IP com o servidor central quando fica on-line.
      *	Usu�rio contata o servidor central para encontrar endere�os IP dos �amigos�.

## Servi�os dos protocolos de transporte da Internet

**Servi�o TCP**:
  
*	Orientado � conex�o: conex�o requerida entre processos cliente e servidor 
*	Transporte confi�vel entre os processos de envio e recep��o
*	Controle de fluxo: o transmissor n�o sobrecarrega o receptor  
*	Controle de congestionamento: protege a rede do excesso de tr�fego
*	**N�o oferece**: garantias de temporiza��o e de banda m�nima

**Servi�o UDP**: 

*	Transfer�ncia de dados n�o confi�vel entre os processos transmissor e receptor  
*	**N�o oferece**: estabelecimento de conex�o, controle de fluxo e de congestionamento, garantia de temporiza��o e de banda m�nima.

## HTTP - Hypertext Transfer Protocol

### Vis�o geral:

*	Protocolo da camada de aplica��o da Web
*	Modelo cliente/servidor 
  *	Cliente: navegador que solicita, recebe e apresenta objetos da Web
  *	Servidor: envia objetos em resposta a pedidos  
*	HTTP 1.0: RFC 1945
*	HTTP 1.1: RFC 2068
*	Utiliza TCP: 
  *	Cliente inicia conex�o TCP (cria socket) para o servidor na porta 80
  *	Servidor aceita uma conex�o TCP do cliente
  *	Mensagens HTTP (mensagens do protocolo de camada de aplica��o) s�o trocadas entre o browser (cliente HTTP) e o servidor Web (servidor HTTP) 
  *	 A conex�o TCP � fechada
*	HTTP � �stateless�
  *	Por default, o servidor n�o mant�m informa��o sobre os pedidos passados pelos clientes
  *	Protocolos que mant�m informa��es de �estado� s�o complexos!
  *	Hist�rico do passado (estado) deve ser mantido
  *	Se o servidor/cliente quebra, suas vis�es de �estado� podem ser inconsistentes, devendo ser reconciliadas

### Modelagem do Tempo de Resposta

*	Defini��o de RTT: tempo para enviar um pequeno pacote que vai do cliente para o servidor e retorna.
*	Tempo de resposta:  
  *	Um RTT para iniciar a conex�o TCP
  *	Um RTT para requisi��o HTTP e primeiros bytes da resposta HTTP para retorno
  *	Tempo de transmiss�o de arquivo
* Total = 2 RTT+ tempo de transmiss�o

### Conex�o HTTP

* HTTP n�o persistente
  *	No m�ximo, um objeto � enviado sobre uma conex�o TCP
  *	O HTTP/1.0 utiliza HTTP n�o persistente
  *	Caracter�sticas do HTTP n�o persistente:  Requer 2 RTTs por objeto
  *	Sistema Operacional deve manipular e alocar recursos do hospedeiro para cada conex�o TCP (Mas os browsers freq�entemente abrem conex�es TCP paralelas para buscar objetos referenciados)
	
*	HTTP persistente
  *	M�ltiplos objetos podem ser enviados sobre uma conex�o
    *	TCP entre o cliente e o servidor 
  *	O HTTP/1.1 utiliza conex�es persistentes em seu modo padr�o
  *	HTTP persistente
  *	Servidor deixa a conex�o aberta ap�s enviar uma resposta
  *	Mensagens HTTP subsequentes entre o mesmo cliente/servidor s�o enviadas pela conex�o
  *	Persistente sem pipelining:  O cliente emite novas requisi��es apenas quando a resposta anterior for recebida
  *	Um RTT para cada objeto referenciado
  *	Persistente com pipelining:  Padr�o no HTTP/1.1
  *	O cliente envia requisi��es assim que encontra um objeto referenciado
  *	T�o curto quanto um RTT para todos os objetos referenciados