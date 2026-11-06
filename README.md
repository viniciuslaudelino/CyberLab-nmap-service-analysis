# CyberLab Enterprise — Projeto 01

## Reconhecimento e Análise de Serviços com Nmap

### 1. Objetivo

Realizar o reconhecimento de serviços de rede em um servidor Linux de laboratório, identificar possíveis riscos de segurança e propor medidas de mitigação.

### 2. Ambiente utilizado

- **Sistema de análise:** Kali Linux
- **Sistema analisado:** Metasploitable 2
- **Ferramenta:** Nmap
- **Rede:** VMnet2 — laboratório isolado
- **IP do alvo:** 10.10.40.20
- **Datas das coletas:** 23/10/2026 e 06/11/2026

### 3. Metodologia

Foram realizadas duas varreduras direcionadas às portas TCP 22, 23, 80 e 3306, utilizando o Nmap com detecção de versões de serviços (`-sV`).

**Coleta inicial — 23/10/2026:**

```bash
nmap -sV -p 22,23,80,3306 -oN ~/CyberLab/evidencias/scan-recuperacao-23-10.txt 10.10.40.20
```

**Validação após reinstalação — 06/11/2026:**

```bash
nmap -sV -p 22,23,80,3306 -oN ~/CyberLab/portfolio/projeto-01/evidencias/scan-06-11-2026.txt 10.10.40.20
```

O parâmetro `-oN` salva a saída em formato de texto. As duas coletas foram preservadas na pasta `evidencias/` do projeto. Os resultados foram comparados para verificar a disponibilidade dos quatro serviços após a reinstalação

### 4. Resultados encontrados

| Porta | Serviço | Versão identificada |
|---|---|---|
| 22/TCP | SSH | OpenSSH 4.7p1 |
| 23/TCP | Telnet | Linux telnetd |
| 80/TCP | HTTP | Apache 2.2.8 |
| 3306/TCP | MySQL | 5.0.51a |

As quatro portas examinadas estavam abertas.

### 5. Análise inicial de riscos

**Telnet — Prioridade alta**

O serviço Telnet utiliza comunicação sem criptografia, podendo expor credenciais e informações transmitidas pela rede.

**SSH — Requer avaliação**

A versão identificada é antiga. Recomenda-se verificar atualizações de segurança, configurações criptográficas e controles de acesso.

**Apache HTTP — Requer avaliação**

O servidor utiliza uma versão antiga. Recomenda-se avaliar vulnerabilidades conhecidas, configurações e exposição de recursos administrativos.

**MySQL — Requer avaliação**

O serviço de banco de dados está acessível pela rede e utiliza uma versão antiga. Recomenda-se restringir o acesso a sistemas autorizados e avaliar a atualização.

### 6. Recomendações

1. Desabilitar Telnet e utilizar SSH com configurações seguras.
2. Atualizar softwares que não recebem mais correções de segurança.
3. Restringir portas acessíveis por regras de firewall.
4. Aplicar o princípio do menor privilégio.
5. Monitorar eventos de autenticação e acessos aos serviços.

### 7. Evidências técnicas

Foram realizadas duas coletas de evidências com Nmap:

**Coleta inicial — 23/10/2026**
- Arquivo: `evidencias/scan-recuperacao-23-10.txt`
- Objetivo: identificar serviços ativos no ambiente original.

**Coleta de validação — 06/11/2026**
- Arquivo: `evidencias/scan-06-11-2026.txt`
- Objetivo: verificar a disponibilidade dos serviços após a reinstalação do Metasploitable 2.

As duas varreduras identificaram as portas TCP
22, 23, 80 e 3306 abertas.

Os arquivos preservam os resultados originais
das coletas realizadas no laboratório.

### 8. Limitações da análise

A varredura examinou apenas quatro portas TCP. Portanto, não representa um inventário completo dos serviços disponíveis.

A identificação de uma versão antiga não comprova, isoladamente, a existência de uma vulnerabilidade explorável.

Não foram realizados testes de exploração neste projeto.

### 9. Competências demonstradas

- Uso do Nmap para identificação de serviços.
- Interpretação de portas TCP abertas.
- Reconhecimento de riscos associados a protocolos.
- Priorização inicial de recomendações.
- Documentação de evidências técnicas.

**Projeto desenvolvido em ambiente próprio e autorizado para fins educacionais.**
