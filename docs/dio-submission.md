# Entrega à DIO — Desafio Medusa + Kali Linux

## Repositório público

**Nome:** Authentication Security Lab | Kali Linux + Medusa  
**URL:** https://github.com/MariMecucci/dio-kali-medusa-security-lab

## Descrição curta para o campo “Entregar Projeto”

> Laboratório educacional de segurança de autenticação realizado com Kali Linux, Metasploitable 2 e Medusa, em uma rede interna isolada no VirtualBox. Configurei os endereços IP privados, validei a comunicação entre as VMs, identifiquei serviços com Nmap e executei um teste controlado de autenticação SSH com duas senhas de laboratório. O Medusa identificou a credencial padrão intencionalmente vulnerável. Documentei os resultados observados, as limitações e as recomendações de mitigação no README e na pasta de evidências. Este projeto não envolveu sistemas reais nem alvos externos.

## Arquivos disponíveis para avaliação

- [README principal](../README.md): objetivo, topologia, ferramentas, resultados e análise defensiva
- [Relatório técnico](2026-11-08-verified-lab-evidence.md): método, resultados e escopo
- [Transcrição selecionada das evidências](../evidence/verified-terminal-excerpts.md): registros observados de `ping`, `nmap` e `medusa`
- [Este guia](dio-submission.md): resumo da entrega e declaração do escopo

## Checklist de submissão

- [x] Repositório **público**, com README
- [x] Laboratório virtual instalado e executado
- [x] Conexão Kali–Metasploitable validada
- [x] Reconhecimento do alvo isolado realizado
- [x] Teste de autenticação SSH com Medusa executado
- [x] Resultado e medidas defensivas documentados
- [x] Evidências textuais transcritas e identificadas como transcrição, sem fingir que são logs originais
- [ ] **Usuária:** enviar o link no botão **Entregar Projeto** da DIO

**Capturas de tela:** opcionais de acordo com o enunciado exibido no curso. Os arquivos de imagem da sessão não estão hospedados neste repositório. As evidências textuais são suficientes para apresentar os comandos, as observações e o resultado de forma auditável, mas a plataforma ou avaliador pode solicitar evidência adicional.

## Limitação de escopo

A execução comprovada é uma **adaptação controlada com SSH**. O enunciado também apresenta FTP, DVWA e SMB como possibilidades; não há alegação de execução desses outros cenários. A aceitação do projeto depende das condições da DIO.

**Este projeto foi desenvolvido para fins educacionais e exclusivamente em ambiente autorizado e isolado.**
