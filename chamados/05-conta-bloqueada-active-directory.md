# Chamado 05 — Usuário não consegue entrar na conta

**Cenário de laboratório:** o usuário informa que não consegue fazer login no computador com a conta corporativa. Depois de algumas tentativas, aparece uma mensagem indicando bloqueio da conta.

> Neste caso estou estudando o fluxo de atendimento em um ambiente com domínio e Active Directory. É uma simulação de laboratório, não experiência profissional com AD.

## Primeiro eu confirmaria o problema

Antes de desbloquear ou redefinir qualquer coisa, eu confirmaria a identidade do usuário seguindo o procedimento da empresa.

Também perguntaria qual mensagem aparece na tela e se ele consegue entrar em outros serviços com a mesma conta. Isso ajuda a separar senha incorreta, conta bloqueada, senha expirada e problema de comunicação com o domínio.

## Conferindo o computador

Eu verificaria se a máquina está conectada à rede corporativa. Dependendo do ambiente, um computador fora da rede ou sem VPN pode não conseguir se comunicar corretamente com os serviços internos.

Alguns testes básicos:

```bat
ipconfig /all
```

```bat
ping servidor
```

O `ping` é apenas uma pista. Um servidor pode estar configurado para não responder ICMP.

## Active Directory

Em um laboratório com as ferramentas administrativas instaladas, eu procuraria o usuário em **Active Directory Users and Computers (ADUC)** e verificaria o estado da conta.

Eu observaria, por exemplo:

- se a conta está habilitada;
- se está bloqueada;
- se a senha expirou;
- se existe exigência de troca de senha no próximo login;
- se estou olhando a conta correta.

Se a política e meu nível de acesso permitirem, o desbloqueio seria feito somente depois de validar o usuário e entender por que a conta foi bloqueada.

## PowerShell no laboratório

Com o módulo do Active Directory disponível, um exemplo para consultar uma conta é:

```powershell
Get-ADUser -Identity usuario -Properties LockedOut, Enabled, PasswordExpired
```

Para verificar o bloqueio:

```powershell
Get-ADUser -Identity usuario -Properties LockedOut | Select-Object Name, LockedOut
```

E, em um ambiente no qual eu tenha autorização para isso, existe o comando:

```powershell
Unlock-ADAccount -Identity usuario
```

Eu não usaria esses comandos em produção sem permissão e sem seguir o procedimento de segurança da empresa.

## Por que a conta voltou a bloquear?

Se eu desbloquear a conta e ela bloquear novamente pouco tempo depois, eu não ficaria repetindo o desbloqueio.

Investigaria se existe uma senha antiga salva em algum lugar, como:

- outro computador;
- celular com e-mail corporativo;
- unidade de rede;
- VPN;
- tarefa ou serviço configurado com credencial antiga;
- Gerenciador de Credenciais do Windows.

Isso pode explicar várias tentativas automáticas com uma senha que já foi alterada.

## Redefinição de senha

Redefinir senha não seria automaticamente a primeira solução para todo bloqueio. Se for necessário, eu seguiria a política da empresa para identificação do usuário, senha temporária e troca no próximo login.

Senha nunca deve ser registrada no texto do chamado.

## Validação

Depois da correção, eu pediria para o usuário entrar novamente com a própria credencial e verificaria se os recursos necessários para o trabalho dele estão acessíveis.

## Exemplo de registro do chamado

> Usuário informou falha de autenticação na estação. Identidade validada conforme procedimento e estado da conta verificado no ambiente de domínio. Conta estava bloqueada. Após o desbloqueio autorizado, o login foi realizado novamente e validado com o usuário. Orientado a informar o suporte caso o bloqueio volte a ocorrer para investigação da origem das tentativas.

## O que pratiquei neste caso

- diferença entre senha incorreta, senha expirada e conta bloqueada;
- noções de Active Directory Users and Computers;
- consulta de usuário com PowerShell;
- importância da validação de identidade antes de alterar uma conta;
- investigação de bloqueios recorrentes;
- cuidado para não registrar senhas em chamados.
