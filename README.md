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

## Documentos

- [Escopo do projeto](docs/escopo.pdf)
