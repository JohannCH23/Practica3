<h3> #Practica 3 - Johan Erazo </h3>

<h2>1-Realiza unha consulta "dig danielcastelao.org" e identific cada parte da resposta (IN, CNAME, A, QUERY SECTION, ANSWER SECTION, AUTHORITY SECTION, etc)</h2>

Para empezar, teremos que lanzar o comando: (dig danielcastelao.org), que nos mostrará unha variedade de datos onde aparecen os seguintes:

    QUESTION SECTION: Amósanos o tipo de rexistro solicitado.
    
    IN: Isto aparece como referencia ao tipo de consulta.
    
    A: Este devolve a IP asociada co nome de dominio solicitado.
    
    ANSWER SECTION: É a resposta á consulta, onde se nos devolve a IP do dominio solicitado.
    
    ADDITIONAL SECTION: Inclúe información adicional como a IP dos servidores DNS autoritativos.
    
    AUTHORITY SECTION: Indícanos os servidores DNS autoritativos para o dominio.

<h2>2-Realiza consutas dos seguintes nomes e identifica as diferencias: moodle.danielcastelao.org, www.danielcastelao.org</h2>

Primeiro facemos os comandos respectivos para velos: (dig moodle.danielcastelao.org) e (dig www.danielcastelao.org). Xa con estes datos, observamos as diferenzas.

En primeiro lugar, vemos que moodle.danielcastelao.org é un subdominio de www.danielcastelao.org, e mostraranos a IP e un alias que redirixe a outro dominio.

Despois, observamos que en www.danielcastelao.org, ao ser o dominio principal, devolve a mesma dirección IP, a diferenza do subdominio.

<h2>3-Averigua o nome e IP dos servidores de DNS autoritativos de www.danielcastelao.org, por qué soen ser 2 servidores autoritativos?</h2>

Para ver isto, executamos o comando: (dig NS danielcastelao.org), co que podemos ver que os nomes e IP dos servidores son: (ms1.hover.com.) e (dnsmaster.hover.com.).

Isto faise para que, se un dos dous falla, o outro poida seguir funcionando, proporcionando así redundancia e tolerancia a erros.

<h2>4-Realiza as consultas de nomes inversas: 130.206.164.68 e de outras dúas IPs que se che ocorran.</h2>

Para isto, executamos o comando: (dig -x 130.206.164.68). Co parámetro -x móstranos o nome asociado á IP. Neste caso, devolve os dous nomes de DNS que serían: (pluto.tlm.unavarra.es.) e (s164m68.unavarra.es.). Para as outras dúas, seguimos o mesmo procedemento.

<h2>5-A qué servidor DNS estás consultando? Cómo o podes cambiar sen tocar os ficheiros de configuración do sistema?</h2>

Revísase co comando: (nslookup) e, xa dentro, executamos o comando (dig @8.8.8.8 www.danielcastelao.org). Con isto, visualizamos o servidor e a dirección (server e address).

<h2>6-Obtén o rexistro SOA (Start of Authority) do dominio  moodle.danielcastelao.org preguntándolle ó servidor DNS de google e logo preoguntándollo directamente ó servidor primario do dominio danielcastelao.org.</h2>

Para obter o rexistro, usamos o comando: (dig @8.8.8.8 SOA moodle.danielcastelao.org) para consultar o rexistro usando os DNS de Google.

A continuación, para consultar o servidor primario con NS, facémolo así: (dig danielcastelao.org NS). Co servidor autoritativo, podemos facer a consulta da seguinte maneira: (dig @ns1.hover.com. SOA moodle.danielcastelao.org).

<h2>7-Consulta a IP de www.elpais.com. Cánto tempo queda almaceado o rexistro de recurso no DNS local?, se preguntas ó DNS local por este recurso, qué observas no TTL do rexistro?</h2>

Para consultar, facemos o comando: (dig www.elpais.com). Observamos o campo **TTL** para ver o tempo do rexistro, ou o campo **Query time: 22 msec**, que nos indica o tempo da consulta.

<h2>8-Busca o TTL de distintos nomes de dominio de servicios que escollas, a qué se poden deber as diferencias?</h2>

Aquí facemos o comando: (dig www.google.com) e (dig www.facebook.com), e no tempo indícanos **23 msec** sen diferenza.

<h2>9-Determina o TTL máximo (original) dun nome de dominio.</h2>

Para isto, o **TTL máximo** e o **valor inicial** aparecen na resposta do comando dig.

<h2>10-Averigua cántas máquinas con distintas IPs están detrás do dominio web www.google.es, sempre son as mesmas e na mesma orde? por qué?</h2>

Necesitaremos usar o comando: (dig @J.ROOT-SERVERS.NET www.google.es) e amosaranse múltiples IPs. Isto ocorre porque Google ten servidores por todo o mundo. Debido á rotación de servidores e á optimización, a orde pode variar.

<h2>11-Pregunta o mesmo a un server raiz (J.ROOTSERVERS.NET por exemplo) e comproba na resposta se o server acepta o modo recursivo</h2>

Para proceder, debemos executar o comando: (dig @J.ROOTSERVERS.NET j.rootservers.net). Coa execución, recibirémos un aviso que di: **"RECURSION REQUESTED BUT NOT AVAILABLE"**.

Xa con isto, sabremos que a recursión non está dispoñible.

<h2>12-Se queremos ver tóda-las queries que fai o servidor de DNS, qué opción temos que usar? averigua a IP de www.timesonline.co.uk, especifica os pasos dados</h2>

Para velo, temos que executar o comando: (dig +trace www.timesonline.co.uk). Con isto, veremos todas as consultas feitas ata a última.

Para averiguar a IP, utilizamos: (dig www.timesonline.co.uk) e miramos onde pon **ANSWER** para ver a IP.

<h2>13-Usando a información dispoñible a traveso do DNS especifica a máquina (nome e IP) ou máquinas que actúan como servers de correo do dominio danielcastelao.org</h2>

Empezamos executando o comando: (dig ms danielcastelao.org). Podemos ver que o nome é **danielcastelao.org**, e a IP é **178.211.133.37**. A que actúa como servidor é a IP **127.0.0.53**.

<h2>14-Podes obter os rexistros AAAA de www.facebook.com? a qué corresponden?</h2>

Para poder facelo, executamos o comando: (dig AAAA www.facebook.com). Saldrá a información correspondente á IPV6.