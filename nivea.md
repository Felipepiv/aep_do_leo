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