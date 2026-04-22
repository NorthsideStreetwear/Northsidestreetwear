## Hi there 👋

<!--
**NorthsideStreetwear/Northsidestreetwear** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
import os

base_dir = '/mnt/agents/output/northside_complete'
os.makedirs(base_dir, exist_ok=True)
os.makedirs(f'{base_dir}/admin', exist_ok=True)

# Write the complete JavaScript as a separate file
js_content = '''
// ============================================
// NORTHSIDE STREETWEAR - MAIN JAVASCRIPT
// ============================================

// Stripe Configuration - REPLACE WITH YOUR KEYS
const STRIPE_PUBLIC_KEY = 'pk_test_SUA_CHAVE_PUBLICA_AQUI';
const STRIPE_SECRET_KEY = 'sk_test_SUA_CHAVE_SECRETA_AQUI'; // Server-side only
let stripe = null;
let cardElement = null;

// Initialize Stripe
function initStripe() {
    if (!stripe && STRIPE_PUBLIC_KEY !== 'pk_test_SUA_CHAVE_PUBLICA_AQUI') {
        stripe = Stripe(STRIPE_PUBLIC_KEY);
    }
}

// ============================================
// DATA MANAGEMENT
// ============================================

function getProducts() {
    const saved = localStorage.getItem('ns_products');
    if (saved) return JSON.parse(saved);
    return defaultProducts;
}

function getPerfumes() {
    const saved = localStorage.getItem('ns_perfumes');
    if (saved) return JSON.parse(saved);
    return defaultPerfumes;
}

const defaultProducts = [
    {
        id: 1,
        name: "DRAGON HOODIE",
        category: "outerwear",
        price: 299,
        stock: 15,
        description: "Moletom oversize com estampa de dragão em serigrafia de alta definição. Capuz duplo, bolso canguru, punhos largos.",
        details: ["100% algodão francês 400g", "Estampa em serigrafia 3D", "Corte oversize unissex", "Punhos e barra em ribana"],
        sizes: ["P", "M", "G", "GG"],
        image: "DRAGON HOODIE",
        active: true
    },
    {
        id: 2,
        name: "ONI MASK TEE",
        category: "tops",
        price: 149,
        stock: 42,
        description: "Camiseta longline com estampa minimalista de máscara Oni no peito esquerdo. Tecido premium com lavagem enzyme.",
        details: ["100% algodão 180g", "Corte longline", "Lavagem enzyme", "Estampa em waterbase"],
        sizes: ["P", "M", "G", "GG", "XG"],
        image: "ONI MASK TEE",
        active: true
    },
    {
        id: 3,
        name: "CARGO DRAGON",
        category: "bottoms",
        price: 259,
        stock: 8,
        description: "Calça cargo baggy com bolsos laterais em zíper. Patch de dragão bordado no bolso traseiro. Silhueta larga, barra longa.",
        details: ["Sarja 320g", "Silhueta baggy", "Bolsos cargo com zíper", "Patch bordado 3D"],
        sizes: ["36", "38", "40", "42", "44"],
        image: "CARGO DRAGON",
        active: true
    },
    {
        id: 4,
        name: "KOI JOGGER",
        category: "bottoms",
        price: 229,
        stock: 23,
        description: "Jogger tapered com estampa sublimada de carpa koi na perna. Cós elástico com cordão externo. Moletom francês.",
        details: ["Moletom francês 280g", "Corte tapered", "Estampa sublimada", "Cós elástico com cordão"],
        sizes: ["P", "M", "G", "GG"],
        image: "KOI JOGGER",
        active: true
    },
    {
        id: 5,
        name: "ALFAIATARIA SAMURAI",
        category: "bottoms",
        price: 289,
        stock: 12,
        description: "Calça de alfaiataria street com corte reto. Prega frontal, faixa lateral com ideograma bordado. Tecido poli-viscose com queda pesada.",
        details: ["Poli-viscose premium", "Corte reto baggy-skinny", "Prega frontal", "Bordado lateral"],
        sizes: ["36", "38", "40", "42", "44"],
        image: "ALFAIATARIA SAMURAI",
        active: true
    },
    {
        id: 6,
        name: "SAKURA GRUNGE TEE",
        category: "tops",
        price: 169,
        stock: 35,
        description: "Camiseta full-print com estampa de sakura em preto e branco com pinceladas grunge. Efeito tie-dye sutil.",
        details: ["100% algodão 200g", "Full-print digital", "Efeito tie-dye", "Corte regular"],
        sizes: ["P", "M", "G", "GG", "XG"],
        image: "SAKURA GRUNGE",
        active: true
    }
];

const defaultPerfumes = [
    {
        id: 101,
        name: "ONI",
        subtitle: "Eau de Parfum",
        price: 289,
        stock: 20,
        description: "A dualidade entre a fúria e a serenidade. Inspirado na máscara de Oni do teatro Noh — demônio protetor, não maligno.",
        longevity: "8-10 horas",
        projection: "Moderada-Alta",
        occasion: "Noite, eventos, encontros onde você quer deixar rastro.",
        pyramid: {
            top: "Pimenta Preta, Zimbro, Bergamota",
            heart: "Sândalo, Incenso de Kyoto, Ládano",
            base: "Âmbar Gris, Patchouli, Baunilha Negra"
        },
        color: "ns-red",
        image: "ONI",
        active: true
    },
    {
        id: 102,
        name: "SAKURA",
        subtitle: "Eau de Parfum",
        price: 269,
        stock: 18,
        description: "A beleza efêmera que deixa marca permanente. Captura o momento exato entre o botão e a queda da pétala.",
        longevity: "6-8 horas",
        projection: "Suave-Moderada",
        occasion: "Dia, escritório, encontros casuais, primavera o ano todo.",
        pyramid: {
            top: "Flor de Cerejeira, Pera Nashi, Pimenta Rosa",
            heart: "Jasmim Sambac, Lótus, Chá Verde Matcha",
            base: "Almíscar Branco, Cedro, Baunilha"
        },
        color: "ns-cream",
        image: "SAKURA",
        active: true
    },
    {
        id: 103,
        name: "DRAGON'S BLOOD",
        subtitle: "Eau de Parfum Intense",
        price: 319,
        stock: 10,
        description: "O sangue do dragão queimando no peito. Resina rara de Dracaena cinnabari usada em rituais orientais.",
        longevity: "12+ horas",
        projection: "Alta",
        occasion: "Noite fria, eventos especiais, quando você é o centro.",
        pyramid: {
            top: "Açafrão, Cardamomo, Laranja Sanguínea",
            heart: "Resina de Olibano, Rosa de Damasco, Oud",
            base: "Sangue de Dragão (resina), Patchouli, Couro"
        },
        color: "ns-gold",
        image: "DRAGON'S BLOOD",
        active: true
    },
    {
        id: 104,
        name: "NORTHSIDE",
        subtitle: "Eau de Parfum — Signature",
        price: 249,
        stock: 30,
        description: "O cheiro da rua quando tudo está prestes a começar. O perfume da marca. Urbano, concreto, mas com raízes orientais.",
        longevity: "6-8 horas",
        projection: "Moderada",
        occasion: "Qualquer hora, qualquer lugar. O daily driver da coleção.",
        pyramid: {
            top: "Limão Negro, Gengibre, Folha de Violeta",
            heart: "Cedro, Vetiver, Pimenta de Jamaica",
            base: "Âmbar, Almíscar, Baunilha de Madagascar"
        },
        color: "ns-silver",
        image: "NORTHSIDE",
        active: true
    }
];

// Initialize data
if (!localStorage.getItem('ns_products')) {
    localStorage.setItem('ns_products', JSON.stringify(defaultProducts));
}
if (!localStorage.getItem('ns_perfumes')) {
    localStorage.setItem('ns_perfumes', JSON.stringify(defaultPerfumes));
}

let cart = JSON.parse(localStorage.getItem('ns_cart') || '[]');
let currentTab = 'all';

// ============================================
// RENDER FUNCTIONS
// ============================================

function renderProducts() {
    const products = getProducts().filter(p => p.active);
    const grid = document.getElementById('products-grid');
    const filtered = currentTab === 'all' ? products : products.filter(p => p.category === currentTab);
    
    grid.innerHTML = filtered.map(product => `
        <div class="product-card bg-ns-gray rounded-lg overflow-hidden section-hidden" onclick="openProductModal(${product.id})">
            <div class="aspect-[3/4] img-placeholder product-image">${product.image}</div>
            <div class="p-6">
                <div class="flex justify-between items-start mb-2">
                    <div>
                        <p class="font-mono text-[10px] tracking-[0.2em] text-ns-red mb-1">${product.category.toUpperCase()}</p>
                        <h3 class="font-bebas text-xl tracking-wider text-ns-cream">${product.name}</h3>
                    </div>
                </div>
                <div class="flex justify-between items-center">
                    <p class="font-mono text-lg text-ns-cream">R$ ${product.price},00</p>
                    <p class="font-mono text-[10px] text-ns-silver">${product.stock} disp.</p>
                </div>
            </div>
        </div>
    `).join('');
    
    setTimeout(() => {
        document.querySelectorAll('#products-grid .section-hidden').forEach(el => {
            el.classList.add('section-visible');
        });
    }, 100);
}

function renderPerfumes() {
    const perfumes = getPerfumes().filter(p => p.active);
    const grid = document.getElementById('perfumes-grid');
    
    grid.innerHTML = perfumes.map((perfume, index) => `
        <div class="product-card bg-ns-black border border-ns-gray rounded-lg overflow-hidden section-hidden" style="animation-delay: ${index * 0.1}s" onclick="openPerfumeModal(${perfume.id})">
            <div class="aspect-square img-placeholder product-image flex flex-col items-center justify-center gap-2">
                <span class="font-bebas text-2xl tracking-widest">${perfume.image}</span>
                <span class="font-cormorant text-sm italic text-${perfume.color === 'ns-cream' ? 'ns-cream' : perfume.color}">100ml</span>
            </div>
            <div class="p-6">
                <div class="flex justify-between items-start mb-2">
                    <div>
                        <p class="font-mono text-[10px] tracking-[0.2em] text-${perfume.color === 'ns-cream' ? 'ns-cream' : perfume.color} mb-1">FRAGRÂNCIA</p>
                        <h3 class="font-bebas text-2xl tracking-wider text-ns-cream">${perfume.name}</h3>
                        <p class="font-cormorant text-sm text-ns-silver italic">${perfume.subtitle}</p>
                    </div>
                </div>
                <div class="flex justify-between items-center mt-3">
                    <p class="font-mono text-lg text-ns-cream">R$ ${perfume.price},00</p>
                    <p class="font-mono text-[10px] text-ns-silver">${perfume.stock} disp.</p>
                </div>
                <div class="mt-3 flex gap-2">
                    <span class="font-mono text-[10px] text-ns-silver bg-ns-gray px-2 py-1 rounded">${perfume.longevity}</span>
                    <span class="font-mono text-[10px] text-ns-silver bg-ns-gray px-2 py-1 rounded">${perfume.projection}</span>
                </div>
            </div>
        </div>
    `).join('');
    
    setTimeout(() => {
        document.querySelectorAll('#perfumes-grid .section-hidden').forEach(el => {
            el.classList.add('section-visible');
        });
    }, 100);
}

function switchTab(tab) {
    currentTab = tab;
    document.querySelectorAll('.tab-btn').forEach(btn => {
        btn.classList.remove('active');
        if(btn.dataset.tab === tab) btn.classList.add('active');
    });
    renderProducts();
}

// ============================================
// MODALS
// ============================================

function openProductModal(id) {
    const product = getProducts().find(p => p.id === id);
    if(!product || !product.active) return;
    
    document.getElementById('modal-image').textContent = product.image;
    document.getElementById('modal-content').innerHTML = `
        <p class="font-mono text-[10px] tracking-[0.2em] text-ns-red mb-2">${product.category.toUpper
