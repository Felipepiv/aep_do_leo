As Threads (linhas de execução) do galpão rodam no *user space* (Ring 3), 
um ambiente restrito e limitado, sem permissões para gravar diretamente no disco.

As permissões de hardware ficam sob a responsabilidade do kernel (núcleo do 
sistema operacional), que atua no *kernel space* (Ring 0).

Para que um se comunique com o outro, é necessário o uso das *System Calls*. 
É uma instrução especial que provoca a troca do processador do modo usuário 
(Ring 3) para o modo kernel (Ring 0). Nessa transição, o kernel assume o 
controle e realiza a operação em nome da Thread: abre ou cria o arquivo 
(`open`), grava os dados (`write`) e, ao final, fecha o arquivo (`close`). 
O `read` também pode ser usado, caso a Thread precise consultar dados já 
existentes antes de escrever.

As Threads em si não conseguem acessar diretamente o disco, por questões 
de segurança e integridade dos dados, considerando que duas gravações 
simultâneas poderiam corromper o sistema de arquivos.


## Análise das System Calls Observadas

<div align="center">
    <img src="imagens/strace.png" alt="print do terminal debian com strace ls" width="650">
</div>

Ao executar `strace ls`, é possível observar dezenas de chamadas de sistema
acontecendo em sequência, mesmo para um comando aparentemente simples. Isso
evidencia que o programa `ls`, rodando em *user space*, depende constantemente
do kernel para realizar qualquer operação que envolva hardware ou arquivos.

<div align="center">
    <img src="imagens/strace-filtro.png" alt="print do terminal debian com strace ls, focado nas system calls (open, openat, read e close)" width="650">
</div>

<div align="center">
    <img src="imagens/write.png" alt="print do terminal debian com strace ls, para demonstrar write" width="650">
</div>

* Open / openat — Abertura de arquivos <br>
O `openat` é a versão moderna do `open`, usada pelo Linux para evitar
condições de corrida ao resolver caminhos relativos. 
* Read — Leitura de dados <br>
Após abrir cada biblioteca, o processo faz a leitura do seu conteúdo binário
através do descritor retornado pelo `open`/`openat`.
* Write — Escrita de dados <br>
É a chamada que entrega o resultado do comando ao usuário, escrevendo os
dados no descritor de saída padrão (stdout).
* Close — Fechamento de descritores <br>
Ao final do uso de cada arquivo, o processo fecha o descritor correspondente,
liberando o recurso.
