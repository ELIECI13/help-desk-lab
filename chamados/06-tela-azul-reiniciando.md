# Chamado 06 — Computador reiniciando e apresentando tela azul

**Cenário de laboratório:** o usuário relata que o computador começou a reiniciar sozinho e, em alguns momentos, aparece uma tela azul do Windows.

## Primeiro: entender quando acontece

Eu perguntaria quando o problema começou e o que o usuário estava fazendo antes da primeira ocorrência. Também tentaria descobrir se houve atualização do Windows, instalação de programa, troca de periférico ou alguma alteração recente.

Se a tela azul aparecer novamente, registraria o código de parada exibido. Essa informação pode ajudar bastante na investigação.

## Verificações iniciais

Antes de sair formatando o computador, eu verificaria:

- atualizações recentes;
- drivers instalados ou atualizados;
- dispositivos conectados recentemente;
- espaço disponível no disco;
- sinais de superaquecimento;
- frequência com que o problema acontece.

Também observaria se o computador reinicia apenas ao executar determinada tarefa.

## Visualizador de Eventos

Uma das ferramentas que eu consultaria é o **Visualizador de Eventos do Windows** (`eventvwr.msc`).

Procuraria eventos próximos ao horário da falha, principalmente em **Logs do Windows > Sistema**.

O objetivo não seria tratar qualquer evento vermelho como a causa. Eu compararia horário, origem e descrição com o momento em que o computador apresentou o problema.

## Verificação dos arquivos do sistema

Se houver suspeita de corrupção de arquivos do Windows, posso executar como administrador:

```bat
sfc /scannow
```

Dependendo do resultado, também posso verificar a imagem do Windows:

```bat
DISM /Online /Cleanup-Image /ScanHealth
```

## Disco

Para uma verificação inicial do sistema de arquivos:

```bat
chkdsk C: /scan
```

Se surgirem indícios de problema físico no armazenamento, eu não trataria uma correção do sistema de arquivos como diagnóstico definitivo do hardware. O próximo passo seria verificar a saúde do dispositivo com as ferramentas apropriadas e garantir que dados importantes estejam protegidos.

## Memória RAM

Falhas de memória também podem causar travamentos e telas azuis. Uma ferramenta básica disponível no Windows é o **Diagnóstico de Memória do Windows** (`mdsched.exe`).

Como o teste exige reinicialização, eu avisaria o usuário e faria isso em um momento adequado para não interromper o trabalho sem necessidade.

## Drivers

Se o problema começou logo após uma atualização de driver, eu compararia a data com o início das falhas e verificaria o dispositivo envolvido no Gerenciador de Dispositivos.

Eu evitaria baixar drivers de sites aleatórios. Em um ambiente corporativo, seguiria a fonte e o procedimento definidos pela empresa ou pelo fabricante.

## Antes de pensar em formatar

Formatação seria uma das últimas alternativas. Antes dela eu tentaria chegar a uma causa provável e avaliaria se o problema está no Windows, driver ou hardware.

Além de consumir tempo, formatar sem investigar pode fazer o defeito voltar se a causa for física.

## Exemplo de registro do chamado

> Usuário relatou reinicializações inesperadas e tela azul. Foram levantadas alterações recentes e analisados eventos do Windows próximos aos horários das falhas. Realizadas verificações iniciais de sistema e hardware para identificar a origem do problema. Caso mantida a instabilidade, equipamento deve seguir para diagnóstico de hardware antes de uma reinstalação do sistema.

## O que pratiquei neste caso

- coleta de informações antes de alterar o computador;
- uso básico do Visualizador de Eventos;
- `sfc`, `DISM` e `chkdsk` como ferramentas de diagnóstico;
- noções de investigação de memória, disco e drivers;
- evitar formatação como primeira solução;
- registrar evidências para facilitar um possível escalonamento do chamado.
