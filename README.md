# Barbearia Washington — Sistema de Gestão e Agendamento

Sistema completo para a Barbearia Washington: painel do administrador, área do colaborador (barbeiro), agendamento online para clientes e notificações automáticas por WhatsApp. Identidade visual dourada metálica com profundidade 3D.

**Site publicado:** https://shave-savvy-crm.lovable.app

---

## Acessos

| Página | Endereço | Quem usa |
|---|---|---|
| Login do administrador | `/` ou `/admin/login` | Dono / gerência |
| Painel financeiro | `/admin` | Administrador |
| Login do colaborador | `/colaborador/login` | Barbeiros |
| Agendamento online | `/agendar` | Clientes (público) |
| Área do cliente | `/cliente` | Clientes cadastrados |

O link de agendamento pode ser compartilhado pela aba **Clientes**, tanto no painel do administrador quanto no do colaborador.

---

## Módulos

### Administrador
- **Financeiro** — receitas, despesas e comissões, com botão para ocultar/mostrar valores.
- **Agenda** — todos os agendamentos, criação manual e detalhes de cada atendimento.
- **Relatórios** — serviços, produtos, bebidas vendidas (separadas de cosméticos), ranking de barbeiros. Botão de ocultar valores.
- **Estoque** — produtos, vendas e consumo interno.
- **Cupons** — códigos de desconto aplicados no agendamento online.
- **Equipes** — quadro de tarefas da equipe com lembretes.
- **Gerenciamento** — barbeiros, serviços, unidades, clientes (com ficha individual: visitas, gasto total, intervalo médio, fidelidade) e **reset de dados** protegido por senha do administrador (registros, valores, estoque, clientes, barbeiros, serviços).
- **Central de mensagens / WhatsApp** — base de clientes, fila de envio e configuração da integração.
- **Notificações em tempo real** com som a cada novo agendamento.

### Colaborador (barbeiro)
- Agenda própria, bloqueio de horários, clientes, relatórios e comissões.
- Notificação de novo agendamento no app e no WhatsApp.

### Cliente
- Agendamento em etapas: unidade → serviço → barbeiro → data/horário → confirmação.
- Cupom de desconto com valor original, desconto e total final.
- Cadastro com senha para entrar e agendar novamente.
- Remarcação, contagem regressiva do próximo horário e avaliação do atendimento.

### Aplicativo instalável (PWA)
- Pode ser instalado no celular com o nome e ícone da Barbearia Washington.
- Atualiza sozinho quando há nova versão publicada.

---

## Regras importantes
- Valores são exibidos exatamente como registrados, com 2 casas decimais, sem arredondamento.
- A primeira tela do sistema é sempre o login do administrador.
- A página de agendamento é pública; as páginas internas exigem login com o perfil correto.

---

## Tecnologia

- **Frontend:** React 18, TypeScript, Vite, Tailwind CSS, shadcn/ui, Framer Motion, TanStack Query.
- **Backend:** Lovable Cloud — autenticação, banco de dados com regras de acesso por perfil, funções de servidor e tempo real.
- **Funções de servidor:** `notify-appointment`, `notify-client-appointment`, `process-whatsapp-queue`, `send-whatsapp`, `client-appointment-reminders`, `task-reminders`, `admin-reset-data`, `create-barber-account`, `setup-account`, `uazapi-webhook`.
- **WhatsApp:** integração Uazapi com fila automática (processada a cada minuto) e alternativa via wa.me / WhatsApp Web.
- **Push:** OneSignal.

### Estrutura
```text
src/
  pages/admin/        Painel do administrador
  pages/colaborador/  Área do barbeiro
  pages/cliente/      Área do cliente
  pages/auth/         Telas de login
  components/         Componentes (booking, admin, colaborador, ui...)
  hooks/              Acesso a dados e autenticação
  lib/                Utilitários (datas, preços, telefone, WhatsApp)
supabase/functions/   Funções de servidor
```

---

## Rodar localmente

Requisito: Node.js 18+ (ou Bun).

```sh
git clone <URL_DO_REPOSITORIO>
cd <PASTA_DO_PROJETO>
npm install
npm run dev
```

O arquivo `.env` é gerado automaticamente pelo Lovable Cloud (`VITE_SUPABASE_URL`, `VITE_SUPABASE_PUBLISHABLE_KEY`, `VITE_SUPABASE_PROJECT_ID`).

## Publicação
No editor do Lovable: **Publicar → Atualizar**.
