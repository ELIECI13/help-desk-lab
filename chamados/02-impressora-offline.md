# Chamado 02 — Impressora aparece offline

**Cenário de laboratório:** o usuário tenta imprimir um documento, mas a impressora aparece como offline no Windows.

## Primeiro contato

Antes de reinstalar driver ou remover a impressora, eu tentaria entender o cenário. Perguntaria se outras pessoas conseguem imprimir nela e se o problema começou naquele momento ou já vinha acontecendo.

Também confirmaria qual impressora o usuário está tentando usar. Em um ambiente com várias impressoras isso evita perder tempo mexendo no equipamento errado.

## Verificação no equipamento

Eu começaria pelo básico:

- impressora ligada e sem mensagem de erro no painel;
- papel disponível;
- sem atolamento;
- cabo USB ou cabo de rede conectado, dependendo do modelo;
- se for uma impressora de rede, verificar se ela continua conectada à rede.

## Fila de impressão

No Windows, abriria a fila para verificar se existe algum trabalho preso.

Se houver vários documentos parados, tentaria cancelar a fila e enviar uma página de teste.

Também conferiria se as opções **Pausar impressão** ou **Usar impressora offline** foram ativadas por engano.

## Serviço de impressão do Windows

Se a fila estiver travada, verificaria o serviço **Spooler de Impressão** em `services.msc`.

Pelo PowerShell, uma forma de consultar o serviço é:

```powershell
Get-Service Spooler
```

Se o serviço estiver parado, primeiro tentaria entender o motivo. Quando fizer sentido no cenário, ele pode ser reiniciado:

```powershell
Restart-Service Spooler
```

## Se for uma impressora de rede

Eu verificaria o endereço IP configurado para a impressora e testaria a comunicação. Exemplo:

```bat
ping 192.168.1.50
```

Se não houver resposta, o problema pode estar antes do Windows: conexão da impressora, porta de rede, Wi-Fi, endereço IP alterado ou algum equipamento da rede.

Se houver comunicação com o IP, eu conferiria a porta configurada nas propriedades da impressora e compararia com o endereço atual do equipamento.

## Driver

Eu deixaria reinstalação ou atualização de driver para depois das verificações anteriores. Se outras máquinas imprimem normalmente e somente um computador apresenta erro, o driver passa a ser uma possibilidade mais forte.

## Teste final

Depois da correção, enviaria uma página de teste e pediria para o usuário imprimir o documento que estava tentando usar originalmente.

Não consideraria o chamado resolvido apenas porque a impressora voltou a aparecer como online.

## Exemplo de registro do chamado

> Usuário informou que a impressora estava offline. Equipamento e conectividade verificados. Foi identificado travamento na fila de impressão. Após normalização do serviço de impressão, foi enviada página de teste e a impressão foi validada com o usuário.

## O que pratiquei neste caso

- diferenciar problema do computador e problema da impressora;
- verificar a fila antes de reinstalar componentes;
- consultar o Spooler de Impressão;
- testar comunicação com impressora de rede;
- validar a solução junto ao usuário.
