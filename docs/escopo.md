---
title: "Escopo do Projeto — Sistema de Gestão de Filas"
subtitle: "Projeto Integrador IV · Turma 0102 · Grupo 06 · 2026-2"
lang: pt-BR
---

# Parte 1. O problema

Hoje, o cliente que faz um pedido no balcão de uma praça de alimentação precisa saber quanto falta para o pedido ficar pronto, mas as ferramentas do local (pager, painel de senha, chamada por voz) só avisam no momento "pronto" e não mostram o andamento, o que faz o cliente esperar em pé perto do balcão durante toda a refeição e interromper o atendente a cada poucos minutos para perguntar do pedido.

**Evidência.** _[Inserir o print do preço do pager, página de produto de loja mostrando o valor.]_

O que a evidência mostra: _[Uma frase. Ex.: "É o que o restaurante paga hoje só para chamar o cliente, R\$ XX por unidade mais a reposição por perda, e mesmo assim o pager avisa só o 'pronto', não o andamento."]_

Observação do grupo: em uma refeição de um dos integrantes, a mesa esperou 20 minutos e chamou o garçom para reclamar. Ele consultou a maquininha e o pedido tinha sido lançado havia 20 minutos, contra um preparo médio de 22. Estava no prazo. O dado do andamento existia, estava na maquininha do garçom, mas não chegava ao cliente.

# Parte 2. Objetivo geral, objetivos específicos e critério de sucesso

**Objetivo geral.** Construir uma aplicação web de acompanhamento de pedidos para praças de alimentação e restaurantes, acessada por QR code e sem cadastro, que mostre ao cliente a etapa atual e a estimativa de tempo do seu pedido e se atualize sozinha.

**Objetivos específicos.**

- **OE1.** Representar o ciclo de vida do pedido (Recebido → Em preparo → Pronto) e alimentá-lo automaticamente para a demonstração.
- **OE2.** Dar ao cliente uma página, sem instalar aplicativo e sem cadastro, que mostra a etapa e a estimativa de tempo do seu pedido.
- **OE3.** Manter a página do cliente atualizada e sinalizar quando o pedido fica pronto.
- **OE4.** Empacotar o sistema para subir com um comando em qualquer máquina.

**Critério de sucesso.** Em dezembro, o grupo abre a página do cliente pelo QR code e digita a senha de um pedido. A página acompanha o pedido avançar pelas três etapas, com cada mudança aparecendo sozinha na tela em até 10 segundos, e mostra o aviso "Pedido pronto" ao fim. Nada disso exige instalar aplicativo ou criar conta.

# Parte 3. O escopo: os entregáveis

O produto é um só: o app do cliente. O painel do atendente está fora do escopo (Parte 4), então a lista abaixo decompõe esse app.

Cada linha vai do dado à tela e funciona sozinha, sem depender de um item futuro para ser demonstrada. A coluna "Depende de" diz o que precisa estar pronto antes. Os tamanhos seguem a régua do plano de ensino: P = 8 h, M = 20 h, G = 40 h, contando o trabalho do grupo somado.

| ID | Entregável | Feito quando | Depende de | Obj. | Tam. |
|----|------------|--------------|------------|------|------|
| E1 | Chegada ao pedido pela senha | O cliente aponta a câmera do celular para o QR impresso, o navegador abre a tela de senha, ele digita "42" e vê o número da senha e a etapa atual escrita por extenso. Senha que não existe mostra "Pedido não encontrado, confira o número na sua senha". | — | OE2 | P |
| E2 | Fila de demonstração | Com o sistema no ar e ninguém mexendo, a cada 30 s entra um pedido novo com senha própria e os existentes avançam de etapa sozinhos até "Encerrado". O botão "reiniciar demo" esvazia a fila. | E1 | OE1 | P |
| E3 | A tela se atualiza sozinha | Com a tela aberta na senha "42" e o cliente sem tocar em nada, a etapa muda na tela em até 10 s depois que a fila avança aquele pedido. | E1, E2 | OE3 | P |
| E4 | Quanto falta na tela | Além da etapa, a tela mostra "cerca de 8 min" e uma barra com Recebido, Em preparo e Pronto, com a atual destacada e as anteriores marcadas como cumpridas. Em "Pronto", mostra "pode retirar" no lugar do número. | E1 | OE2 | P |
| E5 | Aviso de pronto | Quando a fila leva o pedido a "Pronto", a tela aberta muda de cor e mostra "Pedido pronto, pode retirar". O aviso fica visível até o pedido ser encerrado. | E3 | OE3 | P |
| E6 | Sistema empacotado | Num clone limpo do repositório, `docker compose up` sobe o sistema. O README diz a URL, onde está o QR de teste e qual senha usar. Quem nunca viu o projeto chega à tela de acompanhamento em menos de 5 minutos. | E1 | OE4 | P |

