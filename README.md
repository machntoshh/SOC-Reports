Relátorio sobre cenário sinalizado pela Hackers Hive
Cenário

Durante o monitoramento de eventos em um SOC, foi identificado que um endpoint executou o seguinte comando PowerShell fora do horário comercial:

powershell.exe -nop -w hidden -EncodedCommand

Mais detalhes sobre o cenário

    Execução fora de horário de trabalho
    Usuário não possui privilégio administrativo
    Comando powershell codificado e oculto

Perguntas a serem respondidas diante disso
1. Esse comportamento pode indicar algo suspeito?

R: Indica algo suspeito pois como o usuário não possui privilégios e o comando do mesmo foi executado fora do horário de trabalho, isso pode ter sido uma invasão, Nesse caso o atacante já passou da fase de "Reconnaisance" de acordo com a MITRE ATT&CK e está na fase de "Execution".

    O comando -nop ou -NoProfile, implica que a execução de scripts será mais rápida, tirando os perfis do PowerShell.
    O comando -hidden é utilizado para executar o PowerShell de forma oculta ou sem exibir nenhuma interface visual.
    O comando -EncodedCommand permite passar um comando em formato Base64, que será decodificado e executado pelo PowerShell. O comando codificado geralmente está logo após esse parâmetro e é usado para ofuscar o que será executado, dificultando a análise manual e a detecção por antivírus.

Em resumo se não foi um comando reconhecido, ele é então feito para atividades máliciosas.
2. Nome da técnica MITRE ATT&CK relacionada ao uso de PowerShell

para execução de comandos maliciosos?

R: Esse comando implica o uso de uma tecnica em "Execution" chamada de "Command and Scripting Interpreter".
3. Qual consequência desse comando?

R: Baixar e executar um malware
4. Isso é um caso SOC?

R: Sim, porém necessário saber que nível de privilégio o análista tem na empresa, como é algo que está em estado já avançado no framework MITRE ATT&CK será necessário fazer escalação.
Mapeamento MITRE ATT&CK

    Tática (Tactic) e a Técnica (Technique) relacionadas ao uso do PowerShell: "Execution" e "Command and Scripting Interpreter: PowerShell"

    ID da Técnica: T1059.001

    Plataforma: Windows

    Ferramentas ofensivas para essa técnica: Empire, PowerSploit, PoshC2

Expansão da Investigação

Baseando-se apenas no evento detectado, os próximos passos seriam:

    Coletar outros eventos correlacionados (ex.: outros logs de PowerShell, alertas de EDR).
    Analisar as conexões de rede do host para identificar comunicações suspeitas.
    Fazer dump de memória (para detectar payloads injetados ou persistentes na memória).
