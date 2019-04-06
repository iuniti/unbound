# unbound

# instalação das dependencias
apt-get install unbound nano wget dnsutils dnstop zabbix-agent -y

cd /etc/unbound/unbound.conf.d
rm root-auto-trust-anchor-file.conf
nano nomedoarquivo.conf

# cole o arquivo que esta como unbound.conf na pasta do curso e 
altere a acl
memoria
processamento
ativar ipv6
colocar interface ::1

# volte com o dns para a maquina porque ela altera para 127.0.0.1
echo nameserver 8.8.8.8 > /etc/resolv.conf

# Ir para a pasta do unbound e baixar o arquivo com os endereços dos root server
/etc/unbound
wget http://www.internic.net/domain/named.root

# Renomear o arquivo de named.conf para root.hints
mv named.root root.hints

	
# Cria a chave de criptografia para o funcionamento do DNSSEC
unbound-anchor -v

chown unbound.unbound /etc/unbound/ -R
/etc/init.d/unbound stop
/etc/init.d/unbound start

ps ax | grep unbound

	Teste DNS
	dig www.uol.com.br @127.0.0.1
	dig www.uol.com.br AAAA para ipv6
	dig www.uol.com.br A @127.0.0.1
	dig www.uol.com.br AAAA @2804:213c:1::26
================================================================================================================
# caso precise fazer troubleshooting

nano /etc/unbound/unbound.conf.d/nomedoarquivo.conf

# log queries - em tempo real, nao deixar habilitado em producao.(caminho do arquivo de log)
log-queries: /etc/unbound/unbound.log
 
 
# log verbosity (nivel do log)
verbosity: 5

touch /etc/unbound/unbound.log

chown unbound.unbound /etc/unbound/ -R
/etc/init.d/unbound restart

===============================================================================================================
dnstop ens32
dnstop ens32 -l 4

#log queries
log-queries: yes

#nao usar syslog /var/log/syslog
use-syslog: no

================================================================================================================

# instalar o template no zabbix server
# instalar o template no grafana server
# adicionar o UserParameter no zabbix-agent, colocar o servidor e da permição sudo para o usuario zabbix no visudo
