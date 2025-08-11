// Demo data sản phẩm
const products = [
  { id:1, title:"Acc Liên Quân - Rank Cao", desc:"Rank Cao + skin xịn", price:"120.000đ", img:"https://via.placeholder.com/400x240?text=LQ" },
  { id:2, title:"Acc PUBG - Prime", desc:"Acc prime, nhiều skin", price:"90.000đ", img:"https://via.placeholder.com/400x240?text=PUBG" },
  { id:3, title:"Acc Free Fire - Elite", desc:"Acc elite, tướng đẹp", price:"75.000đ", img:"https://via.placeholder.com/400x240?text=FF" },
  { id:4, title:"Acc LMHT - Cao Rank", desc:"Rank Cao + rune chuẩn", price:"150.000đ", img:"https://via.placeholder.com/400x240?text=LOL" }
];

const grid = document.getElementById('product-grid');
const modal = document.getElementById('buyModal');
const modalTitle = document.getElementById('modal-title');
const modalDesc = document.getElementById('modal-desc');
const modalClose = document.getElementById('modalClose');
const confirmBuy = document.getElementById('confirmBuy');
let selectedProduct = null;

function renderProducts(){
  grid.innerHTML = '';
  products.forEach(p => {
    const card = document.createElement('div');
    card.className = 'card';
    card.innerHTML = `
      <img src="${p.img}" alt="${p.title}">
      <h3>${p.title}</h3>
      <p>${p.desc}</p>
      <div class="meta">
        <div class="price">${p.price}</div>
        <button class="btn small" data-id="${p.id}">Mua</button>
      </div>
    `;
    grid.appendChild(card);
  });

  grid.querySelectorAll('button[data-id]').forEach(btn=>{
    btn.addEventListener('click', (e)=>{
      const id = +e.currentTarget.dataset.id;
      openModal(products.find(x=>x.id===id));
    });
  });
}

function openModal(product){
  selectedProduct = product;
  modalTitle.textContent = `Mua: ${product.title}`;
  modalDesc.textContent = `${product.desc} — Giá: ${product.price}`;
  modal.classList.remove('hidden');
  modal.setAttribute('aria-hidden','false');
}

function closeModal(){
  modal.classList.add('hidden');
  modal.setAttribute('aria-hidden','true');
}

modalClose.addEventListener('click', closeModal);
modal.addEventListener('click', (e)=>{
  if(e.target === modal) closeModal();
});

confirmBuy.addEventListener('click', ()=>{
  const name = document.getElementById('buyerName').value.trim();
  if(!name){
    alert('Nhập tên người mua để tiếp tục (demo).');
    return;
  }
  // Demo: hiển thị thông tin order (không có thanh toán)
  alert(`Cảm ơn ${name}!\nYêu cầu mua "${selectedProduct.title}" đã được ghi (demo).`);
  closeModal();
});

document.getElementById('year').textContent = new Date().getFullYear();
document.getElementById('btn-login').addEventListener('click', ()=> alert('Demo: chức năng đăng nhập chưa có.'));

renderProducts();
