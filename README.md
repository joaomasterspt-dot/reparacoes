
<!DOCTYPE html>
<html lang="pt">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>TECHSTORE - Loja Informática</title>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Arial, sans-serif;
}

body {
    background: #f3f5f8;
    color: #222;
}

header {
    background: #101827;
    color: white;
    padding: 22px 8%;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.logo {
    font-size: 25px;
    font-weight: bold;
    color: #38bdf8;
}

nav a {
    color: white;
    text-decoration: none;
    margin-left: 20px;
}

.hero {
    background: linear-gradient(120deg,#101827,#164e75);
    color: white;
    padding: 85px 8%;
    text-align: center;
}

.hero h1 {
    font-size: 42px;
    margin-bottom: 15px;
}

.hero p {
    font-size: 18px;
    margin-bottom: 25px;
}

.btn {
    background: #38bdf8;
    color: #101827;
    padding: 13px 25px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-weight: bold;
}

.container {
    padding: 45px 8%;
}

.container h2 {
    margin-bottom: 25px;
}

.search {
    width: 100%;
    padding: 14px;
    border: 1px solid #ddd;
    border-radius: 6px;
    margin-bottom: 25px;
}

.products {
    display: grid;
    grid-template-columns: repeat(auto-fit,minmax(220px,1fr));
    gap: 22px;
}

.product {
    background: white;
    padding: 20px;
    border-radius: 10px;
    text-align: center;
    box-shadow: 0 3px 12px #00000010;
}

.product img {
    width: 100%;
    height: 160px;
    object-fit: contain;
    margin-bottom: 15px;
}

.product h3 {
    margin-bottom: 10px;
}

.price {
    color: #07834c;
    font-size: 22px;
    font-weight: bold;
    margin: 12px 0;
}

.product button {
    background: #101827;
    color: white;
    padding: 12px;
    border: none;
    border-radius: 5px;
    width: 100%;
    cursor: pointer;
}

.product button:hover {
    background: #087eb0;
}

.cart {
    background: white;
    padding: 25px;
    border-radius: 10px;
    margin-top: 35px;
}

.cart-item {
    padding: 10px 0;
    border-bottom: 1px solid #ddd;
}

footer {
    background: #101827;
    color: white;
    padding: 35px;
    text-align: center;
    margin-top: 40px;
}

@media(max-width:600px) {
    header {
        flex-direction: column;
        gap: 15px;
    }

    nav a {
        margin: 5px;
        font-size: 13px;
    }

    .hero h1 {
        font-size: 30px;
    }
}
</style>
</head>

<body>

<header>
    <div class="logo">TECHSTORE</div>
    <nav>
        <a href="#inicio">Início</a>
        <a href="#produtos">Produtos</a>
        <a href="#carrinho">Carrinho</a>
        <a href="#contactos">Contactos</a>
    </nav>
</header>

<section class="hero" id="inicio">
    <h1>Tecnologia ao melhor preço!</h1>
    <p>Componentes, computadores e acessórios informáticos.</p>
    <a href="#produtos">
        <button class="btn">Ver produtos</button>
    </a>
</section>

<section class="container" id="produtos">
    <h2>Os nossos produtos</h2>

    <input
        class="search"
        id="search"
        placeholder="Pesquisar produtos..."
        oninput="pesquisar()"
    >

    <div class="products" id="listaProdutos"></div>

    <div class="cart" id="carrinho">
        <h2>🛒 O meu carrinho</h2>
        <div id="itensCarrinho">Ainda não existem produtos.</div>
        <h3 id="total">Total: 0,00 €</h3>
        <button class="btn" onclick="finalizar()">
            Finalizar pedido
        </button>
    </div>
</section>

<section class="container" id="contactos">
    <h2>Contacta-nos</h2>
    <p>Email: geral@techstore.pt</p>
    <p>Telefone: 912 345 678</p>
    <p>Localização: Portugal</p>
</section>

<footer>
    <p>© 2026 TECHSTORE - Todos os direitos reservados.</p>
    <p>A tua loja de informática!</p>
</footer>

<script>

// EDITA AQUI OS TEUS PRODUTOS

const produtos = [
    {
        nome: "Placa Gráfica RTX",
        preco: 599.99,
        imagem: "https://placehold.co/300x200?text=Placa+Grafica"
    },
    {
        nome: "Processador Ryzen",
        preco: 249.99,
        imagem: "https://placehold.co/300x200?text=Processador"
    },
    {
        nome: "Memória RAM DDR5",
        preco: 89.99,
        imagem: "https://placehold.co/300x200?text=Memoria+RAM"
    },
    {
        nome: "SSD NVMe 1TB",
        preco: 79.99,
        imagem: "https://placehold.co/300x200?text=SSD"
    },
    {
        nome: "Motherboard Gaming",
        preco: 159.99,
        imagem: "https://placehold.co/300x200?text=Motherboard"
    },
    {
        nome: "Fonte 750W",
        preco: 99.99,
        imagem: "https://placehold.co/300x200?text=Fonte"
    }
];

let carrinho = [];

function mostrarProdutos(lista = produtos) {
    const area = document.getElementById("listaProdutos");

    area.innerHTML = lista.map((p, i) => `
        <div class="product">
            <img src="${p.imagem}" alt="${p.nome}">
            <h3>${p.nome}</h3>
            <div class="price">${p.preco.toFixed(2)} €</div>
            <button onclick="adicionar('${p.nome}')">
                Adicionar ao carrinho
            </button>
        </div>
    `).join("");
}

function pesquisar() {
    const termo = document.getElementById("search")
        .value.toLowerCase();

    const filtrados = produtos.filter(p =>
        p.nome.toLowerCase().includes(termo)
    );

    mostrarProdutos(filtrados);
}

function adicionar(nome) {
    const produto = produtos.find(p => p.nome === nome);

    if (!produto) return;

    carrinho.push(produto);
    atualizarCarrinho();
}

function atualizarCarrinho() {
    const area = document.getElementById("itensCarrinho");
    const total = carrinho.reduce((s, p) => s + p.preco, 0);

    if (carrinho.length === 0) {
        area.innerHTML = "Ainda não existem produtos.";
    } else {
        area.innerHTML = carrinho.map((p, i) => `
            <div class="cart-item">
                ${p.nome} - ${p.preco.toFixed(2)} €
                <button onclick="remover(${i})">Remover</button>
            </div>
        `).join("");
    }

    document.getElementById("total").innerText =
        "Total: " + total.toFixed(2) + " €";
}

function remover(i) {
    carrinho.splice(i, 1);
    atualizarCarrinho();
}

function finalizar() {
    if (carrinho.length === 0) {
        alert("O carrinho está vazio!");
        return;
    }

    let mensagem = "Pedido TECHSTORE:%0A";

    carrinho.forEach(p => {
        mensagem += "- " + encodeURIComponent(p.nome) +
        " - " + p.preco.toFixed(2) + " €%0A";
    });

    const total = carrinho.reduce((s,p) => s+p.preco,0);

    mensagem += "%0ATotal: " + total.toFixed(2) + " €";

    // ALTERA PELO TEU NÚMERO DE WHATSAPP
    const telefone = "351912345678";

    window.open(
        "https://wa.me/" + telefone + "?text=" + mensagem,
        "_blank"
    );
}

mostrarProdutos();

</script>

</body>
</html>
