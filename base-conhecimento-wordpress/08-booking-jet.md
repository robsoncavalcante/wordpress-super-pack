# JetBooking e JetAppointments Booking — reservas e agenda

## Escopo

Este módulo cobre JetBooking 4.1.2.2 e JetAppointments Booking 2.5.1.1 como soluções distintas para reserva de recursos e agendamento de horários.

## 1. Reserva versus appointment

### JetBooking

Modelo orientado a recurso e disponibilidade: imóvel, quarto, equipamento, veículo ou unidade reservável. O sistema precisa controlar períodos, ocupação, preço, status e conflitos.

### JetAppointments Booking

Modelo orientado a slots de agenda: profissional, serviço, duração, intervalo, horário de funcionamento e participantes.

Não escolher pela aparência do formulário. A escolha deve partir da regra de disponibilidade e do ciclo de vida da reserva.

## 2. Modelo mínimo de domínio

Toda implementação deve definir:

- recurso ou profissional;
- serviço ou produto reservado;
- timezone de armazenamento e exibição;
- janela de disponibilidade;
- duração e intervalos;
- capacidade máxima;
- bloqueios e exceções;
- status da reserva;
- proprietário e participantes;
- preço, se houver;
- política de cancelamento;
- notificações;
- retenção e privacidade.

## 3. Estados

Os estados devem ser explícitos e transicionáveis:

`rascunho → pendente → confirmada → concluída`

Com caminhos alternativos:

`pendente → recusada`, `confirmada → cancelada`, `confirmada → no-show`, `pendente → expirada`.

Cada transição deve ter autorização, evento, log e efeito definido. Não alterar status apenas ocultando ou mostrando um widget.

## 4. Concorrência e dupla reserva

O risco mais importante é duas requisições confirmarem o mesmo slot ou recurso.

Requisitos:

- verificar disponibilidade no servidor;
- revalidar imediatamente antes da confirmação;
- usar operação atômica ou mecanismo de lock apropriado;
- impedir confirmação duplicada;
- tratar retry de webhook e refresh do usuário;
- liberar reservas pendentes expiradas;
- registrar identificador idempotente.

Uma checagem visual no calendário não é garantia de disponibilidade.

## 5. Timezone e datas

- Definir timezone do negócio e do usuário.
- Armazenar datas em formato consistente.
- Converter somente na borda de entrada e saída.
- Testar horário de verão quando aplicável.
- Validar virada de dia, meia-noite e reservas que atravessam datas.
- Não misturar timestamp local com UTC sem contrato explícito.

## 6. Formulários

Formulários devem:

- validar datas, horários, recurso, quantidade e contato;
- verificar ownership e autorização;
- proteger CSRF com nonce;
- limitar spam e abuso;
- não confiar em hidden fields para preço, status ou proprietário;
- mostrar mensagens sem expor dados internos;
- criar apenas um registro por tentativa idempotente;
- separar pré-reserva de confirmação.

## 7. Pagamentos e notificações

Pagamento não deve ser considerado confirmado apenas porque o usuário retornou ao site. A confirmação deve vir do gateway validado, normalmente por webhook assinado.

Notificações precisam definir:

- evento que dispara;
- destinatário;
- template;
- retry;
- deduplicação;
- falha e reenvio;
- dados pessoais incluídos.

## 8. Integração com JetEngine e Elementor

- JetEngine pode fornecer campos editoriais e entidades auxiliares.
- O estado transacional da reserva precisa ter fonte única.
- Elementor deve apresentar formulário, calendário, confirmação e histórico.
- Dynamic Visibility não substitui autorização.
- Listings de reservas devem filtrar pelo usuário autorizado no servidor.
- Cache de página não pode servir disponibilidade ou histórico de outro usuário.

## 9. Segurança e privacidade

- Validar capacidade do usuário em criar, editar, cancelar e visualizar.
- Restringir endpoints e payloads.
- Não expor agenda completa de profissionais sem regra de privacidade.
- Escapar nomes, notas e mensagens inseridas pelo usuário.
- Minimizar dados pessoais armazenados.
- Definir retenção, exportação e exclusão.
- Não registrar tokens, dados de cartão ou informações desnecessárias.
- Proteger links de confirmação e cancelamento com tokens expiráveis e uso único.

## 10. Testes obrigatórios

- dois usuários tentando o mesmo slot;
- timezone diferente do servidor;
- horário de verão ou virada de dia;
- slot expirado;
- cancelamento dentro e fora da política;
- pagamento aprovado, recusado e pendente;
- webhook repetido;
- formulário reenviado;
- usuário anônimo e autenticado;
- recurso sem disponibilidade;
- capacidade parcial;
- notificação duplicada ou falha de e-mail;
- cache ativo;
- exportação e exclusão de dados.

## 11. Padrão de implementação

1. Modelar recurso, serviço e participante.
2. Definir timezone e estado.
3. Definir disponibilidade e exceções.
4. Implementar consulta de disponibilidade.
5. Revalidar no servidor durante a confirmação.
6. Tornar confirmação e webhook idempotentes.
7. Integrar pagamento e notificações.
8. Criar telas Elementor com dados autorizados.
9. Testar concorrência, cache e falhas.
10. Documentar recuperação e cancelamento.

## Limites

Ainda falta validar em runtime os mecanismos específicos de disponibilidade, locks, status, pagamentos e notificações de cada versão. Não se deve tratar a inspeção estática como prova de proteção contra dupla reserva.
