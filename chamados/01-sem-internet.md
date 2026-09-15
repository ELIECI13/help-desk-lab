# Chamado 01 — Computador sem acesso à internet

**Cenário de laboratório:** o usuário informa que o computador está conectado à rede, mas nenhum site abre.

## Antes de mexer

Eu começaria tentando descobrir se o problema está só naquela máquina ou se outras pessoas também estão sem acesso. Também perguntaria quando começou e se houve alguma mudança antes da falha.

Isso evita sair alterando configuração sem saber onde está o problema.

## 1. Conferência inicial

Primeiro verificaria o básico:

- cabo de rede ou conexão Wi-Fi;
- ícone de rede do Windows;
- se o adaptador está habilitado;
- se outros equipamentos da mesma rede conseguem navegar.

Depois abriria o Prompt de Comando:

```bat
ipconfig /all
```

Aqui eu procuraria principalmente endereço IPv4, gateway padrão e servidores DNS.

Se a máquina recebeu um endereço `169.254.x.x`, eu investigaria primeiro por que ela não conseguiu obter um IP válido do DHCP.

## 2. Testes de conectividade

Testaria o próprio TCP/IP:

```bat
ping 127.0.0.1
```

Depois o gateway da rede. Exemplo:

```bat
ping 192.168.1.1
```

Em seguida faria um teste por IP externo:

```bat
ping 8.8.8.8
```

E por nome:

```bat
ping google.com
```

Se o IP externo responder e o nome não, DNS passa a ser uma das principais suspeitas.

## 3. DNS

Para conferir a resolução de nomes:

```bat
nslookup google.com
```

Também posso limpar o cache DNS do computador:

```bat
ipconfig /flushdns
```

Eu não trocaria o DNS da máquina logo de início. Primeiro tentaria identificar se o servidor configurado realmente é a causa.

## 4. Renovação do endereço

Se houver indício de problema na configuração recebida por DHCP, posso testar:

```bat
ipconfig /release
ipconfig /renew
```

Antes disso, confirmaria que a interface usada é realmente configurada por DHCP.

## 5. Se ainda não funcionar

Eu verificaria, conforme o ambiente:

- proxy configurado no Windows ou navegador;
- VPN;
- firewall;
- driver/adaptador de rede;
- status do roteador, switch ou ponto de acesso;
- se o problema afeta outros usuários.

Também usaria:

```bat
tracert 8.8.8.8
```

para ter mais uma pista de onde a comunicação está parando.

## Exemplo de encerramento do chamado

> Usuário relatou falta de acesso à internet. Conectividade local verificada e configuração IP conferida. Após os testes, foi identificado problema de resolução de nomes. Cache DNS limpo e acesso validado novamente com o usuário.

## O que pratiquei neste caso

- separar problema local de problema geral;
- conferir IP, gateway e DNS;
- testar conectividade em etapas;
- não aplicar uma solução antes de levantar evidências;
- registrar de forma curta o que foi feito.
