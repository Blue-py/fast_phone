/* app.js — Fast Phone (Firebase modular SDK) */
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";
import {
  getAuth,
  GoogleAuthProvider,
  signInWithPopup,
  setPersistence,
  browserLocalPersistence,
  signOut,
  onAuthStateChanged
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";
import {
  getFirestore,
  collection,
  addDoc,
  doc,
  updateDoc,
  deleteDoc,
  getDocs,
  onSnapshot,
  query,
  orderBy
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";
import {
  getStorage,
  ref as storageRef,
  uploadBytes,
  getDownloadURL
} from "https://www.gstatic.com/firebasejs/10.12.2/firebase-storage.js";

/* ================= Firebase config ================= */
const firebaseConfig = {
  apiKey: "AIzaSyB5dqUC2YubUVMuWP8_wLznve0Tx8TB_rM",
  authDomain: "fast-phone-7b145.firebaseapp.com",
  projectId: "fast-phone-7b145",
  storageBucket: "fast-phone-7b145.appspot.com",
  messagingSenderId: "614637173695",
  appId: "1:614637173695:web:7249c266d38d41b3b97f0a",
  measurementId: "G-KJZWYEEBVD"
};

const app = initializeApp(firebaseConfig);
const auth = getAuth(app);
const provider = new GoogleAuthProvider();
const db = getFirestore(app);
const storage = getStorage(app);

/* ================= App state & helpers ================= */
const OWNER_EMAIL = 'ayoubkobraff@gmail.com';
const LS_KEYS = { CART: 'ff_cart', LANG: 'ff_lang' };
const PHONE_OWNER = '213657340489';
const CURRENCY = 'د.ج';

const $ = (s, ctx = document) => ctx.querySelector(s);
const $$ = (s, ctx = document) => Array.from(ctx.querySelectorAll(s));
function uid(pref = 'id') { return `${pref}_${Math.random().toString(36).slice(2,9)}`; }
function toast(msg) {
  const el = document.createElement('div'); el.className = 'toast'; el.textContent = msg;
  document.body.appendChild(el); setTimeout(()=>el.remove(), 2200);
}
function formatPrice(n){ return `${Number(n||0).toLocaleString('ar-DZ')} ${CURRENCY}`; }

/* UI refs */
const loginBtn = $('#loginBtn');
const logoutBtn = $('#logoutBtn');
const userWrap = $('#userWrap');
const userName = $('#userName');
const userAvatar = $('#userAvatar');
const catalog = $('#catalog');
const cartItems = $('#cartItems');
const cartCount = $('#cartCount');
const cartTotal = $('#cartTotal');
const ownerDialog = $('#ownerDialog');

/* local state */
let currentUser = null;
let products = [];
let cart = JSON.parse(localStorage.getItem(LS_KEYS.CART) || '[]');
let currentLang = localStorage.getItem(LS_KEYS.LANG) || 'ar';

/* ============= Auth (safe popup) ============= */
async function signIn() {
  try {
    await setPersistence(auth, browserLocalPersistence);
    await signInWithPopup(auth, provider);
    // onAuthStateChanged will update UI
  } catch (err) {
    console.error('signIn error', err);
    if (err.code === 'auth/popup-closed-by-user') toast('تم إغلاق نافذة تسجيل الدخول.');
    else if (err.code === 'auth/popup-blocked') toast('النافذة المنبثقة محجوبة — سمح بالبنوافذ أو افتح عبر رابط مباشر.');
    else toast('خطأ في تسجيل الدخول — تحقق من إعدادات Firebase وAuthorized domains.');
  }
}
loginBtn.addEventListener('click', signIn);
logoutBtn.addEventListener('click', async ()=> {
  try{ await signOut(auth); } catch(e){ console.error(e); toast('خطأ في تسجيل الخروج'); }
});

onAuthStateChanged(auth, user => {
  currentUser = user || null;
  if (user) {
    loginBtn.style.display = 'none';
    userWrap.style.display = 'flex';
    logoutBtn.style.display = 'inline-block';
    userName.textContent = user.displayName || user.email;
    userAvatar.src = user.photoURL || ('https://i.pravatar.cc/64?u='+encodeURIComponent(user.email));
  } else {
    loginBtn.style.display = 'inline-block';
    userWrap.style.display = 'none';
    logoutBtn.style.display = 'none';
  }
  renderCatalog(); // to show/hide edit buttons
});

/* ============= Realtime products (Firestore) ============= */
const productsQ = query(collection(db,'products'), orderBy('createdAt','desc'));
onSnapshot(productsQ, snap => {
  products = []; snap.forEach(d => products.push({ id: d.id, ...d.data() }));
  renderCatalog();
  populateProductSelect();
}, err => {
  console.error('products snapshot error', err);
  toast('خطأ في مزامنة المنتجات. تحقق من قواعد Firestore.');
});

/* ============= Render catalog ============= */
function productCard(p){
  const name = (p.name && (p.name[currentLang] || p.name.ar)) || p.name || '—';
  const desc = (p.desc && (p.desc[currentLang] || p.desc.ar)) || '';
  const outOfStock = (p.stock||0) <= 0;
  return `
    <article class="product card" data-id="${p.id}">
      <div class="thumb">${p.imageURL ? `<img src="${p.imageURL}" alt="${name}" />` : '<div style="padding:1rem;color:var(--muted)">لا صورة</div>'}</div>
      <div class="body">
        <div style="display:flex;justify-content:space-between;align-items:center">
          <div style="font-weight:800">${name}</div>
          <div><span class="price">${formatPrice(p.price)}</span> ${p.oldPrice? `<span class="old">${formatPrice(p.oldPrice)}</span>`: ''}</div>
        </div>
        <div style="color:var(--muted);font-size:.95rem;margin-top:.4rem">${desc}</div>
        <div style="display:flex;gap:.4rem;margin-top:.6rem">
          <button class="btn" data-act="add" ${outOfStock?'disabled':''}>${currentLang==='ar'?'إضافة للسلة':'Add to cart'}</button>
          <button class="btn primary" data-act="buy" ${outOfStock?'disabled':''}>${currentLang==='ar'?'طلب':'Buy'}</button>
          ${currentUser && currentUser.email && currentUser.email.toLowerCase() === OWNER_EMAIL.toLowerCase() ? `<button class="btn" data-act="edit">تعديل</button>` : ''}
        </div>
      </div>
    </article>
  `;
}

function renderCatalog(){
  const q = $('#searchInput').value.trim().toLowerCase();
  const inStockOnly = $('#filterInStock').classList.contains('active');
  let list = [...products];
  if (q) list = list.filter(p => {
    const names = ((p.name && (p.name.ar||'') + ' ' + (p.name.fr||'')) || '').toLowerCase();
    const descs = ((p.desc && (p.desc.ar||'') + ' ' + (p.desc.fr||'')) || '').toLowerCase();
    return names.includes(q) || descs.includes(q);
  });
  if (inStockOnly) list = list.filter(p => (p.stock||0) > 0);
  const sort = $('#sortSelect').value;
  if(sort === 'price-asc') list.sort((a,b)=> (a.price||0) - (b.price||0));
  if(sort === 'price-desc') list.sort((a,b)=> (b.price||0) - (a.price||0));
  if(sort === 'new') list.sort((a,b)=> (b.createdAt||0) - (a.createdAt||0));
  if(sort === 'pop') list.sort((a,b)=> (b.pop||0) - (a.pop||0));
  catalog.innerHTML = list.map(productCard).join('') || '<div class="empty">لا يوجد منتجات</div>';

  // bind buttons
  $$('#catalog .product').forEach(card=>{
    const id = card.getAttribute('data-id');
    const item = products.find(x=>x.id === id);
    if(!item) return;
    card.querySelectorAll('button').forEach(btn=>{
      btn.addEventListener('click', ()=> {
        const act = btn.getAttribute('data-act');
        if(act === 'add') addToCart(item.id,1);
        if(act === 'buy'){ addToCart(item.id,1); openCheckout(); }
        if(act === 'edit'){ openEditDialog(item); }
      });
    });
  });

  updateCartUI();
}

/* ============= Cart ============= */
function saveCart(){ localStorage.setItem(LS_KEYS.CART, JSON.stringify(cart)); }
function updateCartUI(){
  cartCount.textContent = cart.reduce((s,r)=>s+r.qty,0);
  const { total } = calcCartTotal();
  cartTotal.textContent = formatPrice(total);
}
function renderCart(){
  if(!cart.length){ cartItems.innerHTML = '<div class="empty">السلة فارغة حالياً</div>'; updateCartUI(); return; }
  cartItems.innerHTML = cart.map(row => {
    const p = products.find(x=>x.id===row.id) || { name:{ar:'عنصر محذوف'}, price:0 };
    const name = (p.name && (p.name[currentLang]||p.name.ar)) || p.name;
    return `<div class="row" data-id="${row.id}">
      <div><div style="font-weight:800">${name}</div><div style="color:var(--muted)">${formatPrice(p.price)} × ${row.qty}</div></div>
      <div style="display:flex;gap:.4rem;align-items:center">
        <button class="icon-btn" data-act="dec">➖</button>
        <strong>${row.qty}</strong>
        <button class="icon-btn" data-act="inc">➕</button>
        <button class="icon-btn" data-act="del">🗑</button>
      </div>
    </div>`;
  }).join('');
  $$('#cartItems .row .icon-btn').forEach(btn=>{
    btn.addEventListener('click', ()=>{
      const rowEl = btn.closest('.row'); const id = rowEl.getAttribute('data-id'); const act = btn.getAttribute('data-act');
      const idx = cart.findIndex(x=>x.id===id); if(idx===-1) return;
      if(act==='inc') cart[idx].qty++;
      if(act==='dec') cart[idx].qty = Math.max(1, cart[idx].qty - 1);
      if(act==='del') cart.splice(idx,1);
      saveCart(); renderCart(); updateCartUI();
    });
  });
  updateCartUI();
}

function addToCart(id, qty=1){
  const p = products.find(x=>x.id===id);
  if(!p) return toast('منتج غير موجود');
  if((p.stock||0) <= 0) return toast('غير متوفر');
  const row = cart.find(x=>x.id===id);
  if(row) row.qty += qty; else cart.push({ id, qty });
  saveCart(); renderCart(); toast('أضيف إلى السلة');
}

function calcCartTotal(){
  let total = 0; cart.forEach(r=>{ const p = products.find(x=>x.id===r.id); if(p) total += (p.price||0) * r.qty; });
  return { total, grand: total };
}

$('#clearCart').addEventListener('click', ()=>{ cart=[]; saveCart(); renderCart(); updateCartUI(); });
$('#checkoutBtn').addEventListener('click', openCheckout);
function openCheckout(){
  if(!cart.length) return toast('السلة فارغة');
  const { total } = calcCartTotal();
  const lines = cart.map(r=>{ const p = products.find(x=>x.id===r.id); const name=(p.name && (p.name[currentLang]||p.name.ar))||p.name; return `• ${name} × ${r.qty} = ${formatPrice((p.price||0)*r.qty)}`; }).join('\n');
  const msg = `طلب جديد من Fast Phone\n\n${lines}\n\nالمجموع: ${formatPrice(total)}\n\nمن فضلك أكدوا التوفر والموعد.`;
  window.open(`https://wa.me/${PHONE_OWNER}?text=${encodeURIComponent(msg)}`, '_blank');
}

/* ============= Search & filters binding ============= */
$('#searchInput').addEventListener('input', ()=> renderCatalog());
$('#sortSelect').addEventListener('change', ()=> renderCatalog());
$('#filterInStock').addEventListener('click', e => { e.currentTarget.classList.toggle('active'); renderCatalog(); });

/* ============= Owner panel — CRUD ============= */
$('#openOwnerPanel').addEventListener('click', ()=>{
  if(!currentUser || (currentUser.email && currentUser.email.toLowerCase() !== OWNER_EMAIL.toLowerCase())) return toast('هذه الميزة للمالك فقط');
  populateProductSelect();
  ownerDialog.showModal();
});
$('#closeOwnerDialog').addEventListener('click', ()=> ownerDialog.close());

function populateProductSelect(){
  const sel = $('#productSelect');
  sel.innerHTML = products.map(p=>`<option value="${p.id}">${(p.name && (p.name.ar||p.name)) || p.name}</option>`).join('');
}

/* Add product: upload image then add doc */
$('#addProductBtn').addEventListener('click', async ()=>{
  if(!currentUser || currentUser.email.toLowerCase() !== OWNER_EMAIL.toLowerCase()) return toast('غير مصرح');
  try{
    const nameAr = $('#pNameAr').value.trim(), nameFr = $('#pNameFr').value.trim();
    const price = Number($('#pPrice').value||0), oldPrice = Number($('#pOldPrice').value||0), stock = Number($('#pStock').value||0);
    const descAr = $('#pDescAr').value.trim(), descFr = $('#pDescFr').value.trim(), category = $('#pCategory').value;
    const file = $('#pImageFile').files[0];
    let imageURL = '';
    if(file){
      const fref = storageRef(storage, `products/${uid('img')}_${file.name}`);
      await uploadBytes(fref, file);
      imageURL = await getDownloadURL(fref);
    }
    await addDoc(collection(db,'products'), {
      name: { ar: nameAr, fr: nameFr },
      desc: { ar: descAr, fr: descFr },
      price, oldPrice, stock, imageURL, category,
      pop: 0, createdAt: Date.now()
    });
    toast('تمت إضافة المنتج');
    // clear
    $('#pNameAr').value=''; $('#pNameFr').value=''; $('#pPrice').value=''; $('#pOldPrice').value=''; $('#pStock').value=''; $('#pDescAr').value=''; $('#pDescFr').value=''; $('#pImageFile').value='';
  } catch(err){ console.error(err); toast('فشل إضافة المنتج'); }
});

/* select product -> populate fields */
$('#productSelect').addEventListener('change', ()=>{
  const id = $('#productSelect').value; const p = products.find(x=>x.id===id); if(!p) return;
  $('#pNameAr').value = (p.name && p.name.ar) || '';
  $('#pNameFr').value = (p.name && p.name.fr) || '';
  $('#pPrice').value = p.price || '';
  $('#pOldPrice').value = p.oldPrice || '';
  $('#pStock').value = p.stock || 0;
  $('#pDescAr').value = (p.desc && p.desc.ar) || '';
  $('#pDescFr').value = (p.desc && p.desc.fr) || '';
  $('#pCategory').value = p.category || 'accessories';
});

/* update product */
$('#updateProductBtn').addEventListener('click', async ()=>{
  if(!currentUser || currentUser.email.toLowerCase() !== OWNER_EMAIL.toLowerCase()) return toast('غير مصرح');
  const id = $('#productSelect').value; if(!id) return toast('اختر منتجًا');
  try{
    const pDoc = doc(db,'products',id);
    const nameAr = $('#pNameAr').value.trim(), nameFr = $('#pNameFr').value.trim();
    const price = Number($('#pPrice').value||0), oldPrice = Number($('#pOldPrice').value||0), stock = Number($('#pStock').value||0);
    const descAr = $('#pDescAr').value.trim(), descFr = $('#pDescFr').value.trim(), category = $('#pCategory').value;
    const file = $('#pImageFile').files[0];
    let imageURL = undefined;
    if(file){
      const fref = storageRef(storage, `products/${uid('img')}_${file.name}`);
      await uploadBytes(fref, file);
      imageURL = await getDownloadURL(fref);
    }
    const updateObj = { name: { ar: nameAr, fr: nameFr }, desc: { ar: descAr, fr: descFr }, price, oldPrice, stock, category };
    if(imageURL) updateObj.imageURL = imageURL;
    await updateDoc(pDoc, updateObj);
    toast('تم التحديث');
  } catch(err){ console.error(err); toast('فشل التحديث'); }
});

/* delete product */
$('#deleteProductBtn').addEventListener('click', async ()=>{
  if(!currentUser || currentUser.email.toLowerCase() !== OWNER_EMAIL.toLowerCase()) return toast('غير مصرح');
  const id = $('#productSelect').value; if(!id) return toast('اختر منتجًا');
  if(!confirm('هل تريد حذف هذا المنتج؟')) return;
  try{ await deleteDoc(doc(db,'products',id)); toast('تم الحذف'); } catch(err){ console.error(err); toast('فشل الحذف'); }
});

/* export/import */
$('#exportBtn').addEventListener('click', async ()=>{
  try{
    const snap = await getDocs(collection(db,'products'));
    const arr = snap.docs.map(d=>({ id:d.id, ...d.data() }));
    const blob = new Blob([JSON.stringify(arr,null,2)],{type:'application/json'});
    const a = document.createElement('a'); a.href = URL.createObjectURL(blob); a.download = `products-backup-${new Date().toISOString().slice(0,10)}.json`; a.click();
  } catch(e){ console.error(e); toast('فشل التصدير'); }
});
$('#importBtn').addEventListener('click', ()=> $('#importFile').click());
$('#importFile').addEventListener('change', async e=>{
  const file = e.target.files[0]; if(!file) return; const text = await file.text();
  try{
    const arr = JSON.parse(text); if(!Array.isArray(arr)) throw new Error('invalid');
    for(const item of arr){ const data = {...item}; delete data.id; await addDoc(collection(db,'products'), data); }
    toast('تم الاستيراد');
  } catch(err){ console.error(err); toast('ملف غير صالح'); } finally { e.target.value=''; }
});

/* helper: open editor from card */
function openEditDialog(item){
  if(!currentUser || currentUser.email.toLowerCase() !== OWNER_EMAIL.toLowerCase()) return;
  $('#productSelect').value = item.id; $('#productSelect').dispatchEvent(new Event('change')); ownerDialog.showModal();
}

/* small UX */
ownerDialog.addEventListener('click', e=>{ if(e.target === ownerDialog) ownerDialog.close(); });
$('#year').textContent = new Date().getFullYear();

/* init */
renderCart(); updateCartUI();
function renderCart(){ renderCart(); } // ensure defined before use — but actual renderCart defined above; call update only
// fix: ensure cart rendering executed properly now:
renderCart = function(){ // override no-op with real
  if(!cart.length){ cartItems.innerHTML = '<div class="empty">السلة فارغة حالياً</div>'; updateCartUI(); return; }
  cartItems.innerHTML = cart.map(row => {
    const p = products.find(x=>x.id===row.id) || { name:{ar:'عنصر محذوف'}, price:0 };
    const name = (p.name && (p.name[currentLang]||p.name.ar)) || p.name;
    return `<div class="row" data-id="${row.id}">
      <div><div style="font-weight:800">${name}</div><div style="color:var(--muted)">${formatPrice(p.price)} × ${row.qty}</div></div>
      <div style="display:flex;gap:.4rem;align-items:center">
        <button class="icon-btn" data-act="dec">➖</button>
        <strong>${row.qty}</strong>
        <button class="icon-btn" data-act="inc">➕</button>
        <button class="icon-btn" data-act="del">🗑</button>
      </div>
    </div>`;
  }).join('');
  $$('#cartItems .row .icon-btn').forEach(btn=>{
    btn.addEventListener('click', ()=>{
      const rowEl = btn.closest('.row'); const id = rowEl.getAttribute('data-id'); const act = btn.getAttribute('data-act');
      const idx = cart.findIndex(x=>x.id===id); if(idx===-1) return;
      if(act==='inc') cart[idx].qty++;
      if(act==='dec') cart[idx].qty = Math.max(1, cart[idx].qty - 1);
      if(act==='del') cart.splice(idx,1);
      saveCart(); renderCart(); updateCartUI();
    });
  });
  updateCartUI();
};
// call renderCatalog to populate initial UI (products will fill via snapshot)
renderCatalog();
