# O que é um System Calls?
System calls são formas de comunicação entre os programas e o sistema operacional. Elas permitem que um programa, que normalmente funciona no modo usuário, possa solicitar ao sistema operacional algumas tarefas que precisam de permissões especiais. 

Por exemplo, quando um programa precisa abrir um arquivo, ele pode utilizar a função open(). Se for necessário criar um novo processo, pode ser utilizada a função fork(). Já para estabelecer uma conexão de rede, existe a função connect(). Essas funções fazem uma solicitação ao kernel, que é a parte principal do sistema operacional responsável por controlar os recursos do computador. De uma forma mais simples, podemos imaginar as system calls como uma ponte entre os programas e o sistema operacional. Por meio delas, os programas conseguem acessar recursos como arquivos, memória, processos, rede e informações do sistema de maneira controlada e segura. Sem as system calls, os programas teriam muitas limitações e não conseguiriam realizar várias tarefas importantes que usamos no dia a dia. Por isso, elas são fundamentais para o funcionamento dos sistemas operacionais e para que os softwares consigam interagir com o hardware do computador.


# Espaço de Usuário vs Espaço de Kernel
Os sistemas operacionais modernos dividem a execução dos programas em dois modos: User Mode, onde funcionam os aplicativos comuns, e Kernel Mode, onde o sistema operacional possui acesso completo aos recursos do computador. Quando um programa precisa realizar uma tarefa que exige mais permissões, ele utiliza uma system call. Nesse momento, a CPU muda do User Mode para o Kernel Mode, executa a operação solicitada e depois retorna ao modo de usuário. Durante essa troca, o sistema salva o estado atual do processo, utiliza a pilha de kernel para executar a operação e, ao final, restaura o contexto anterior. A pilha de kernel é uma área de memória protegida utilizada durante system calls e interrupções. Ela possui tamanho limitado e é específica para cada processo ou thread. Como seu espaço é pequeno, um estouro da pilha pode causar problemas graves no funcionamento do sistema.

# Caminho de uma System Call: Passo a Passo
Invocação do usuário, Entrada no kernel, Troca de contexto, Despacho da syscall, Execução do serviço, Retorno ao usuário


# Segurança e isolamento
As system calls também são muito importantes para manter a segurança do sistema operacional. Elas funcionam como uma espécie de controle, impedindo que qualquer programa tenha acesso direto a recursos importantes do computador. Sem esse controle, um programa poderia fazer coisas perigosas, como alterar configurações da rede, modificar arquivos que não deveria, acessar informações de outros processos ou até interferir diretamente no hardware. Por isso, a troca entre o User Mode e o Kernel Mode pode exigir um pouco mais de tempo e processamento, mas ela é necessária para manter o sistema seguro e organizado. Dessa forma, o sistema consegue verificar as informações recebidas, controlar quem pode acessar determinados recursos, proteger a memória e registrar as ações realizadas.