E1 junta QR, dado, API e tela, e é o único item que não depende de nenhum outro. Os cinco restantes penduram nele.

**6 entregáveis, todos P: 6 × 8 h = 48 horas.**

# Parte 4. Fora de escopo

O painel de operação do restaurante, em que o funcionário cria o pedido e avança a etapa à mão, custaria cerca de **44 h**: cadastro de pedido com validação (12 h), lista de pedidos ativos (8 h), ação de avançar etapa (8 h), identificação do restaurante (8 h), campo de estimativa (4 h) e layout para tablet (4 h). Isso é quase tanto quanto o escopo inteiro que ficou de pé (48 h) e consome quase três quartos das 60 horas-pessoa que o grupo tem no semestre. Na demonstração, a fila é gerada automaticamente (E2).

Login e fica de fora: o sistema sem autenticação. O login adiciona uma barreira ao cliente, que muitas vezes só que acompanhar o pedido, sem criar conta.

A integração com PDV e a emissão de nota fiscal dependem de contrato com fabricante de PDV e de certificado digital, que não temos. Não daria nem para validar se funciona.

# Parte 5. A conta da viabilidade

**Passo 1. Quantas semanas.** Da data desta entrega (15/09/2026) até a entrega final do projeto, em dezembro, descontando os recessos de 12/10, 15 a 17/10, 02/11, 20 e 21/11 e 08/12, restam **12 semanas**.

**Passo 2. Quantas horas por semana cada integrante consegue.** Todos os cinco cursam outras disciplinas no mesmo semestre e trabalham no período da tarde/noite. O grupo só começa a construir mais para frente, depois de fechar o escopo na diciplina de Ideação; a hora por semana abaixo é a média do período inteiro e já absorve essas duas primeiras semanas.

| Integrante | Horas por semana |
|------------|:----------------:|
| João Pedro Júlio | 1 |
| Murilo Ferrez dos Santos | 1 |
| Neilton de Lima Tavarez | 1 |
| Patrick Eduardo Pereira de Oliveira | 1 |
| Pedro Henrique Meira | 1 |
| **Total do grupo, por semana** | **5** |

**Passo 3. Horas-pessoa disponíveis.** 5 horas por semana × 12 semanas = **60 horas-pessoa**.

**Passo 4. Quanto o escopo custa.**

| Tamanho | Quantos itens | Horas |
|---------|:-------------:|:-----:|
| P (8 h) | 6 | 48 |
| **Total** | **6 itens** | **48 horas** |

**Passo 5. O fecho.** Temos 60 horas-pessoa e o escopo pede 48. **Cabe, com folga de 12 horas** para documento, reunião, teste e o que der errado.

# Parte 6. Onde está tudo

```
Repositório:          https://github.com/pedromeira220/pi4-2026-2-0102-grupo06
Card no OpenProject:  https://srv1889234.hstgr.cloud/projects/pi-iv-0102-g6/work_packages/167

Integrantes:
  João Pedro Júlio                       @Moiitta
  Murilo Ferrez dos Santos               @yMrlx
  Neilton de Lima Tavarez                @NYZD777
  Patrick Eduardo Pereira de Oliveira    @patrick-eduardo
  Pedro Henrique Meira                   @pedromeira220
```
