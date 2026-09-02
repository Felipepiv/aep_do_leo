# Como a comunicação entre o software do galpão conversa com o hardware do servidor?

Para garantir qeu a comunicação entre o software e o hardware ocorra de forma segura e sem corromper o sistema de arquivos, utiliza-se o Sistema Operacional(Debian). Ele atua com base no conceito de máquina flexível(ou estendida) e intermedeia todas as operações por meio das System Calls.

# S.O como uma máquina flexível:

O S.O cria uma camada por cima do hardware para ocultar sua complexidade, apresentando uma interface mais simples e flexível para o desenvolvedor. Assim, em vez do software do galpão ter que lidar com setores físicos, ele ira lidar com arquivos, pastas, conexões de rede e processos.

# A separação dos modos: como o hardware é protegido

Modo de Usuário: É onde o seu software do galpão (o sistema web, o script de triagem, etc.) roda. Nesse modo, o código tem restrições estritas: não pode executar instruções críticas do processador nem acessar o hardware diretamente.

Modo Kernel: É o modo privilegiado onde apenas o núcleo do Sistema Operacional (o Kernel do Debian) executa. Ele tem acesso total a todos os componentes físicos da máquina.

# O papel das System calls:

São usadas quando o software do galpão precisa realizar qualquer ação no mundo físico para salvar um registro de um médico no disco. O software não consegue fazer isso sozinho por estar no modo usuário.

### como que funciona o uso das System calls:






