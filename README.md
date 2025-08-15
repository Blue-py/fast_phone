<!doctype html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Fast Phone — متجر وصيانة</title>
<meta name="description" content="Fast Phone — متجر وصيانة هواتف. تسجيل دخول Google، لوحة مالك، رفع صور، سلة وطلب واتساب." />
<style>
  :root{--bg:#071226;--card:#0f1724;--muted:#94a3b8;--text:#e2e8f0;--accent:#06b6d4;--accent2:#22c55e}
  *{box-sizing:border-box}body{margin:0;font-family:ui-sans-serif,system-ui,-apple-system,"Segoe UI",Roboto,"Noto Kufi Arabic",Cairo,Arial;background:radial-gradient(800px 400px at 10% 0%, rgba(34,197,94,.06), transparent),var(--bg);color:var(--text);min-height:100vh}
  .container{width:min(1100px,94vw);margin:0 auto;padding:1rem}
  header{position:sticky;top:0;background:linear-gradient(180deg,rgba(2,6,23,.9),rgba(2,6,23,.7));backdrop-filter:blur(8px);padding:.8rem 0;border-bottom:1px solid rgba(148,163,184,.04);z-index:40}
  .nav{display:flex;align-items:center;justify-content:space-between;gap:1rem;width:min(1100px,94vw);margin:auto}
  .brand{display:flex;align-items:center;gap:.6rem}
  .logo{width:40px;height:40px;border-radius:10px;background:linear-gradient(135deg,var(--accent),#7dd3fc);display:grid;place-items:center;font-weight:900;color:#001018}
  .search{flex:1;display:flex;justify-content:center}
  .search input{width:min(520px,60%);padding:.6rem .9rem;border-radius:999px;border:1px solid rgba(148,163,184,.06);background:var(--card);color:var(--text)}
  .actions{display:flex;align-items:center;gap:.5rem}
  .btn{padding:.5rem .8rem;border-radius:999px;border:1px solid rgba(148,163,184,.06);background:var(--card);color:var(--text);cursor:pointer}
  .btn.primary{background:linear-gradient(135deg,var(--accent),#38bdf8);color:#001018;font-weight:700;border-color:transparent}
  main{padding:1.2rem 0}
  .hero{display:grid;grid-template-columns:1.1fr .9fr;gap:1rem;margin-bottom:1rem}
  .card{background:linear-gradient(180deg,rgba(2,6,23,.25),rgba(2,6,23,.45));padding:1rem;border-radius:12px;border:1px solid rgba(148,163,184,.04)}
  .grid{display:grid;grid-template-columns:1.2fr .8fr;gap:1rem}
  .catalog{display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:.8rem}
  .product{display:flex;flex-direction:column;border-radius:12px;overflow:hidden;background:#071226}
  .thumb{aspect-ratio:1/1;background:#041226;display:grid;place-items:center}
  .thumb img{width:100%;height:100%;object-fit:cover}
  .body{padding:.8rem;display:flex;flex-direction:column;gap:.4rem}
  .price{color:var(--accent2);font-weight:800}
  .old{color:var(--muted);text-decoration:line-through}
  .services{display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:.8rem}
  aside .card.cart{position:sticky;top:88px}
  .items{max-height:52vh;overflow:auto;padding:.6rem;display:flex;flex-direction:column;gap:.6rem}
  .row{display:flex;justify-content:space-between;align-items:center;padding:.6rem;border-radius:10px;border:1px dashed rgba(148,163,184,.04)}
  .empty{color:var(--muted);padding:1rem;text-align:center}
  dialog{border:none;border-radius:12px;padding:0}
  input,textarea,select{background:#071226;border:1px solid rgba(148,163,184,.04);color:var(--text);padding:.6rem .7rem;border-radius:8px;width:100%}
  .flex{display:flex;gap:.6rem;align-items:center}
  .icon-btn{width:36px;height:36px;border-radius:10px;border:1px solid rgba(148,163,184,.04);display:grid;place-items:center;background:#071226;cursor:pointer}
  @media (max-width:920px){.hero{grid-template-columns:1fr}.grid{grid-template-columns:1fr}}
</style>
</head>
<body>
<header>
  <div class="nav container">
    <div class="brand">
      <div class="logo">⚡</div>
      <div>
        <div style="font-weight:800">Fast Phone</div>
        <small style="color:var(--muted)">متجر وخدمات صيانة الهواتف</small>
      </div>
    </div>

    <div class="search"><input id="searchInput" placeholder="ابحث عن منتج أو خدمة…" /></div>

    <div class="actions">
      <div id="langWrap" class="flex"><button class="btn" id="langBtn">العربية</button></div>
      <button class="btn" id="loginBtn">تسجيل بـ Google</button>
      <div id="userWrap" style="display:none" class="flex">
        <img id="userAvatar" src="" alt="" style="width:34px;height:34px;border-radius:50%;border:1px solid rgba(148,163,184,.04)" />
        <div id="userName" style="padding:.15rem .6rem;border-radius:999px;background:transparent"></div>
        <button class="btn" id="logoutBtn">خروج</button>
      </div>
      <button class="btn primary" id="openCart">سلة (<span id="cartCount">0</span>)</button>
    </div>
  </div>
</header>

<main class="container">
  <section class="hero">
    <div class="card">
      <h1>مرحبًا بك في <span style="color:var(--accent)">Fast Phone</span></h1>
      <p style="color:var(--muted)">اطلب المنتجات أو الخدمات. المالك يستطيع إدارة العناصر بعد تسجيل الدخول.</p>
    </div>

    <div class="card">
      <div style="display:flex;gap:.6rem;flex-wrap:wrap">
        <button class="btn" id="openOwnerPanel">لوحة المالك</button>
        <button class="btn" id="backupBtn">نسخ احتياطي</button>
        <button class="btn" id="restoreBtn">استرجاع</button>
      </div>
      <div style="margin-top:.8rem;color:var(--muted)">المالك: <strong>ayoubkobraff@gmail.com</strong></div>
    </div>
  </section>

  <section class="grid">
    <div>
      <div style="display:flex;justify-content:space-between;align-items:center">
        <h2>المنتجات</h2>
        <div style="display:flex;gap:.5rem;align-items:center">
          <select id="sortSelect" style="padding:.5rem;border-radius:8px">
            <option value="pop">الأكثر شيوعًا</option>
            <option value="new">الأحدث</option>
            <option value="price-asc">السعر: الأقل</option>
            <option value="price-desc">السعر: الأعلى</option>
          </select>
          <button class="btn" id="filterInStock">متوفر فقط</button>
        </div>
      </div>

      <div id="catalog" class="catalog"></div>

      <h2 style="margin-top:1rem">الخدمات</h2>
      <div id="services" class="services"></div>
    </div>

    <aside>
      <div class="card cart">
        <div style="display:flex;justify-content:space-between;align-items:center;padding:.8rem;border-bottom:1px dashed rgba(148,163,184,.04)">
          <strong>سلة المشتريات</strong>
          <button class="icon-btn" id="clearCart">🗑</button>
        </div>
        <div class="items" id="cartItems"><div class="empty">السلة فارغة حالياً</div></div>
        <div style="padding:.8rem;border-top:1px dashed rgba(148,163,184,.04)">
          <div style="display:flex;justify-content:space-between;align-items:center"><span>الإجمالي</span><strong id="cartTotal">0 د.ج</strong></div>
          <div style="display:flex;gap:.5rem;margin-top:.6rem">
            <input id="couponInput" placeholder="كوبون خصم" style="padding:.5rem;border-radius:8px" />
            <button class="btn" id="applyCoupon">تطبيق</button>
            <button class="btn primary" id="checkoutBtn">طلب</button>
          </div>
          <div style="margin-top:.6rem;color:var(--muted)">ستتم عملية الطلب عبر محادثة مع المالك.</div>
        </div>
      </div>
    </aside>
  </section>

  <footer style="margin-top:1.2rem;color:var(--muted)">© <span id="year"></span> Fast Phone — كل الحقوق محفوظة.</footer>
</main>

<!-- Owner/Admin Dialog -->
<dialog id="ownerDialog">
  <div style="padding:1rem;min-width:320px">
    <div style="display:flex;justify-content:space-between;align-items:center">
      <h3>لوحة تحكم المالك</h3>
      <button class="icon-btn" id="closeOwnerDialog">✖</button>
    </div>

    <div style="margin-top:.6rem">
      <label>الاسم (عربي)</label>
      <input id="pNameAr" />
      <label>الاسم (فرنسي)</label>
      <input id="pNameFr" />
      <div style="display:grid;grid-template-columns:1fr 1fr;gap:.5rem;margin-top:.5rem">
        <div>
          <label>السعر (د.ج)</label>
          <input id="pPrice" type="number" min="0" />
        </div>
        <div>
          <label>السعر القديم (اختياري)</label>
          <input id="pOldPrice" type="number" min="0" />
        </div>
      </div>
      <label style="margin-top:.5rem">المخزون</label>
      <input id="pStock" type="number" min="0" />
      <label style="margin-top:.5rem">الوصف (عربي)</label>
      <textarea id="pDescAr"></textarea>
      <label>الوصف (فرنسي)</label>
      <textarea id="pDescFr"></textarea>
      <label>الفئة</label>
      <select id="pCategory"><option value="accessories">إكسسوارات</option><option value="spare">قطع غيار</option><option value="phones">هواتف</option></select>
      <label style="margin-top:.5rem">صورة المنتج (رفع)</label>
      <input id="pImageFile" type="file" accept="image/*" />
      <div style="display:flex;gap:.5rem;margin-top:.6rem">
        <button class="btn primary" id="addProductBtn">إضافة</button>
        <button class="btn" id="updateProductBtn">تعديل</button>
        <button class="btn" id="deleteProductBtn">حذف</button>
      </div>

      <hr style="margin:.8rem 0;border:none;border-top:1px dashed rgba(148,163,184,.04)" />

      <h4>قوائم المنتجات</h4>
      <select id="productSelect" style="width:100%;padding:.5rem;margin-top:.4rem"></select>
      <div style="display:flex;gap:.5rem;margin-top:.6rem">
        <button class="btn" id="exportBtn">تصدير JSON</button>
        <input type="file" id="importFile" accept="application/json" style="display:none" />
        <button class="btn" id="importBtn">استيراد JSON</button>
      </div>
    </div>
  </div>
</dialog>

<!-- Firebase modules (ESM) -->
<script type="module">
  // ------ Firebase config (مؤمن منك مسبقًا؛ مع تصحيح storageBucket) -------
  const firebaseConfig = {
    apiKey: "AIzaSyB5dqUC2YubUVMuWP8_wLznve0Tx8TB_rM",
    authDomain: "fast-phone-7b145.firebaseapp.com",
    projectId: "fast-phone-7b145",
    storageBucket: "fast-phone-7b145.appspot.com",
    messagingSenderId: "614637173695",
    appId: "1:614637173695:web:7249c266d38d41b3b97f0a",
    measurementId: "G-KJZWYEEBVD"
  };

  // Import modular SDK from CDN
  import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";
  import { getAuth, GoogleAuthProvider, signInWithPopup, signOut, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";
  import { getFirestore, collection, addDoc, doc, setDoc, getDocs, onSnapshot, deleteDoc, updateDoc, query, orderBy } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";
  import { getStorage, ref as storageRef, uploadBytes, getDownloadURL } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-storage.js";

  const app = initializeApp(firebaseConfig);
  const auth = getAuth(app);
  const provider = new GoogleAuthProvider();
  const db = getFirestore(app);
  const storage = getStorage(app);

  // Expose a simple interface for the rest of the page
  window.FB = { auth, provider, db, storage, signInWithPopup, signOut, onAuthStateChanged, collection, addDoc, doc, setDoc, getDocs, onSnapshot, deleteDoc, updateDoc, query, orderBy, storageRef, uploadBytes, getDownloadURL };

  // ================== App logic (UI wiring) ==================
  (function(){
    // Helpers
    const $ = (s,ctx=document)=>ctx.querySelector(s);
    const $$ = (s,ctx=document)=>Array.from(ctx.querySelectorAll(s));
    const OWNER_EMAIL = 'ayoubkobraff@gmail.com';
    const LS_KEYS = { CART: 'ff_cart' };
    const CURRENCY = 'د.ج';

    function uid(pref='id'){ return pref + '_' + Math.random().toString(36).slice(2,9); }
    function toast(t){ const el=document.createElement('div'); el.textContent=t; Object.assign(el.style,{position:'fixed',right:'16px',bottom:'16px',background:'#0b1324',color:'#e2e8f0',padding:'.6rem .9rem',borderRadius:'10px',border:'1px solid rgba(148,163,184,.06)',zIndex:9999}); document.body.appendChild(el); setTimeout(()=>el.remove(),2200); }
    function formatPrice(n){ return `${Number(n||0).toLocaleString('ar-DZ')} ${CURRENCY}`; }

    // State
    let currentUser = null;
    let products = []; // local cache; real-time via onSnapshot
    let cart = JSON.parse(localStorage.getItem(LS_KEYS.CART) || '[]');
    let appliedCoupon = null;

    // UI elements
    const loginBtn = $('#loginBtn'); const logoutBtn = $('#logoutBtn'); const userWrap = $('#userWrap'); const userName = $('#userName'); const userAvatar = $('#userAvatar');
    const catalog = $('#catalog'); const servicesWrap = $('#services');
    const cartItems = $('#cartItems'); const cartCount = $('#cartCount'); const cartTotal = $('#cartTotal');

    // Auth flows
    loginBtn.addEventListener('click', async ()=>{
      try{
        await signInWithPopup(auth, provider);
        // onAuthStateChanged handler will run
      }catch(err){ console.error(err); toast('خطأ في تسجيل الدخول'); }
    });
    logoutBtn.addEventListener('click', async ()=>{ try{ await signOut(auth); }catch(e){ console.error(e); toast('خطأ في تسجيل الخروج'); } });

    onAuthStateChanged(auth, user=>{
      if(user){
        currentUser = user;
        loginBtn.style.display='none';
        userWrap.style.display='flex';
        logoutBtn.style.display='inline-block';
        userName.textContent = user.displayName || user.email;
        userAvatar.src = user.photoURL || ('https://i.pravatar.cc/64?u=' + encodeURIComponent(user.email));
        // show/hide owner UI
        if(user.email && user.email.toLowerCase() === OWNER_EMAIL.toLowerCase()){
          $('#ownerDialog'); // exists
        }
      } else {
        currentUser = null;
        loginBtn.style.display='inline-block';
        userWrap.style.display='none';
        logoutBtn.style.display='none';
      }
      renderOwnerPanelVisibility();
    });

    // Owner panel show/hide
    function renderOwnerPanelVisibility(){
      // openOwnerPanel button will check isOwner on click
    }

    // Real-time products listener
    const productsCol = collection(db,'products');
    // order by createdAt desc for display
    const qProducts = query(productsCol, orderBy('createdAt','desc'));
    onSnapshot(qProducts, snap=>{
      products = []; snap.forEach(d=>products.push({ id:d.id, ...d.data() }));
      renderCatalog();
      populateProductSelect();
    });

    // Render product card (multi-lang fields stored as {ar,fr})
    let currentLang = localStorage.getItem('ff_lang') || 'ar';
    $('#langBtn').textContent = currentLang === 'ar' ? 'العربية' : 'Français';
    $('#langBtn').addEventListener('click', ()=>{
      currentLang = currentLang === 'ar' ? 'fr' : 'ar';
      localStorage.setItem('ff_lang', currentLang);
      $('#langBtn').textContent = currentLang === 'ar' ? 'العربية' : 'Français';
      renderCatalog();
    });

    function productCard(p){
      const name = (p.name && (p.name[currentLang] || p.name.ar)) || (p.name || '—');
      const desc = (p.desc && (p.desc[currentLang] || p.desc.ar)) || '';
      const out = `
      <article class="product card" data-id="${p.id}">
        <div class="thumb">${p.imageURL? `<img src="${p.imageURL}" alt="${name}" />` : '<div style="padding:1rem;color:var(--muted)">لا صورة</div>'}</div>
        <div class="body">
          <div style="display:flex;justify-content:space-between;align-items:center">
            <div style="font-weight:800">${name}</div>
            <div><span class="price">${formatPrice(p.price)}</span> ${p.oldPrice? `<span class="old">${formatPrice(p.oldPrice)}</span>`: ''}</div>
          </div>
          <div style="color:var(--muted);font-size:.95rem;margin-top:.4rem">${desc}</div>
          <div style="display:flex;gap:.4rem;margin-top:.6rem">
            <button class="btn" data-act="add">إضافة للسلة</button>
            <button class="btn primary" data-act="buy">طلب</button>
            ${currentUser && currentUser.email && currentUser.email.toLowerCase() === 'ayoubkobraff@gmail.com' ? `<button class="btn" data-act="edit">تعديل</button>` : ''}
          </div>
        </div>
      </article>`;
      return out;
    }

    function renderCatalog(){
      const q = $('#searchInput').value.trim().toLowerCase();
      const inStockOnly = $('#filterInStock').classList.contains('active');
      let list = [...products];
      if(q) list = list.filter(p => ((p.name && (p.name.ar + ' ' + (p.name.fr||'')).toLowerCase()) || '').includes(q) || (p.desc && (p.desc.ar + (p.desc.fr||'')).toLowerCase().includes(q)));
      if(inStockOnly) list = list.filter(p => (p.stock || 0) > 0);
      const sort = $('#sortSelect').value;
      if(sort === 'price-asc') list.sort((a,b)=> (a.price||0) - (b.price||0));
      if(sort === 'price-desc') list.sort((a,b)=> (b.price||0) - (a.price||0));
      if(sort === 'new') list.sort((a,b)=> (b.createdAt||0) - (a.createdAt||0));
      if(sort === 'pop') list.sort((a,b)=> (b.pop||0) - (a.pop||0));

      catalog.innerHTML = list.map(productCard).join('') || '<div class="empty">لا يوجد منتجات</div>';

      // bind buttons
      $$('#catalog .product').forEach(card=>{
        const id = card.getAttribute('data-id');
        const item = products.find(x=>x.id===id);
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
    }

    // Cart functions
    function saveCart(){ localStorage.setItem(LS_KEYS.CART, JSON.stringify(cart)); }
    function updateCartUI(){
      cartCount.textContent = cart.reduce((s,r)=>s+r.qty,0);
      const { total } = calcCartTotal();
      cartTotal.textContent = formatPrice(total);
    }
    function renderCart(){
      if(!cart.length){ cartItems.innerHTML = '<div class="empty">السلة فارغة حالياً</div>'; updateCartUI(); return; }
      cartItems.innerHTML = cart.map(row=>{
        const p = products.find(x=>x.id===row.id) || { name: { ar: 'عنصر محذوف' }, price: 0 };
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
      // bind
      $$('#cartItems .row .icon-btn').forEach(btn=>{
        btn.addEventListener('click', ()=>{
          const rowEl = btn.closest('.row'); const id = rowEl.getAttribute('data-id'); const act = btn.getAttribute('data-act');
          const idx = cart.findIndex(x=>x.id===id); if(idx===-1) return;
          if(act==='inc') cart[idx].qty++;
          if(act==='dec') cart[idx].qty = Math.max(1, cart[idx].qty -1);
          if(act==='del') cart.splice(idx,1);
          saveCart(); renderCart(); updateCartUI();
        });
      });
      updateCartUI();
    }

    function addToCart(id,qty=1){
      const p = products.find(x=>x.id===id); if(!p) return toast('منتج غير موجود');
      if((p.stock||0) <= 0) return toast('غير متوفر');
      const row = cart.find(x=>x.id===id);
      if(row) row.qty += qty; else cart.push({ id, qty });
      saveCart(); renderCart(); toast('أضيف إلى السلة');
    }

    function calcCartTotal(){
      let total = 0;
      cart.forEach(r=>{ const p = products.find(x=>x.id===r.id); if(p) total += (p.price||0) * r.qty; });
      return { total, discount:0, grand: total };
    }

    $('#clearCart').addEventListener('click', ()=>{ cart=[]; saveCart(); renderCart(); updateCartUI(); });

    $('#checkoutBtn').addEventListener('click', openCheckout);
    function openCheckout(){
      if(!cart.length) return toast('السلة فارغة');
      const { total } = calcCartTotal();
      const lines = cart.map(r=>{ const p = products.find(x=>x.id===r.id); const name=(p.name && (p.name[currentLang]||p.name.ar))||p.name; return `• ${name} × ${r.qty} = ${formatPrice((p.price||0)*r.qty)}`; }).join('\n');
      const msg = `طلب جديد من Fast Phone\n\n${lines}\n\nالمجموع: ${formatPrice(total)}\n\nمن فضلك أكدوا التوفر والموعد.`;
      const phone = '213657340489';
      window.open(`https://wa.me/${phone}?text=${encodeURIComponent(msg)}`, '_blank');
    }

    // Search & filters
    $('#searchInput').addEventListener('input', ()=> renderCatalog());
    $('#sortSelect').addEventListener('change', ()=> renderCatalog());
    $('#filterInStock').addEventListener('click', e=> { e.currentTarget.classList.toggle('active'); renderCatalog(); });

    // Owner panel interactions
    const ownerDialog = $('#ownerDialog');
    $('#openOwnerPanel').addEventListener('click', ()=>{
      if(!currentUser || (currentUser.email && currentUser.email.toLowerCase() !== 'ayoubkobraff@gmail.com')) return toast('هذه الميزة للمالك فقط');
      populateProductSelect();
      ownerDialog.showModal();
    });
    $('#closeOwnerDialog').addEventListener('click', ()=> ownerDialog.close());

    function populateProductSelect(){
      const sel = $('#productSelect');
      sel.innerHTML = products.map(p=>`<option value="${p.id}">${(p.name && (p.name.ar||'')) || p.name}</option>`).join('');
    }

    // Add product (upload image to Storage then save to Firestore)
    $('#addProductBtn').addEventListener('click', async ()=>{
      if(!currentUser || currentUser.email.toLowerCase() !== 'ayoubkobraff@gmail.com') return toast('غير مصرح');
      const nameAr = $('#pNameAr').value.trim(); const nameFr = $('#pNameFr').value.trim();
      const price = Number($('#pPrice').value||0); const oldPrice = Number($('#pOldPrice').value||0); const stock = Number($('#pStock').value||0);
      const descAr = $('#pDescAr').value.trim(); const descFr = $('#pDescFr').value.trim(); const category = $('#pCategory').value;
      const file = $('#pImageFile').files[0];
      let imageURL = '';
      try{
        if(file){
          const fref = storageRef(storage, `products/${uid('img')}_${file.name}`);
          await uploadBytes(fref, file);
          imageURL = await getDownloadURL(fref);
        }
        const docRef = await addDoc(collection(db,'products'), {
          name: { ar: nameAr, fr: nameFr },
          desc: { ar: descAr, fr: descFr },
          price, oldPrice, stock, imageURL, category,
          pop: 0, createdAt: Date.now()
        });
        toast('تمت إضافة المنتج');
        // clear fields
        $('#pNameAr').value=''; $('#pNameFr').value=''; $('#pPrice').value=''; $('#pOldPrice').value=''; $('#pStock').value=''; $('#pDescAr').value=''; $('#pDescFr').value=''; $('#pImageFile').value='';
        // product will appear via onSnapshot
      }catch(e){ console.error(e); toast('فشل إضافة المنتج'); }
    });

    // Update product: load selected product into fields then update
    $('#productSelect').addEventListener('change', ()=>{
      const id = $('#productSelect').value;
      const p = products.find(x=>x.id === id); if(!p) return;
      $('#pNameAr').value = (p.name && p.name.ar) || '';
      $('#pNameFr').value = (p.name && p.name.fr) || '';
      $('#pPrice').value = p.price || '';
      $('#pOldPrice').value = p.oldPrice || '';
      $('#pStock').value = p.stock || 0;
      $('#pDescAr').value = (p.desc && p.desc.ar) || '';
      $('#pDescFr').value = (p.desc && p.desc.fr) || '';
      $('#pCategory').value = p.category || 'accessories';
    });

    $('#updateProductBtn').addEventListener('click', async ()=>{
      if(!currentUser || currentUser.email.toLowerCase() !== 'ayoubkobraff@gmail.com') return toast('غير مصرح');
      const id = $('#productSelect').value; if(!id) return toast('اختر منتجًا');
      const pDoc = doc(db,'products',id);
      const nameAr = $('#pNameAr').value.trim(); const nameFr = $('#pNameFr').value.trim();
      const price = Number($('#pPrice').value||0); const oldPrice = Number($('#pOldPrice').value||0); const stock = Number($('#pStock').value||0);
      const descAr = $('#pDescAr').value.trim(); const descFr = $('#pDescFr').value.trim(); const category = $('#pCategory').value;
      const file = $('#pImageFile').files[0];
      try{
        let imageURL = undefined;
        if(file){
          const fref = storageRef(storage, `products/${uid('img')}_${file.name}`);
          await uploadBytes(fref, file);
          imageURL = await getDownloadURL(fref);
        }
        const updateObj = {
          name: { ar: nameAr, fr: nameFr },
          desc: { ar: descAr, fr: descFr },
          price, oldPrice, stock, category
        };
        if(imageURL) updateObj.imageURL = imageURL;
        await updateDoc(pDoc, updateObj);
        toast('تم التحديث');
      }catch(e){ console.error(e); toast('فشل التحديث'); }
    });

    $('#deleteProductBtn').addEventListener('click', async ()=>{
      if(!currentUser || currentUser.email.toLowerCase() !== 'ayoubkobraff@gmail.com') return toast('غير مصرح');
      const id = $('#productSelect').value; if(!id) return toast('اختر منتجًا');
      if(!confirm('هل تريد حذف هذا المنتج؟')) return;
      try{ await deleteDoc(doc(db,'products',id)); toast('تم الحذف'); }catch(e){ console.error(e); toast('فشل الحذف'); }
    });

    // Export/import (backup/restore)
    $('#exportBtn').addEventListener('click', async ()=>{
      const snap = await getDocs(collection(db,'products'));
      const arr = snap.docs.map(d=>({ id:d.id, ...d.data() }));
      const blob = new Blob([JSON.stringify(arr,null,2)],{type:'application/json'});
      const a=document.createElement('a'); a.href=URL.createObjectURL(blob); a.download=`products-backup-${new Date().toISOString().slice(0,10)}.json`; a.click();
    });
    $('#importBtn').addEventListener('click', ()=> $('#importFile').click());
    $('#importFile').addEventListener('change', async e=>{
      const file = e.target.files[0]; if(!file) return;
      const text = await file.text();
      try{
        const arr = JSON.parse(text);
        if(!Array.isArray(arr)) throw new Error('invalid');
        for(const item of arr){
          const data = { ...item }; delete data.id;
          await addDoc(collection(db,'products'), data);
        }
        toast('تم الاستيراد');
      }catch(err){ console.error(err); toast('ملف غير صالح'); } finally { e.target.value=''; }
    });

    // Helper to open editor via edit button on product card
    function openEditDialog(item){
      if(!currentUser || currentUser.email.toLowerCase() !== 'ayoubkobraff@gmail.com') return;
      $('#productSelect').value = item.id; $('#productSelect').dispatchEvent(new Event('change')); ownerDialog.showModal();
    }

    // Init UI
    $('#year').textContent = new Date().getFullYear();
    // initial render cart from storage
    renderCart();
    updateCartUI();

    // small UX: clicking outside dialog closes it
    ownerDialog.addEventListener('click', (e)=>{ if(e.target === ownerDialog) ownerDialog.close(); });

  })();
</script>
</body>
</html>
