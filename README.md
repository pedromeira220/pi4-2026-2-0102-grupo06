# Sistema de Gestão de Filas

Aplicação web que mostra ao cliente de uma praça de alimentação a etapa, a estimativa de tempo e a posição na fila do seu pedido. O cliente abre a página no celular, digita a senha do comprovante, sem cadastro, e a tela se atualiza sozinha até avisar "Pedido pronto, pode retirar". Nesta versão os pedidos vêm de um simulador de cozinha, que cria e avança a fila sem ninguém operando.

Projeto Integrador IV · PUC-Campinas · Turma 0102 · Grupo 06 · 2026-2

## Integrantes e papéis

| Nome | RA | GitHub | Responde por |
|---|---|---|---|
| João Pedro Júlio | 25003942 | [@Moiitta](https://github.com/Moiitta) | Backend 1 |
| Murilo Ferrez dos Santos | 25005312 | [@yMrlx](https://github.com/yMrlx) | Backend 1 |
| Neilton de Lima Tavarez | 24802407 | [@NYZD777](https://github.com/NYZD777) | Frontend |
| Patrick Eduardo Pereira de Oliveira | 26014655 | [@patrick-eduardo](https://github.com/patrick-eduardo) | Backend 2 |
| Pedro Henrique Meira | 25005199 | [@pedromeira220](https://github.com/pedromeira220) | Banco, Frontend, Backend 2 e este repositório |

## Repositórios

| Repositório | O que tem |
|---|---|
| [pi4-2026-2-0102-grupo06](https://github.com/pedromeira220/pi4-2026-2-0102-grupo06) | Este: `docker-compose.yml`, README e o documento de projeto |
| [pi4-0102-g6-backend-1](https://github.com/pedromeira220/pi4-0102-g6-backend-1) | Backend 1 (Java, Spring Boot): consulta de pedidos, simulador da cozinha, scripts do banco, contratos CT1 a CT4, CT7 e CT8 |
| [pi4-0102-g6-backend-2](https://github.com/pedromeira220/pi4-0102-g6-backend-2) | Backend 2 (Java, Spring Boot): recebe os avisos por Socket e os repassa por WebSocket, contratos CT5 e CT6 |
| [pi4-0102-g6-frontend](https://github.com/pedromeira220/pi4-0102-g6-frontend) | Frontend (React, TypeScript): telas do cliente, página `/demo`, painel da cozinha e os fluxos E1 a E6 |

## Pré-requisitos

Git 2+ e Docker com Compose v2 (testado com Docker 23.0 e Compose 2.17; o Docker Desktop traz os dois). Java, Node e PostgreSQL não precisam ser instalados: tudo roda nos contêineres.

## Como subir

1. Numa pasta vazia, clone os quatro repositórios lado a lado:

   ```bash
   git clone https://github.com/pedromeira220/pi4-2026-2-0102-grupo06.git
   git clone https://github.com/pedromeira220/pi4-0102-g6-backend-1.git
   git clone https://github.com/pedromeira220/pi4-0102-g6-backend-2.git
   git clone https://github.com/pedromeira220/pi4-0102-g6-frontend.git
   ```

2. Entre no repositório principal e crie o arquivo de variáveis a partir do exemplo:

   ```bash
   cd pi4-2026-2-0102-grupo06
   cp .env.example .env
   ```

   No Windows (PowerShell), use `copy .env.example .env`. Os valores do exemplo já funcionam com os clones do passo 1. Só mude se os módulos estiverem em pastas com outro nome ou se quiser outra senha para o banco.

3. Suba o sistema. A primeira vez leva alguns minutos, porque baixa as imagens e compila os módulos:

   ```bash
   docker compose up --build
   ```

   Está pronto quando o log mostrar `Started Backend1Application`.

4. Abra http://localhost:5173 no navegador e digite a senha **42**, o pedido de teste que o banco cria na primeira subida.

| Módulo | Endereço |
|---|---|
| Frontend | http://localhost:5173 |
| Backend 1 (HTTP) | http://localhost:8080/pedidos/42 |
| Backend 2 (WebSocket) | ws://localhost:8082/ws |

Para parar, `Ctrl+C` e depois `docker compose down`. Para zerar o banco junto, `docker compose down -v`.

## Como usar

Não há login. A "senha" é o número do pedido. O simulador cria um pedido a cada 20 a 30 s (senhas 42, 43… na primeira subida; 1, 2… depois de reiniciar), e cada um passa por Recebido, Em preparo e Pronto em cerca de 1 a 2 minutos.

- **E1. Ver o pedido:** abra http://localhost:5173 e digite uma senha. As senhas que existem agora aparecem em http://localhost:5173/prototipo-fluxo. No celular, na mesma rede Wi-Fi, use `http://<ip-desta-máquina>:5173` (IP: `ipconfig getifaddr en0` no macOS, `ipconfig` no Windows, `hostname -I` no Linux).
- **E2. Fila de demonstração:** anda sozinha. Para recomeçar, abra http://localhost:5173/demo e clique em "Reiniciar demo".
- **E3. Atualização sozinha:** deixe a tela de um pedido em Recebido aberta; ela muda de etapa sem recarregar.
- **E4. Quanto falta:** a tela mostra "Cerca de N min", a posição na fila e a barra das etapas. A estimativa está em minutos reais e a demonstração é acelerada (1 min = 10 s).
- **E5. Aviso de pronto:** em Pronto, a tela fica verde com "Pedido pronto, pode retirar".
- **E6. Sistema empacotado:** é o passo a passo de "Como subir".
- **Painel da cozinha:** em `/prototipo-fluxo`, o botão "Horário de pico" faz chegar mais pedidos para a fila crescer.

Se a porta 5173, 8080, 8082 ou 5432 estiver ocupada, feche o programa que a usa e suba de novo.

## Documentação

- [Documento de projeto](docs/documento-de-projeto.md): visão geral, requisitos, arquitetura, banco, contratos, testes e telas
- [Escopo da Entrega 1](docs/escopo.pdf)
