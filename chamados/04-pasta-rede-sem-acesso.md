# Chamado 04 — Usuário não consegue acessar pasta compartilhada

**Cenário de laboratório:** o usuário informa que uma pasta compartilhada da rede que ele costuma utilizar não está abrindo.

## Entendendo o chamado

Antes de alterar permissões, eu tentaria descobrir o alcance do problema.

Perguntaria se a pasta já funcionava para aquele usuário, quando parou de funcionar e se outras pessoas conseguem acessá-la normalmente. Também confirmaria o caminho que ele está tentando abrir.

Exemplo de caminho de rede:

```text
\\servidor\documentos
```

Se ninguém consegue acessar, eu investigaria primeiro a rede ou o equipamento que hospeda o compartilhamento. Se somente um usuário apresenta o problema, a investigação muda de direção.

## 1. Verificar a rede do computador

Primeiro confirmaria se a máquina está conectada normalmente à rede.

```bat
ipconfig
```

Depois testaria a comunicação com o servidor pelo nome:

```bat
ping servidor
```

Se eu souber o IP do equipamento, também posso testar diretamente:

```bat
ping 192.168.1.10
```

É importante lembrar que um servidor pode estar configurado para não responder a ping. Por isso, falha nesse teste sozinha não prova que ele está fora do ar.

## 2. Nome do servidor e DNS

Se o acesso pelo IP funcionar, mas pelo nome não, eu verificaria resolução de nomes.

```bat
nslookup servidor
```

Também conferiria as configurações recebidas pela máquina:

```bat
ipconfig /all
```

## 3. Testar o caminho compartilhado

No Explorador de Arquivos ou em `Win + R`, tentaria abrir diretamente:

```text
\\servidor\documentos
```

Se o Windows informar que o caminho não existe, eu investigaria conectividade, nome do servidor e disponibilidade do compartilhamento.

Se a mensagem for de **acesso negado**, o foco passa a ser autenticação e permissões.

## 4. Unidades de rede

Para conferir conexões de rede existentes:

```bat
net use
```

Uma unidade mapeada pode continuar apontando para um caminho antigo ou apresentar problema de autenticação.

Eu evitaria remover todos os mapeamentos do usuário sem antes identificar qual conexão está com problema.

## 5. Permissões

Se a rede estiver funcionando e o compartilhamento estiver disponível para outros usuários, eu verificaria se aquele usuário realmente deveria possuir acesso à pasta.

Em um ambiente corporativo, não adicionaria permissões por conta própria somente para encerrar o chamado. Confirmaria a regra da empresa e, quando necessário, encaminharia a solicitação para quem administra os acessos.

Também levaria em consideração que permissões de compartilhamento e permissões do sistema de arquivos podem trabalhar em conjunto.

## 6. Credenciais

Se houver suspeita de credencial antiga salva no computador, verificaria o **Gerenciador de Credenciais do Windows**.

Eu não pediria a senha do usuário para anotar no chamado e não registraria senhas em documentação.

## Validação

Após a correção, pediria para o próprio usuário abrir a pasta e acessar um arquivo que faça parte da rotina dele, respeitando o nível de permissão que deveria possuir.

## Exemplo de registro do chamado

> Usuário relatou falha ao acessar pasta compartilhada. Conectividade com a rede e disponibilidade do servidor verificadas. O compartilhamento estava disponível para outros usuários e foi identificado problema relacionado ao acesso da conta. Após ajuste conforme a política de permissões do ambiente, o acesso foi validado com o usuário.

## O que pratiquei neste caso

- separar falha de rede de falha de permissão;
- testar comunicação por nome e por IP;
- entender o uso de caminhos UNC (`\\servidor\pasta`);
- consultar unidades de rede com `net use`;
- diferenciar resolução de nomes, autenticação e autorização;
- tratar permissões com cuidado em um ambiente corporativo.
