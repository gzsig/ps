# 🧪 Desafio Técnico – Desenvolvedor(a) Mevo

Olá! 👋

Antes de mais nada, parabéns por chegar até aqui no nosso processo seletivo 🙌

Esse desafio tem como objetivo entender como você estrutura uma aplicação do zero, como toma decisões técnicas e como resolve problemas. Não buscamos algo perfeito ou finalizado — estamos interessados no **seu raciocínio** e **boas decisões** ao longo do caminho.

## 🧠 Contexto

Na Mevo, conectamos marketplaces na nossa farmacia com tecnologia e velocidade. Imagine que estamos construindo o módulo de pedidos de compra de medicamentos e queremos sua ajuda para começar esse sistema!

Você recebeu uma tarefa urgente: construir uma **API** simples que:

1. **Recebe pedidos de compra de medicamentos** e salva no banco de dados.
2. Permite **atualizar o status** do pedido ao longo do tempo.
3. Quando o status muda para **`faturado`**, **chama uma API externa** que aciona um motoboy para fazer a entrega.
4. Quando o status muda para **`entregue`**, **o pedido deve ser travado**, ou seja, **não pode mais ser alterado**.
5. Um cliente (frontend ou app) deve ser capaz de:

   * Listar todos os pedidos
   * Consultar os dados detalhados de um pedido específico

> Pode ser uma API REST ou GraphQL, A escolha é sua — apenas esteja pronto para explicar o motivo da decisão.

---

## ✅ O que esperamos que você implemente

Você terá **até 2 horas** para desenvolver e apresentar sua solução. Sabemos que o tempo é curto, então o mais importante é:

* Mostrar **boas decisões de design**
* Escrever **código claro e consistente**
* Compartilhar **seu raciocínio ao longo do processo**

### Funcionalidades mínimas esperadas

* [ ] Criar um novo pedido
* [ ] Atualizar status do pedido
* [ ] Listar todos os pedidos
* [ ] Buscar um pedido por ID
* [ ] Impedir alteração se o pedido estiver com status `entregue`
* [ ] Chamar uma API externa (fictícia ou mockada) quando status for `faturado`

---

## 🧩 O modelo de dados é livre, mas pense em algo como:

```ts
interface Order {
  buyer: {name: string, cpf: string}
  items: Array<{ name: string; quantity: number, price: number }>;
  status: 'pendente' | 'na entrega' | 'faturado' | 'entregue' | 'cancelado';
}
```

---

## 🚚 Sobre a "API do motoboy"

Você **não precisa integrar** com nenhum serviço real. Basta simular a chamada com uma função como essa:

```ts
function requestMotoboy(orderId: string): Promise<void> {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const falhou = Math.random() < 0.25;
      if (falhou) {
        return reject(new Error(`[MOTOBOY] Falha ao agendar entrega do pedido ${orderId}`));
      }
      console.log(`[MOTOBOY] Pedido ${orderId} enviado para entrega.`);
      resolve();
    }, 1000); // simula delay de 1 segundo
  });
}

```

Ela deve ser chamada apenas uma vez quando o status de um pedido muda para faturado.


---

## 🧠 Algumas provocações

* Como esse sistema **escala** se passarmos de 100 para 10.000 pedidos por dia?
* Como você separaria responsabilidades na aplicação?
* Como garantir que a chamada ao motoboy **não falhe silenciosamente**?
* Como evitar que um pedido seja alterado depois de entregue ou cancelado?
* Onde você colocaria logs e validações?
* Como lidaria com múltiplas atualizações concorrentes no mesmo pedido?
* Como você implementaria testes na aplicação

---

## 🛠️ Requisitos técnicos

* Recomendamos o uso de **TypeScript**
* Use **Node.js** com o framework de sua preferência (Express, NestJS, etc.)
* Pode usar um banco em memória ou SQLite para simplificar (não precisa configurar PostgreSQL ou algo mais robusto)
* Não use ferramentas de geração automática de código como GitHub Copilot ou ChatGPT
* Use Google, Stack Overflow, documentação — tudo que você usaria no dia a dia (exceto LLMs 😉)

---

## 🤝 Durante a entrevista

* Compartilhe sua tela desde o início
* Explique seu raciocínio e decisões em voz alta
* Pode parar para pesquisar, perguntar, discutir
* Erros e dúvidas são bem-vindos — estamos aqui para ver **como você pensa**, não só o que você sabe

---

Vamos nessa!

Time Mevo 🧪
