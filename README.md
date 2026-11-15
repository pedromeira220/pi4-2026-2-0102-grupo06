# Sistema de Gestão de Filas

Aplicação web que mostra ao cliente de uma praça de alimentação a etapa e a estimativa de tempo do seu pedido, acessada por QR code e sem cadastro.

Projeto Integrador IV - Turma 0102 - Grupo 06.

## Integrantes

- João Pedro Júlio — [@Moiitta](https://github.com/Moiitta)
- Murilo Ferrez dos Santos — [@yMrlx](https://github.com/yMrlx)
- Neilton de Lima Tavarez — [@NYZD777](https://github.com/NYZD777)
- Patrick Eduardo Pereira de Oliveira — [@patrick-eduardo](https://github.com/patrick-eduardo)
- Pedro Henrique Meira — [@pedromeira220](https://github.com/pedromeira220)

## Como rodar

Precisa de Git e Docker. Clone os quatro repositórios lado a lado, na mesma pasta:

```bash
git clone https://github.com/pedromeira220/pi4-2026-2-0102-grupo06.git
git clone https://github.com/pedromeira220/pi4-0102-g6-backend-1.git
git clone https://github.com/pedromeira220/pi4-0102-g6-backend-2.git
git clone https://github.com/pedromeira220/pi4-0102-g6-frontend.git
```

Suba o sistema:

```bash
cd pi4-2026-2-0102-grupo06
docker compose up --build
```

| Módulo | Endereço |
|---|---|
| Frontend | http://localhost:5173 |
| Backend 1 (HTTP) | http://localhost:8080/pedidos/{senha} |
| Backend 2 (WebSocket) | ws://localhost:8082/ws |

Para parar, `docker compose down`. Para zerar o banco junto, `docker compose down -v`.

Se os módulos estiverem em pastas com outro nome, crie um `.env` nesta pasta com `BACKEND1_DIR`, `BACKEND2_DIR` e `FRONTEND_DIR` apontando para elas.

## Como funciona a demonstração

A fila anda sozinha assim que o sistema sobe. Ninguém precisa criar pedido nem clicar em nada.

**A cada 30 segundos**, o simulador do Backend 1 faz duas coisas:

1. avança cada pedido existente uma etapa: recebido → em preparo → pronto → encerrado;
2. cria um pedido novo em recebido, com a senha seguinte (1, 2, 3…).

Cada pedido passa uns 30 segundos em cada etapa e leva cerca de 90 segundos do início ao fim.

**Para acompanhar um pedido**, abra http://localhost:5173 e digite a senha. Num celular na mesma rede, use `http://<ip-desta-máquina>:5173`. Para descobrir o IP:

| Sistema | Comando | O IP é |
|---|---|---|
| macOS | `ipconfig getifaddr en0` | a linha que o comando imprime |
| Windows | `ipconfig` | o "Endereço IPv4" do adaptador Wi-Fi |
| Linux | `hostname -I` | o primeiro endereço da lista |

A tela se atualiza sozinha, sem recarregar:

- a etapa muda em até 10 segundos depois que o simulador avança o pedido;
- a estimativa e a posição na fila mudam a cada ciclo;
- em pronto, a tela fica verde e mostra "Pedido pronto, pode retirar".

Uma senha que ainda não existe mostra "Pedido não encontrado".

**A posição na fila** conta os pedidos em recebido ou em preparo que chegaram antes. No ritmo da demonstração, há no máximo dois pedidos na fila ao mesmo tempo.

**A estimativa** está em minutos de uma cozinha de verdade. Ela vem dos itens de cada pedido e do que falta preparar de quem está à frente, com três postos de preparo. Como a demonstração comprime o tempo, o pedido fica pronto bem antes do que a estimativa diz. A estimativa é recalculada a cada ciclo e não é um cronômetro.

**Para recomeçar do zero**, abra http://localhost:5173/demo e clique em "Reiniciar demo". Todos os pedidos são apagados, e o próximo ciclo cria a senha 1.

## Documentos

- [Escopo do projeto](docs/escopo.pdf)
