# DS Meta

Aplicação **full stack** desenvolvida no bootcamp **DevSuperior** (prof. Nélio Alves).  
O projeto consiste em um **backend Spring Boot** e um **frontend React (Vite + TypeScript)** para consultar um relatório de **vendas** por período e enviar **notificações via SMS** (Twilio).

> Observação: este repositório foi originalmente publicado no **Heroku (plano gratuito)**. Como o plano gratuito foi descontinuado, a aplicação não está mais online. O código continua pronto para rodar localmente e pode ser implantado em qualquer plataforma que suporte Java/Node (Heroku, Render, Railway, etc.).

---

## 🧩 Tecnologias

**Backend**
- Java 17
- Spring Boot
- Spring Data JPA
- Banco **H2 em memória** (dados iniciais em `import.sql`)
- Integração com **Twilio** (SMS)

**Frontend**
- React 18
- Vite
- TypeScript
- Axios
- React Datepicker
- React Toastify

---

## 📂 Estrutura

- `backend/` → API REST + serviço de SMS
- `frontend/` → interface web (lista de vendas + filtro por datas)

---

## ✅ Pré-requisitos

- **Java 17**
- **Node.js** (recomendado 16+ ou 18+)
- (opcional) **Yarn** ou **NPM**
- (opcional) Conta Twilio para SMS

---

## ▶️ Como rodar localmente

### 1) Backend (Spring Boot)

```bash
cd backend
./mvnw spring-boot:run
```

A API sobe por padrão em: `http://localhost:8080`

Extras:
- Console do H2: `http://localhost:8080/h2-console`
  - JDBC URL: `jdbc:h2:mem:testdb`
  - user: `sa`
  - senha: *(vazia)*

### 2) Frontend (React + Vite)

Em outro terminal:

```bash
cd frontend
npm install
npm run dev
```

A aplicação abre (geralmente) em: `http://localhost:5173`

O frontend usa a variável `VITE_BACKEND_URL` (com fallback para `http://localhost:8080`).

---

## 🔌 Variáveis de ambiente (SMS / Twilio)

O endpoint de notificação chama o Twilio. Para habilitar o envio de SMS, defina as variáveis abaixo no ambiente do **backend**:

- `TWILIO_SID`
- `TWILIO_KEY`
- `TWILIO_PHONE_FROM`
- `TWILIO_PHONE_TO`

Sem essas variáveis, o endpoint de notificação pode falhar (dependendo do comportamento do Twilio / credenciais).

---

## 📡 Endpoints principais

- `GET /sales?minDate=YYYY-MM-DD&maxDate=YYYY-MM-DD`  
  Retorna vendas paginadas e filtradas por período.

- `GET /sales/{id}/notification`  
  Envia SMS para a venda informada (Twilio).

Exemplo:

```bash
curl "http://localhost:8080/sales?minDate=2022-01-01&maxDate=2022-12-31"
```

---

## 🚀 Deploy (resumo)

O projeto já contém `system.properties` no backend (útil em PaaS como Heroku para fixar a versão do Java).

Uma estratégia comum:
1. Publicar o **backend** (Java) em um PaaS (Heroku/Render/Railway).
2. Publicar o **frontend** como site estático (Vercel/Netlify) ou no mesmo PaaS.
3. No frontend, configurar `VITE_BACKEND_URL` apontando para a URL pública do backend.
4. No backend, configurar as variáveis do Twilio como *Config Vars* (se for usar SMS).

---

## 👤 Autor

Afonso Benintendi da Silveira  
Bootcamp DevSuperior – DS Meta
