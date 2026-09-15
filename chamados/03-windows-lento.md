# Chamado 03 — Computador com Windows muito lento

**Cenário de laboratório:** o usuário relata que o computador demora para iniciar, abrir programas e alternar entre tarefas.

## Entendendo o problema

Antes de fazer limpeza ou instalar qualquer ferramenta, eu perguntaria quando a lentidão começou e em quais situações ela aparece.

Tentaria descobrir se o computador fica lento o tempo todo ou somente ao abrir algum programa específico. Também perguntaria se houve instalação ou atualização recente.

## Primeira verificação

Abriria o Gerenciador de Tarefas (`Ctrl + Shift + Esc`) e observaria principalmente:

- uso de CPU;
- memória RAM;
- disco;
- programas consumindo muitos recursos;
- quantidade de programas iniciando junto com o Windows.

Se o disco estivesse em 100%, por exemplo, eu não concluiria imediatamente que ele está com defeito. Primeiro tentaria descobrir qual processo está causando o uso.

## Espaço em disco

Também verificaria quanto espaço livre existe na unidade do sistema.

No PowerShell posso consultar os discos com:

```powershell
Get-Volume
```

Arquivos temporários e pouco espaço disponível podem contribuir para problemas de desempenho, mas eu evitaria apagar pastas manualmente sem saber o que existe nelas.

## Programas na inicialização

No Gerenciador de Tarefas, verificaria a aba de aplicativos de inicialização.

Programas que não precisam abrir junto com o Windows podem ser desabilitados, desde que eu saiba qual é a função deles. Eu evitaria desativar antivírus, drivers ou programas corporativos somente para tentar deixar a máquina mais rápida.

## Verificação do Windows

Se houver indício de arquivos do sistema corrompidos, uma ferramenta que posso usar em Prompt de Comando aberto como administrador é:

```bat
sfc /scannow
```

O resultado do comando precisa ser conferido antes de decidir o próximo passo.

Para verificar a imagem do Windows, quando necessário:

```bat
DISM /Online /Cleanup-Image /ScanHealth
```

Esses comandos não seriam minha primeira ação em todo computador lento. Eu usaria quando o diagnóstico apontasse nessa direção.

## Hardware

Se o computador continuar lento, eu levantaria informações como:

- quantidade de memória RAM;
- tipo de armazenamento (HD ou SSD);
- temperatura e ventilação do equipamento;
- possíveis erros de disco;
- idade e configuração da máquina.

Um computador antigo usando HD pode apresentar uma experiência bem diferente de uma máquina com SSD, mesmo que não exista uma falha no Windows.

## Malware e segurança

Se o comportamento for anormal, também verificaria a solução de segurança utilizada pela empresa e faria a análise conforme o procedimento definido no ambiente.

Não instalaria um antivírus aleatório em uma máquina corporativa sem autorização.

## Validação

Depois das alterações, reiniciaria a máquina quando necessário e compararia o comportamento com o início do atendimento: tempo para iniciar, abrir os programas usados pelo usuário e executar as tarefas que estavam lentas.

## Exemplo de registro do chamado

> Usuário relatou lentidão geral no computador. Durante o diagnóstico foi identificado alto consumo de recursos por aplicativos iniciados automaticamente. Aplicativos não essenciais foram retirados da inicialização e o equipamento foi reiniciado. Desempenho validado novamente com o usuário.

## O que pratiquei neste caso

- investigar antes de fazer uma “limpeza” genérica;
- analisar CPU, memória e disco;
- revisar aplicativos de inicialização;
- conhecer ferramentas nativas de diagnóstico do Windows;
- considerar limitações de hardware;
- validar se a alteração realmente resolveu a reclamação do usuário.
