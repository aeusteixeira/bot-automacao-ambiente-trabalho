# Bot de Inicialização do Ambiente de Trabalho

Este documento descreve como configurar um bot que automatiza a inicialização do seu ambiente de trabalho. O bot é configurado através de um script batch que abre alguns sites que tenho o costume de acessar no Google Chrome e uma pasta com os arquivos dos projetos que trabalho ao iniciar o Windows. A configuração é realizada utilizando o Agendador de Tarefas do Windows.

## Descrição
O bot foi criado para facilitar a inicialização do ambiente de trabalho, abrindo automaticamente os sites e pastas necessários ao iniciar o Windows. Isso economiza tempo e garante que todas as ferramentas e recursos necessários estejam prontamente disponíveis.


### Conteúdo do Script Batch (`boot.bat`)

O script batch `boot.bat` contém os comandos necessários para abrir os sites e a pasta especificados.

```batch
@echo off
rem Abrir sites no Chrome
start chrome.exe "https://mentesnotaveis-team.monday.com/"
start chrome.exe "https://mail.google.com/"
start chrome.exe "https://asoftmurmur.com/"
start chrome.exe "https://www.tecmundo.com.br/"

rem Abrir uma pasta específica
start "" "C:\dev"

rem Finalizar o script
exit
```

### Exportação da Tarefa Agendada (`task.xml`)

A configuração da tarefa agendada foi exportada para um arquivo XML. Abaixo está o conteúdo do arquivo `task.xml`:

```xml
<?xml version="1.0" encoding="UTF-16"?>
<Task version="1.2" xmlns="http://schemas.microsoft.com/windows/2004/02/mit/task">
  <RegistrationInfo>
    <Date>2024-06-03T18:26:18.1486032</Date>
    <Author>DESKTOP-K2VTIHC\Matheus Teixeira</Author>
    <Description>Este script abre vários sites no Chrome e uma pasta específica ao iniciar o Windows.</Description>
    <URI>\Abra Sites e Pastas</URI>
  </RegistrationInfo>
  <Triggers>
    <BootTrigger>
      <Enabled>true</Enabled>
    </BootTrigger>
  </Triggers>
  <Principals>
    <Principal id="Author">
      <UserId>ANONYMIZED</UserId>
      <LogonType>InteractiveToken</LogonType>
      <RunLevel>LeastPrivilege</RunLevel>
    </Principal>
  </Principals>
  <Settings>
    <MultipleInstancesPolicy>IgnoreNew</MultipleInstancesPolicy>
    <DisallowStartIfOnBatteries>true</DisallowStartIfOnBatteries>
    <StopIfGoingOnBatteries>true</StopIfGoingOnBatteries>
    <AllowHardTerminate>true</AllowHardTerminate>
    <StartWhenAvailable>false</StartWhenAvailable>
    <RunOnlyIfNetworkAvailable>false</RunOnlyIfNetworkAvailable>
    <IdleSettings>
      <Duration>PT10M</Duration>
      <WaitTimeout>PT1H</WaitTimeout>
      <StopOnIdleEnd>true</StopOnIdleEnd>
      <RestartOnIdle>false</RestartOnIdle>
    </IdleSettings>
    <AllowStartOnDemand>true</AllowStartOnDemand>
    <Enabled>true</Enabled>
    <Hidden>false</Hidden>
    <RunOnlyIfIdle>false</RunOnlyIfIdle>
    <WakeToRun>false</WakeToRun>
    <ExecutionTimeLimit>PT72H</ExecutionTimeLimit>
    <Priority>7</Priority>
  </Settings>
  <Actions Context="Author">
    <Exec>
      <Command>"C:\Users\Matheus Teixeira\OneDrive\Documentos\Automações\inicializar-trabalho\boot.bat"</Command>
    </Exec>
  </Actions>
</Task>
```

### Passos para Importar a Tarefa no Agendador de Tarefas do Windows

1. **Abrir o Agendador de Tarefas:**
   - Pressione `Win + R`, digite `taskschd.msc` e pressione `Enter`.

2. **Importar a Tarefa:**
   - No painel da direita, clique em **Importar Tarefa...**.
   - Navegue até o local onde o arquivo `task.xml` está salvo e selecione-o.
   - Revise as configurações importadas e clique em **OK** para concluir a importação.

3. **Verificar e Testar:**
   - Verifique se a tarefa foi importada corretamente e está ativa.
   - Para testar a tarefa, clique com o botão direito sobre a tarefa e selecione **Executar**.