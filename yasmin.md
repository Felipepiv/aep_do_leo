# Squad de Interface e System Calls

## 1. Por que o Software não acessa o Hardware Diretamente?

O S.O. é um intermediário obrigatório por 3 motivos:

- Segurança: Evita corrupção de dados
- Simplicidade: Padroniza o acesso ao hardware
- Estabilidade: Isola falhas de programas

A CPU tem níveis de privilégio:
- Ring 0 (Kernel): Acesso total ao hardware
- Ring 3 (Usuário): Acesso restrito (onde as threads rodam)

---

## 2. O que são System Calls?

São a ponte segura entre o programa e o kernel.

Processo:
1. Thread chama write()
2. CPU executa trap -> muda para modo kernel
3. Kernel executa a operação
4. Kernel retorna o resultado à thread

---

## 3. Observando com strace

No terminal execute:

strace ls

Chamadas comuns:

- open: Abrir arquivo
- read: Ler arquivo
- write: Escrever dados
- close: Fechar arquivo

---

## 4. Por que as Threads usam System Calls para gravar no Disco?

- Proteção: Kernel verifica permissões
- Abstração: Não precisa conhecer o hardware
- Isolamento: Falha em uma thread não afeta o sistema

---

## Resumo

As threads usam System Calls (ex: write) para gravar no disco porque o kernel (Ring 0) é o único que pode acessar o hardware diretamente, garantindo segurança e estabilidade.