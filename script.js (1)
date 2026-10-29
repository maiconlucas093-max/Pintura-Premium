
/*
  CONFIGURAÇÃO DO SITE
  Troque o número abaixo pelo WhatsApp real do pintor.
  Use código do país + DDD + número, somente dígitos.
  Exemplo de formato: 5531999999999
*/

const CONFIG = {
  nome: "Pintura Premium",
  whatsapp: "5531999999999"
};

// Menu para celular
const menuToggle = document.getElementById("menuToggle");
const nav = document.getElementById("nav");

if (menuToggle && nav) {
  menuToggle.addEventListener("click", () => {
    const aberto = nav.classList.toggle("open");

    menuToggle.setAttribute("aria-expanded", String(aberto));
    menuToggle.setAttribute(
      "aria-label",
      aberto ? "Fechar menu" : "Abrir menu"
    );
    menuToggle.textContent = aberto ? "✕" : "☰";
  });

  nav.querySelectorAll("a").forEach((link) => {
    link.addEventListener("click", () => {
      nav.classList.remove("open");
      menuToggle.setAttribute("aria-expanded", "false");
      menuToggle.setAttribute("aria-label", "Abrir menu");
      menuToggle.textContent = "☰";
    });
  });
}

// Ano automático no rodapé
const year = document.getElementById("year");

if (year) {
  year.textContent = new Date().getFullYear();
}

// Validação básica do número do WhatsApp
function numeroWhatsAppValido() {
  const numero = String(CONFIG.whatsapp).replace(/\D/g, "");

  // O número de exemplo não pode ser usado para atendimento real.
  if (
    !numero ||
    numero === "5531999999999" ||
    numero.length < 12 ||
    numero.length > 15
  ) {
    return false;
  }

  return numero;
}

// Abre a conversa com uma mensagem preparada
function abrirWhatsApp(mensagem) {
  const numero = numeroWhatsAppValido();

  if (!numero) {
    mostrarStatus(
      "Configure o número real do WhatsApp no arquivo script.js antes de receber pedidos."
    );
    return;
  }

  const url =
    "https://wa.me/" +
    numero +
    "?text=" +
    encodeURIComponent(mensagem);

  window.open(url, "_blank", "noopener,noreferrer");
}

// Mensagem de estado para o formulário
function mostrarStatus(mensagem) {
  const status = document.getElementById("formStatus");

  if (!status) return;

  status.textContent = mensagem;
  status.classList.add("visible");
}

// Botões diretos do WhatsApp
const mensagemDireta =
  "Olá! Gostaria de conhecer os serviços de pintura e solicitar um orçamento.";

["directWhatsApp", "floatingWhatsApp"].forEach((id) => {
  const link = document.getElementById(id);

  if (!link) return;

  link.addEventListener("click", (event) => {
    event.preventDefault();
    abrirWhatsApp(mensagemDireta);
  });
});

// Formulário de orçamento
const quoteForm = document.getElementById("quoteForm");

if (quoteForm) {
  quoteForm.addEventListener("submit", (event) => {
    event.preventDefault();

    if (!quoteForm.reportValidity()) return;

    const dados = new FormData(quoteForm);

    const campos = {
      nome: dados.get("nome"),
      telefone: dados.get("telefone"),
      imovel: dados.get("imovel"),
      servico: dados.get("servico"),
      area: dados.get("area"),
      estado: dados.get("estado"),
      local: dados.get("local"),
      prazo: dados.get("prazo"),
      detalhes: dados.get("detalhes")
    };

    const mensagem = [
      "Olá! Gostaria de solicitar um orçamento de pintura.",
      "",
      "NOME: " + (campos.nome || "Não informado"),
      "TELEFONE: " + (campos.telefone || "Não informado"),
      "",
      "TIPO DE IMÓVEL: " + (campos.imovel || "Não informado"),
      "SERVIÇO: " + (campos.servico || "Não informado"),
      "ÁREA APROXIMADA: " + (campos.area || "Não informada"),
      "ESTADO DAS PAREDES: " + (campos.estado || "Não informado"),
      "LOCAL: " + (campos.local || "Não informado"),
      "PRAZO: " + (campos.prazo || "Não informado"),
      "",
      "DETALHES:",
      campos.detalhes || "Nenhum detalhe adicional informado.",
      "",
      "Aguardo o retorno para avaliação e orçamento. Obrigado!"
    ].join("\n");

    const numero = numeroWhatsAppValido();

    if (!numero) {
      mostrarStatus(
        "O formulário está funcionando, mas falta configurar o número real do WhatsApp no script.js."
      );
      return;
    }

    mostrarStatus("Abrindo o WhatsApp para você revisar e enviar seu pedido...");

    abrirWhatsApp(mensagem);
  });
}
