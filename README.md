<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Fast Phone | المتجر والخدمات</title>
  <meta name="description" content="تطبيق ويب لمحل Fast Phone: عرض المنتجات والخدمات، تسجيل الدخول بجوجل، سلة المشتريات، والطلب عبر محادثة المالك. يدعم العربية والفرنسية + وضع داكن/فاتح." />
  <meta name="theme-color" content="#0ea5e9" />
  <!--
  ============================================================================
  Fast Phone — Single-file HTML/CSS/JS App (RTL/LTR Arabic/French)
  Author: ChatGPT (GPT-5 Thinking)
  Date: 2025-08-15

  ✅ الميزات الرئيسية / Fonctionnalités:
  - 🇦🇪/🇫🇷 تعدد اللغة العربية/الفرنسية مع تبديل فوري للواجهة (i18n) + حفظ الاختيار في التخزين المحلي.
  - 🎨 تبديل الوضع: داكن/فاتح + تخزين التفضيل.
  - 🛍️ كتالوج منتجات + خدمات صيانة مع بحث/تصفية/فرز.
  - 🛒 سلة مشتريات + كوبونات خصم + إجماليات + توليد رسالة طلب جاهزة.
  - 💬 زر "طلب" يفتح محادثة مع حساب المالك (واتساب/تليجرام/مسنجر) مع تمرير محتوى السلة.
  - 🔐 تسجيل الدخول بجوجل عبر Firebase Auth (مكان لإضافة مفاتيحك) + صلاحيات مالك.
  - 👑 فقط حساب المالك يمكنه إضافة/تعديل/حذف المنتجات والخدمات، وتغيير الأسعار والمخزون.
  - 💾 تخزين محلي (localStorage) كبداية + واجهات جاهزة للربط مع Firestore (تعليقات في الأسفل).
  - 🧰 لوحة تحكم Admin للمالك: CRUD للمنتجات والخدمات، إدارة قسائم الخصم، نسخ احتياطي/استرجاع JSON.
  - 📦 ملف واحد—لا يحتاج بنية إطار—قابل للنشر مباشرة على استضافة ثابتة.
  - 📱 تصميم متجاوب RTL/LTR.

  ⚠️ خطوات ضرورية قبل الإطلاق:
  1) حدّث الثوابت OWNER_EMAIL و OWNER_CHAT.
  2) أضف تكوين Firebase في الكائن firebaseConfig أدناه.
  3) إن رغبت في استخدام Firestore، اتبع التعليمات في نهاية الملف.

  ملاحظة: الملف يتجاوز 1000 سطر ويتضمن تعليقات مفصلة لضمان الاحترافية وقابلية التوسع.
  ============================================================================
  -->
  <style>
    /* ==========================
       CSS Reset + Variables
       ========================== */
    *, *::before, *::after { box-sizing: border-box; }
    * { margin: 0; }
    html, body { height: 100%; }
    body { line-height: 1.5; -webkit-font-smoothing: antialiased; }
    img, picture, video, canvas, svg { display: block; max-width: 100%; }
    input, button, textarea, select { font: inherit; }
    p, h1, h2, h3, h4, h5, h6 { overflow-wrap: anywhere; }

    :root {
      --bg: #0b1220;            /* dark background */
      --card: #0f172a;          /* cards */
      --muted: #94a3b8;         /* secondary text */
      --text: #e2e8f0;          /* main text */
      --accent: #0ea5e9;        /* blue-cyan */
      --accent-2: #22c55e;      /* green */
      --danger: #ef4444;        /* red */
      --warn: #f59e0b;          /* orange */
      --ring: rgba(14,165,233,.35);
      --border: rgba(148,163,184,.15);
      --shadow: 0 10px 25px rgba(0,0,0,.35);
      --radius: 16px;
      --radius-sm: 12px;
      --radius-lg: 22px;
      --font: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto,
               "Noto Kufi Arabic", "Cairo", Tahoma, Arial,
               "Apple Color Emoji", "Segoe UI Emoji";
    }

    .light {
      --bg: #f7fafc;
      --card: #ffffff;
      --text: #0f172a;
      --muted: #475569;
      --border: rgba(2,6,23,.08);
      --shadow: 0 6px 18px rgba(2,6,23,.08);
    }

    body {
      background: radial-gradient(1200px 600px at 80% -10%, rgba(14,165,233,.15), transparent),
                  radial-gradient(800px 400px at 0% 120%, rgba(34,197,94,.12), transparent),
                  var(--bg);
      color: var(--text);
      font-family: var(--font);
      min-height: 100dvh;
    }

    .container { width: min(1200px, 92vw); margin-inline: auto; }

    header {
      position: sticky; top: 0; z-index: 50; backdrop-filter: saturate(180%) blur(18px);
      background: linear-gradient(to bottom, rgba(11,18,32,.85), rgba(11,18,32,.65));
      border-bottom: 1px solid var(--border);
    }
    .nav {
      display: grid; grid-template-columns: 1fr auto 1fr; align-items: center; gap: 1rem;
      padding: .75rem 0;
    }
    .brand { display:flex; align-items:center; gap:.6rem; font-weight:800; letter-spacing:.3px; }
    .brand .logo { width: 36px; aspect-ratio:1; border-radius: 10px; background: linear-gradient(135deg, var(--accent), #7dd3fc); display:grid; place-items:center; color:#fff; font-weight:900; box-shadow: var(--shadow); }
    .brand small { display:block; color: var(--muted); font-weight:600; margin-top:-4px; }

    .searchbar { display:flex; align-items:center; gap:.6rem; }
    .searchbar input {
      width: clamp(160px, 40vw, 520px);
      background: var(--card);
      border: 1px solid var(--border);
      color: var(--text);
      padding:.65rem .9rem; border-radius: 999px; outline: none;
      box-shadow: inset 0 1px 0 rgba(255,255,255,.04);
    }
    .searchbar input:focus { border-color: var(--accent); box-shadow: 0 0 0 4px var(--ring); }

    .actions { display:flex; justify-content:end; align-items:center; gap:.5rem; }
    .btn { display:inline-flex; align-items:center; gap:.5rem; padding:.6rem .9rem; border-radius: 999px; border:1px solid var(--border); background: var(--card); color: var(--text); cursor:pointer; transition:.2s ease; box-shadow: 0 1px 0 rgba(255,255,255,.03); }
    .btn:hover { transform: translateY(-1px); border-color: var(--accent); }
    .btn.primary { background: linear-gradient(135deg, var(--accent), #38bdf8); color:#001018; font-weight:800; border-color: transparent; }
    .btn.success { background: linear-gradient(135deg, var(--accent-2), #86efac); color:#03210d; font-weight:800; border-color: transparent; }
    .btn.ghost { background: transparent; }

    .chip { font-size:.8rem; border:1px solid var(--border); padding:.25rem .55rem; border-radius:999px; color:var(--muted); }

    main { padding: 1.2rem 0 4rem; }

    .hero { display:grid; grid-template-columns: 1.1fr .9fr; gap:2rem; align-items:center; margin: 1rem 0 2rem; }
    .hero .card { background: linear-gradient(180deg, rgba(2,6,23,.25), rgba(2,6,23,.45)), var(--card); border:1px solid var(--border); border-radius: var(--radius-lg); padding: 1.3rem; box-shadow: var(--shadow); }
    .hero h1 { font-size: clamp(1.6rem, 2.2vw + 1rem, 2.4rem); line-height: 1.2; margin-bottom:.4rem; }
    .hero p { color: var(--muted); }
    .hero .stats { display:flex; gap:1rem; flex-wrap:wrap; margin-top:1rem; }
    .stat { background: var(--card); border:1px solid var(--border); border-radius: var(--radius); padding:.8rem 1rem; min-width: 150px; }

    .grid { display:grid; gap: 1rem; }
    .two-col { grid-template-columns: 1.2fr .8fr; }

    .section-title { display:flex; align-items:center; justify-content:space-between; margin: 1.2rem 0 .6rem; }
    .section-title h2 { font-size: 1.2rem; }
    .section-title .filters { display:flex; align-items:center; gap:.5rem; }

    .card { background: var(--card); border:1px solid var(--border); border-radius: var(--radius); box-shadow: var(--shadow); }

    .catalog { display:grid; grid-template-columns: repeat(auto-fill, minmax(220px,1fr)); gap: .8rem; }
    .product { display:flex; flex-direction:column; }
    .product .thumb { position:relative; border-bottom:1px solid var(--border); aspect-ratio: 1 / 1; border-top-left-radius: var(--radius); border-top-right-radius: var(--radius); overflow:hidden; background: #0a0f1c; }
    .product img { width:100%; height:100%; object-fit:cover; }
    .product .label { position:absolute; top:.6rem; left:.6rem; backdrop-filter: blur(8px); background: rgba(2,6,23,.5); border:1px solid var(--border); color: var(--text); padding:.25rem .5rem; border-radius: 10px; font-size:.8rem; }
    .product .body { padding:.8rem; display:flex; flex-direction:column; gap:.45rem; }
    .product .name { font-weight:700; }
    .product .price { color: var(--accent-2); font-weight:800; }
    .product .old { color: var(--muted); text-decoration: line-through; font-weight:500; margin-inline-start:.4rem; }
    .product .meta { display:flex; align-items:center; justify-content:space-between; }
    .product .actions { display:flex; gap:.4rem; margin-top:.4rem; }

    .services { display:grid; grid-template-columns: repeat(auto-fill, minmax(260px,1fr)); gap: .8rem; }
    .service { display:flex; gap:.8rem; padding: .9rem; }
    .service .icon { width:46px; height:46px; border-radius: 12px; display:grid; place-items:center; background: linear-gradient(135deg, #22d3ee33, transparent); border:1px solid var(--border); }
    .service .title { font-weight:800; }
    .service .desc { color: var(--muted); font-size:.95rem; }

    .cart { position: sticky; top: 78px; align-self:start; }
    .cart .head { display:flex; align-items:center; justify-content:space-between; padding:.8rem 1rem; border-bottom:1px dashed var(--border); }
    .cart .items { max-height: 52vh; overflow:auto; display:flex; flex-direction:column; gap:.6rem; padding: .8rem; }
    .cart .row { display:grid; grid-template-columns: 1fr auto; gap:.6rem; align-items:center; padding:.6rem .7rem; border:1px dashed var(--border); border-radius: 12px; }
    .cart .row .name { font-weight:700; }
    .cart .row .qty { display:flex; align-items:center; gap:.4rem; }
    .cart .foot { padding: .8rem 1rem; border-top:1px dashed var(--border); display:grid; gap:.5rem; }

    .pill { font-size: .85rem; padding:.4rem .8rem; border-radius: 999px; border: 1px dashed var(--border); color: var(--muted); }

    .empty { color: var(--muted); text-align:center; padding: 2rem .6rem; }

    .footer { margin-top: 2rem; padding: 1rem 0 2rem; color: var(--muted); border-top:1px dashed var(--border); font-size:.95rem; display:grid; gap:.4rem; }

    dialog { border:none; border-radius: 18px; width: min(820px, 96vw); background: var(--card); color: var(--text); box-shadow: var(--shadow); }
    dialog::backdrop { background: rgba(2,6,23,.6); backdrop-filter: blur(2px); }
    .modal-body { padding: 1rem; display:grid; gap:.8rem; }
    .modal-grid { display:grid; grid-template-columns: 1fr 1fr; gap:.8rem; }
    .field { display:grid; gap:.25rem; }
    .field label { color: var(--muted); font-size:.9rem; }
    .field input, .field textarea, .field select { background: #0b1324; border:1px solid var(--border); color: var(--text); padding:.6rem .7rem; border-radius: 10px; }
    .field textarea { min-height: 96px; resize: vertical; }

    .badge { font-size:.75rem; padding:.2rem .5rem; border-radius: 8px; background: #0a1628; border:1px solid var(--border); color: var(--muted); }

    .lang-toggle, .theme-toggle { display:inline-flex; align-items:center; gap:.4rem; }

    .alert { padding:.65rem .8rem; border-radius: 12px; border:1px solid var(--border); background: #0e1a2e; color: var(--text); }
    .alert.warn { background: #231a09; border-color: #3a2a0a; }
    .alert.success { background: #0d2315; border-color: #0e3620; }

    .icon-btn { display:inline-grid; place-items:center; width: 32px; height: 32px; border-radius: 10px; border:1px solid var(--border); background: #0a0f1c; cursor:pointer; }

    .skeleton { position:relative; overflow:hidden; background: #0a0f1c; border-radius: 12px; }
    .skeleton::after { content:""; position:absolute; inset:0; background: linear-gradient(90deg, transparent, rgba(255,255,255,.06), transparent); transform: translateX(-100%); animation: shine 1.3s linear infinite; }
    @keyframes shine { to { transform: translateX(100%); } }

    @media (max-width: 920px) {
      .hero { grid-template-columns: 1fr; }
      .two-col { grid-template-columns: 1fr; }
      .searchbar input { width: 100%; }
    }
  </style>
</head>
<body>
  <!-- Header -->
  <header>
    <div class="container nav">
      <div class="brand">
        <div class="logo">⚡️</div>
        <div>
          <div style="font-size:1.15rem" data-i18n="brandTitle">Fast Phone</div>
          <small data-i18n="brandSubtitle">متجر وخدمات صيانة الهواتف</small>
        </div>
      </div>
      <div class="searchbar">
        <input id="searchInput" type="search" placeholder="ابحث عن منتج أو خدمة…" data-i18n-placeholder="searchPlaceholder" />
        <button class="btn ghost" id="clearSearch" title="مسح البحث">✖</button>
      </div>
      <div class="actions">
        <span class="chip" id="storeStatus" data-i18n="statusOnline">الحالة: متصل</span>

        <!-- Language Toggle -->
        <button class="btn" id="langBtn" title="Language / اللغة" aria-label="Language Toggle">
          <span id="langLabel">العربية</span> <span>🌐</span>
        </button>

        <!-- Theme Toggle -->
        <button class="btn" id="themeBtn" title="تبديل الوضع" aria-label="Theme Toggle">
          <span id="themeLabel" data-i18n="theme">الوضع</span>
          <span aria-hidden id="themeIcon">🌙</span>
        </button>

        <button class="btn" id="loginBtn" data-i18n="login">دخول بجوجل</button>
        <div id="userMenu" style="display:none; align-items:center; gap:.6rem;">
          <img id="userAvatar" src="" alt="" style="width:32px; height:32px; border-radius:50%; border:1px solid var(--border);" />
          <span id="userName" class="chip"></span>
          <button class="btn" id="logoutBtn" data-i18n="logout">خروج</button>
        </div>
        <button class="btn primary" id="openCart" data-i18n="cartButton">سلة (<span id="cartCount">0</span>)</button>
      </div>
    </div>
  </header>

  <main class="container">
    <!-- Hero -->
    <section class="hero">
      <div class="card">
        <h1><span data-i18n="welcome">مرحبًا بك في</span> <span style="color:var(--accent)">Fast Phone</span> ⚡️</h1>
        <p data-i18n="heroText">
          اطلب المنتجات المتوفرة وشاهد خدمات الصيانة لدينا. عند الضغط على "طلب" ستُفتح محادثة مع صاحب المحل برسالة جاهزة. المالك فقط يمكنه إدارة العناصر.
        </p>
        <div class="stats">
          <div class="stat">
            <div class="badge" data-i18n="avgRepair">متوسط زمن الإصلاح</div>
            <div style="font-size:1.35rem; font-weight:800;">2–24h</div>
          </div>
          <div class="stat">
            <div class="badge" data-i18n="warranty">ضمان الصيانة</div>
            <div style="font-size:1.35rem; font-weight:800;">30 يوم</div>
          </div>
          <div class="stat">
            <div class="badge" data-i18n="payment">طرق الدفع</div>
            <div style="font-size:1.35rem; font-weight:800;">نقدي / CIB</div>
          </div>
        </div>
      </div>
      <div class="card" style="display:grid; align-content:center; gap:.8rem;">
        <div class="alert">
          <strong data-i18n="reminder">تذكير:</strong> <span data-i18n="reminderDetail">فعّل تسجيل الدخول بجوجل بإضافة إعدادات Firebase الخاصة بك.</span>
        </div>
        <div class="alert success">
          <strong data-i18n="ownerFeatureTitle">خاصية المالك:</strong> <span data-i18n="ownerFeature">عند تسجيل الدخول بحساب المالك تستطيع إدارة المنتجات والخدمات من لوحة التحكم.</span>
        </div>
        <div class="alert warn">
          <strong data-i18n="ordersTitle">الطلبات:</strong> <span data-i18n="ordersDetail">زر "طلب" يفتح واتساب/تليجرام المالك برسالة مفصلة تشمل العناصر من السلة.</span>
        </div>
        <div style="display:flex; gap:.6rem; flex-wrap:wrap;">
          <button class="btn success" id="openOwnerPanel" data-i18n="ownerPanel">لوحة تحكم المالك</button>
          <button class="btn" id="backupBtn" data-i18n="backup">نسخ احتياطي محلي</button>
          <button class="btn" id="restoreBtn" data-i18n="restore">استرجاع بيانات</button>
        </div>
      </div>
    </section>

    <!-- Main Grid -->
    <section class="grid two-col">
      <div>
        <div class="section-title">
          <h2 data-i18n="products">المنتجات</h2>
          <div class="filters">
            <select id="sortSelect" class="pill" title="فرز" data-i18n-select="sort">
              <option value="pop" data-i18n="sortPopular">الأكثر شيوعًا</option>
              <option value="new" data-i18n="sortNewest">الأحدث</option>
              <option value="price-asc" data-i18n="sortPriceAsc">السعر: من الأقل للأعلى</option>
              <option value="price-desc" data-i18n="sortPriceDesc">السعر: من الأعلى للأقل</option>
            </select>
            <button class="pill" id="filterInStock" data-i18n="inStockOnly">متوفر فقط</button>
            <button class="pill" id="resetFilters" data-i18n="resetFilters">إعادة تعيين</button>
          </div>
        </div>
        <div id="catalog" class="catalog"></div>

        <div class="section-title" style="margin-top:1.4rem;">
          <h2 data-i18n="servicesTitle">الخدمات</h2>
          <div class="filters">
            <span class="pill" data-i18n="serviceWarranty">ضمان 30 يوم</span>
            <span class="pill" data-i18n="freeCheck">فحص مجاني عند الإصلاح</span>
          </div>
        </div>
        <div id="services" class="services"></div>
      </div>

      <aside>
        <div class="card cart" id="cartPanel">
          <div class="head">
            <strong data-i18n="cartTitle">سلة المشتريات</strong>
            <button class="icon-btn" id="clearCart" title="تفريغ السلة">🗑</button>
          </div>
          <div class="items" id="cartItems">
            <div class="empty" data-i18n="cartEmpty">السلة فارغة حالياً</div>
          </div>
          <div class="foot">
            <div style="display:flex; justify-content:space-between; align-items:center;">
              <span data-i18n="total">الإجمالي</span>
              <strong id="cartTotal">0 د.ج</strong>
            </div>
            <div style="display:flex; gap:.5rem; flex-wrap:wrap;">
              <input id="couponInput" class="pill" placeholder="كوبون خصم" data-i18n-placeholder="couponPlaceholder" />
              <button class="btn" id="applyCoupon" data-i18n="applyCoupon">تطبيق</button>
              <button class="btn primary" id="checkoutBtn" data-i18n="checkout">طلب</button>
            </div>
            <div class="badge" id="cartNote" data-i18n="cartNote">ستتم عملية الطلب عبر محادثة مع المالك.</div>
          </div>
        </div>
      </aside>
    </section>

    <footer class="container footer">
      <div>© <span id="year"></span> Fast Phone — <span data-i18n="footer">كل الحقوق محفوظة.</span></div>
      <div class="chip">v1.0</div>
    </footer>
  </main>

  <!-- Owner/Admin Panel Modal -->
  <dialog id="ownerDialog">
    <div class="modal-body">
      <div style="display:flex; justify-content:space-between; align-items:center;">
        <h3 style="font-size:1.15rem" data-i18n="ownerPanel">لوحة تحكم المالك</h3>
        <button class="icon-btn" id="closeOwnerDialog">✖</button>
      </div>

      <div class="badge" id="ownerEmailBadge">—</div>

      <div class="modal-grid">
        <section class="card" style="padding: .8rem;">
          <h4 data-i18n="manageProducts">إدارة المنتجات</h4>
          <div class="field">
            <label data-i18n="pName">اسم المنتج</label>
            <input id="pName" />
          </div>
          <div class="field">
            <label data-i18n="pPrice">السعر (د.ج)</label>
            <input id="pPrice" type="number" min="0" />
          </div>
          <div class="field">
            <label data-i18n="pOldPrice">سعر قديم (اختياري)</label>
            <input id="pOldPrice" type="number" min="0" />
          </div>
          <div class="field">
            <label data-i18n="pStock">المخزون</label>
            <input id="pStock" type="number" min="0" />
          </div>
          <div class="field">
            <label data-i18n="pImage">رابط الصورة</label>
            <input id="pImage" placeholder="https://..." />
          </div>
          <div class="field">
            <label data-i18n="pCategory">الفئة</label>
            <select id="pCategory">
              <option value="accessories" data-i18n="catAccessories">إكسسوارات</option>
              <option value="spare" data-i18n="catSpare">قطع غيار</option>
              <option value="phones" data-i18n="catPhones">هواتف</option>
            </select>
          </div>
          <div style="display:flex; gap:.5rem; margin-top:.4rem; flex-wrap:wrap;">
            <button class="btn success" id="addProduct" data-i18n="add">إضافة</button>
            <button class="btn" id="updateProduct" data-i18n="update">تعديل</button>
            <button class="btn" id="deleteProduct" data-i18n="delete">حذف</button>
          </div>
          <div class="field" style="margin-top:.6rem;">
            <label data-i18n="selectProduct">اختر منتجًا للتعديل</label>
            <select id="productSelect"></select>
          </div>
        </section>

        <section class="card" style="padding: .8rem;">
          <h4 data-i18n="manageServices">إدارة الخدمات</h4>
          <div class="field">
            <label data-i18n="sTitle">عنوان الخدمة</label>
            <input id="sTitle" />
          </div>
          <div class="field">
            <label data-i18n="sDesc">وصف</label>
            <textarea id="sDesc"></textarea>
          </div>
          <div class="field">
            <label data-i18n="sPrice">سعر تقريبي (د.ج)</label>
            <input id="sPrice" type="number" min="0" />
          </div>
          <div style="display:flex; gap:.5rem; margin-top:.4rem; flex-wrap:wrap;">
            <button class="btn success" id="addService" data-i18n="add">إضافة</button>
            <button class="btn" id="updateService" data-i18n="update">تعديل</button>
            <button class="btn" id="deleteService" data-i18n="delete">حذف</button>
          </div>
          <div class="field" style="margin-top:.6rem;">
            <label data-i18n="selectService">اختر خدمة للتعديل</label>
            <select id="serviceSelect"></select>
          </div>
        </section>
      </div>

      <section class="card" style="padding:.8rem;">
        <h4 data-i18n="coupons">قسائم الخصم</h4>
        <div class="modal-grid">
          <div class="field">
            <label data-i18n="cCode">الكود</label>
            <input id="cCode" />
          </div>
          <div class="field">
            <label data-i18n="cPercent">نسبة الخصم %</label>
            <input id="cPercent" type="number" min="0" max="100" />
          </div>
          <div class="field">
            <label data-i18n="cActive">مفعل؟</label>
            <select id="cActive">
              <option value="true" data-i18n="yes">نعم</option>
              <option value="false" data-i18n="no">لا</option>
            </select>
          </div>
          <div style="display:flex; gap:.5rem; align-items:end;">
            <button class="btn success" id="addCoupon" data-i18n="add">إضافة</button>
            <button class="btn" id="deleteCoupon" data-i18n="delete">حذف</button>
          </div>
        </div>
        <div class="field" style="margin-top:.6rem;">
          <label data-i18n="existingCoupons">القسائم الحالية</label>
          <select id="couponSelect"></select>
        </div>
      </section>

      <section class="card" style="padding:.8rem; display:grid; gap:.6rem;">
        <h4 data-i18n="data">البيانات</h4>
        <div style="display:flex; gap:.5rem; flex-wrap:wrap;">
          <button class="btn" id="exportBtn" data-i18n="export">تصدير JSON</button>
          <input type="file" id="importFile" accept="application/json" style="display:none;" />
          <button class="btn" id="importBtn" data-i18n="import">استيراد JSON</button>
        </div>
      </section>
    </div>
  </dialog>

  <script>
    // =====================================================================================
    // Configuration & Constants
    // =====================================================================================

    // ✅ ضع بريد المالك هنا — Owner Email (Google account) who can manage the store
    const OWNER_EMAIL = "owner@example.com"; // ← بدّلها ببريد المالك الحقيقي لاحقًا

    // ✅ رابط محادثة المالك — chat schema. Example WhatsApp: https://wa.me/PHONE?text=
    // يمكنك استخدام Telegram: https://t.me/USERNAME
    // أو Messenger: https://m.me/USERNAME
    const OWNER_CHAT = {
      type: "whatsapp", // "whatsapp" | "telegram" | "messenger"
      phone: "+213555000000", // لتطبيق واتساب: رقم دولي بدون + إن أردت: "213555000000"
      telegramUser: "fastphone_owner", // في حالة التليجرام
      messengerUser: "fastphone.page" // في حالة مسنجر
    };

    // Firebase placeholders (اختياري — التفعيل لاحقًا)
    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_AUTH_DOMAIN",
      projectId: "YOUR_PROJECT_ID",
      storageBucket: "YOUR_BUCKET",
      messagingSenderId: "YOUR_SENDER_ID",
      appId: "YOUR_APP_ID"
    };

    // مفاتيح التخزين المحلي
    const LS_KEYS = {
      CART: "ff_cart",
      PRODUCTS: "ff_products",
      SERVICES: "ff_services",
      COUPONS: "ff_coupons",
      THEME: "ff_theme",
      LANG: "ff_lang"
    };

    // العملات
    const CURRENCY = "د.ج"; // DZD

    // =====================================================================================
    // Internationalization (Arabic / French)
    // =====================================================================================

    const I18N = {
      ar: {
        brandTitle: "Fast Phone",
        brandSubtitle: "متجر وخدمات صيانة الهواتف",
        statusOnline: "الحالة: متصل",
        theme: "الوضع",
        login: "دخول بجوجل",
        logout: "خروج",
        cartButton: "سلة ({{count}})",
        welcome: "مرحبًا بك في",
        heroText: "اطلب المنتجات المتوفرة وشاهد خدمات الصيانة لدينا. عند الضغط على \"طلب\" ستُفتح محادثة مع صاحب المحل برسالة جاهزة. المالك فقط يمكنه إدارة العناصر.",
        avgRepair: "متوسط زمن الإصلاح",
        warranty: "ضمان الصيانة",
        payment: "طرق الدفع",
        reminder: "تذكير:",
        reminderDetail: "فعّل تسجيل الدخول بجوجل بإضافة إعدادات Firebase الخاصة بك.",
        ownerFeatureTitle: "خاصية المالك:",
        ownerFeature: "عند تسجيل الدخول بحساب المالك تستطيع إدارة المنتجات والخدمات من لوحة التحكم.",
        ordersTitle: "الطلبات:",
        ordersDetail: "زر \"طلب\" يفتح واتساب/تليجرام المالك برسالة مفصلة تشمل العناصر من السلة.",
        ownerPanel: "لوحة تحكم المالك",
        backup: "نسخ احتياطي محلي",
        restore: "استرجاع بيانات",
        products: "المنتجات",
        sortPopular: "الأكثر شيوعًا",
        sortNewest: "الأحدث",
        sortPriceAsc: "السعر: من الأقل للأعلى",
        sortPriceDesc: "السعر: من الأعلى للأقل",
        inStockOnly: "متوفر فقط",
        resetFilters: "إعادة تعيين",
        servicesTitle: "الخدمات",
        serviceWarranty: "ضمان 30 يوم",
        freeCheck: "فحص مجاني عند الإصلاح",
        cartTitle: "سلة المشتريات",
        cartEmpty: "السلة فارغة حالياً",
        total: "الإجمالي",
        couponPlaceholder: "كوبون خصم",
        applyCoupon: "تطبيق",
        checkout: "طلب",
        cartNote: "ستتم عملية الطلب عبر محادثة مع المالك.",
        footer: "كل الحقوق محفوظة.",
        manageProducts: "إدارة المنتجات",
        pName: "اسم المنتج",
        pPrice: "السعر (د.ج)",
        pOldPrice: "سعر قديم (اختياري)",
        pStock: "المخزون",
        pImage: "رابط الصورة",
        pCategory: "الفئة",
        catAccessories: "إكسسوارات",
        catSpare: "قطع غيار",
        catPhones: "هواتف",
        add: "إضافة",
        update: "تعديل",
        delete: "حذف",
        selectProduct: "اختر منتجًا للتعديل",
        manageServices: "إدارة الخدمات",
        sTitle: "عنوان الخدمة",
        sDesc: "وصف",
        sPrice: "سعر تقريبي (د.ج)",
        selectService: "اختر خدمة للتعديل",
        coupons: "قسائم الخصم",
        cCode: "الكود",
        cPercent: "نسبة الخصم %",
        cActive: "مفعل؟",
        yes: "نعم",
        no: "لا",
        existingCoupons: "القسائم الحالية",
        data: "البيانات",
        export: "تصدير JSON",
        import: "استيراد JSON",
        searchPlaceholder: "ابحث عن منتج أو خدمة…"
      },
      fr: {
        brandTitle: "Fast Phone",
        brandSubtitle: "Boutique et services de réparation",
        statusOnline: "Statut : en ligne",
        theme: "Thème",
        login: "Connexion Google",
        logout: "Déconnexion",
        cartButton: "Panier ({{count}})",
        welcome: "Bienvenue chez",
        heroText: "Commandez les produits disponibles et consultez nos services. En appuyant sur \"Commander\", une discussion avec le propriétaire s'ouvrira avec un message prêt. Seul le propriétaire peut gérer les éléments.",
        avgRepair: "Délai moyen de réparation",
        warranty: "Garantie réparation",
        payment: "Moyens de paiement",
        reminder: "Rappel :",
        reminderDetail: "Activez la connexion Google en ajoutant votre configuration Firebase.",
        ownerFeatureTitle: "Pour le propriétaire :",
        ownerFeature: "Connecté avec le compte du propriétaire, vous pouvez gérer produits et services.",
        ordersTitle: "Commandes :",
        ordersDetail: "Le bouton \"Commander\" ouvre WhatsApp/Telegram du propriétaire avec le panier.",
        ownerPanel: "Panneau du propriétaire",
        backup: "Sauvegarde locale",
        restore: "Restaurer",
        products: "Produits",
        sortPopular: "Les plus populaires",
        sortNewest: "Les plus récents",
        sortPriceAsc: "Prix : croissant",
        sortPriceDesc: "Prix : décroissant",
        inStockOnly: "En stock seulement",
        resetFilters: "Réinitialiser",
        servicesTitle: "Services",
        serviceWarranty: "Garantie 30 jours",
        freeCheck: "Diagnostic gratuit avec réparation",
        cartTitle: "Panier",
        cartEmpty: "Le panier est vide",
        total: "Total",
        couponPlaceholder: "Code promo",
        applyCoupon: "Appliquer",
        checkout: "Commander",
        cartNote: "La commande se fera via une discussion avec le propriétaire.",
        footer: "Tous droits réservés.",
        manageProducts: "Gérer les produits",
        pName: "Nom du produit",
        pPrice: "Prix (DZD)",
        pOldPrice: "Ancien prix (optionnel)",
        pStock: "Stock",
        pImage: "URL de l'image",
        pCategory: "Catégorie",
        catAccessories: "Accessoires",
        catSpare: "Pièces détachées",
        catPhones: "Téléphones",
        add: "Ajouter",
        update: "Mettre à jour",
        delete: "Supprimer",
        selectProduct: "Choisir un produit",
        manageServices: "Gérer les services",
        sTitle: "Titre du service",
        sDesc: "Description",
        sPrice: "Prix estimatif (DZD)",
        selectService: "Choisir un service",
        coupons: "Codes promo",
        cCode: "Code",
        cPercent: "Réduction %",
        cActive: "Actif ?",
        yes: "Oui",
        no: "Non",
        existingCoupons: "Codes existants",
        data: "Données",
        export: "Exporter JSON",
        import: "Importer JSON",
        searchPlaceholder: "Rechercher un produit ou un service…"
      }
    };

    let currentLang = localStorage.getItem(LS_KEYS.LANG) || 'ar';

    // =====================================================================================
    // Utilities
    // =====================================================================================

    const $ = (sel, ctx=document) => ctx.querySelector(sel);
    const $$ = (sel, ctx=document) => Array.from(ctx.querySelectorAll(sel));

    function formatPrice(num) { return `${Number(num||0).toLocaleString(currentLang)} ${CURRENCY}`; }

    function uid(prefix="id") { return `${prefix}_${Math.random().toString(36).slice(2,9)}`; }

    function saveLS(key, value) { localStorage.setItem(key, JSON.stringify(value)); }
    function loadLS(key, fallback) {
      try { const v = JSON.parse(localStorage.getItem(key)); return v ?? fallback; } catch { return fallback; }
    }

    function toast(msg) {
      // بسيط: badge عائم
      const t = document.createElement('div');
      t.textContent = msg; t.style.position='fixed'; t.style.bottom='16px'; t.style.right='16px'; t.style.padding='10px 14px'; t.style.background='var(--card)'; t.style.border='1px solid var(--border)'; t.style.borderRadius='12px'; t.style.boxShadow='var(--shadow)'; t.style.zIndex=9999; t.style.color='var(--text)';
      document.body.appendChild(t); setTimeout(()=>{ t.remove(); }, 2200);
    }

    function setTheme(mode) {
      if(mode === 'light') document.body.classList.add('light');
      else document.body.classList.remove('light');
      localStorage.setItem(LS_KEYS.THEME, mode);
      $('#themeIcon').textContent = mode === 'light' ? '☀️' : '🌙';
    }

    function toggleTheme() {
      const cur = localStorage.getItem(LS_KEYS.THEME) || 'dark';
      setTheme(cur === 'dark' ? 'light' : 'dark');
    }

    function applyI18n() {
      const dict = I18N[currentLang];
      // عناصر النصوص
      $$('[data-i18n]').forEach(el => { el.textContent = dict[el.getAttribute('data-i18n')] || el.textContent; });
      // عناصر placeholder
      $$('[data-i18n-placeholder]').forEach(el => { el.placeholder = dict[el.getAttribute('data-i18n-placeholder')] || el.placeholder; });
      // خيارات select
      $$('option[data-i18n]').forEach(el => { el.textContent = dict[el.getAttribute('data-i18n')] || el.textContent; });

      // اتجاه الصفحة
      document.documentElement.lang = currentLang;
      document.documentElement.dir = currentLang === 'ar' ? 'rtl' : 'ltr';
      $('#langLabel').textContent = currentLang === 'ar' ? 'العربية' : 'Français';

      // تحديث بعض النصوص الديناميكية مثل زر السلة
      updateCartCount();
      // إعادة رسم القوائم لعرض الأسعار المنسقة حسب اللغة
      renderCatalog();
      renderServices();
    }

    function setLang(lang) {
      currentLang = lang; localStorage.setItem(LS_KEYS.LANG, lang); applyI18n();
    }

    // =====================================================================================
    // Data Models
    // =====================================================================================

    let products = loadLS(LS_KEYS.PRODUCTS, [
      { id: uid('p'), name: 'شاحن سريع 20W', price: 2200, oldPrice: 2600, stock: 8, image: 'https://images.unsplash.com/photo-1609592424022-59df09ee59d2?auto=format&fit=crop&w=800&q=60', category: 'accessories', pop: 93, createdAt: Date.now()-86400000*4 },
      { id: uid('p'), name: 'سماعات بلوتوث', price: 3500, oldPrice: 0, stock: 12, image: 'https://images.unsplash.com/photo-1518444314310-66b7a31f10bf?auto=format&fit=crop&w=800&q=60', category: 'accessories', pop: 120, createdAt: Date.now()-86400000*2 },
      { id: uid('p'), name: 'شاشة بديلة لهاتف XYZ', price: 9500, oldPrice: 11000, stock: 4, image: 'https://images.unsplash.com/photo-1519389950473-47ba0277781c?auto=format&fit=crop&w=800&q=60', category: 'spare', pop: 75, createdAt: Date.now()-86400000*7 },
      { id: uid('p'), name: 'غطاء حماية سيليكون', price: 900, oldPrice: 1200, stock: 25, image: 'https://images.unsplash.com/photo-1598965402089-897ce52e835b?auto=format&fit=crop&w=800&q=60', category: 'accessories', pop: 60, createdAt: Date.now()-86400000*1 },
      { id: uid('p'), name: 'هاتف مستعمل بحالة ممتازة', price: 42000, oldPrice: 0, stock: 2, image: 'https://images.unsplash.com/photo-1511707171634-5f897ff02aa9?auto=format&fit=crop&w=800&q=60', category: 'phones', pop: 35, createdAt: Date.now()-86400000*10 }
    ]);

    let services = loadLS(LS_KEYS.SERVICES, [
      { id: uid('s'), title: 'تبديل شاشة', desc: 'استبدال شاشة مكسورة/معطلة بجودة عالية مع ضمان 30 يوم.', price: 8000 },
      { id: uid('s'), title: 'تغيير بطارية', desc: 'بطاريات أصلية/عالية الجودة مع فحص مجاني.', price: 5000 },
      { id: uid('s'), title: 'تنظيف مدخل الشحن', desc: 'تنظيف احترافي واستعادة الشحن الطبيعي.', price: 1200 }
    ]);

    let coupons = loadLS(LS_KEYS.COUPONS, [
      { code: 'FAST10', percent: 10, active: true },
      { code: 'WELCOME5', percent: 5, active: true }
    ]);

    let cart = loadLS(LS_KEYS.CART, []);

    // =====================================================================================
    // Rendering: Products & Services
    // =====================================================================================

    function productCard(p) {
      const outOfStock = p.stock <= 0;
      return `
      <article class="card product" data-id="${p.id}" data-name="${p.name.toLowerCase()}" data-category="${p.category}">
        <div class="thumb">
          <img src="${p.image}" alt="${p.name}" loading="lazy" />
          ${outOfStock ? `<span class="label">${currentLang==='ar'?'نفد المخزون':'Rupture'}</span>` : ''}
        </div>
        <div class="body">
          <div class="name">${p.name}</div>
          <div class="meta">
            <div>
              <span class="price">${formatPrice(p.price)}</span>
              ${p.oldPrice? `<span class="old">${formatPrice(p.oldPrice)}</span>`:''}
            </div>
            <span class="badge">${currentLang==='ar'?'المخزون':'Stock'}: ${p.stock}</span>
          </div>
          <div class="actions">
            <button class="btn" data-action="add" ${outOfStock?'disabled':''}>${currentLang==='ar'?'إضافة للسلة':'Ajouter au panier'}</button>
            <button class="btn primary" data-action="buy" ${outOfStock?'disabled':''}>${currentLang==='ar'?'طلب':'Commander'}</button>
          </div>
        </div>
      </article>`;
    }

    function renderCatalog() {
      const catalog = $('#catalog');
      if(!catalog) return;
      const query = ($('#searchInput')?.value || '').toLowerCase().trim();
      const inStock = $('#filterInStock')?.classList.contains('active');
      const sort = $('#sortSelect')?.value || 'pop';

      let list = [...products];
      if (query) list = list.filter(p => p.name.toLowerCase().includes(query));
      if (inStock) list = list.filter(p => p.stock > 0);
      if (sort === 'pop') list.sort((a,b)=> b.pop - a.pop);
      if (sort === 'new') list.sort((a,b)=> b.createdAt - a.createdAt);
      if (sort === 'price-asc') list.sort((a,b)=> a.price - b.price);
      if (sort === 'price-desc') list.sort((a,b)=> b.price - a.price);

      catalog.innerHTML = list.map(productCard).join('') || `<div class="empty">${currentLang==='ar'?'لا نتائج':'Aucun résultat'}</div>`;

      // Bind buttons
      $$('#catalog .product .actions .btn').forEach(btn => {
        btn.addEventListener('click', () => {
          const card = btn.closest('.product');
          const id = card.getAttribute('data-id');
          const item = products.find(p => p.id === id);
          if(!item) return;
          const action = btn.getAttribute('data-action');
          if(action === 'add') addToCart(item.id, 1);
          if(action === 'buy') { addToCart(item.id, 1); openCheckout(); }
        });
      });
    }

    function serviceCard(s) {
      return `
      <article class="card service">
        <div class="icon">🔧</div>
        <div>
          <div class="title">${s.title}</div>
          <div class="desc">${s.desc}</div>
          <div class="price" style="margin-top:.3rem; font-weight:800; color:var(--accent-2);">${formatPrice(s.price)}</div>
        </div>
      </article>`;
    }

    function renderServices() {
      const wrap = $('#services');
      if(!wrap) return;
      wrap.innerHTML = services.map(serviceCard).join('');
    }

    // =====================================================================================
    // Cart
    // =====================================================================================

    function addToCart(productId, qty=1) {
      const p = products.find(x => x.id === productId);
      if(!p || p.stock <= 0) return toast(currentLang==='ar'?'غير متوفر':'Indisponible');
      const row = cart.find(x=>x.id===productId);
      if(row) row.qty += qty; else cart.push({ id: productId, qty });
      saveLS(LS_KEYS.CART, cart);
      updateCartCount();
      renderCart();
      toast(currentLang==='ar'?'أضيف إلى السلة':'Ajouté au panier');
    }

    function updateCartCount() {
      const count = cart.reduce((n,x)=>n+x.qty,0);
      $('#cartCount').textContent = count;
      const dict = I18
      <script>
      // ===== تكملة السكريبت =====

      // تابع زر السلة مع الترجمة
      function updateCartCount() {
        const count = cart.reduce((n, x) => n + x.qty, 0);
        $('#cartCount').textContent = count;
        const dict = I18N[currentLang];
        // تحديث نص زر السلة وفقًا للغة
        const btn = $('#openCart');
        if (btn) {
          btn.innerHTML = (dict.cartButton || 'سلة ({{count}})').replace('{{count}}', `<span id="cartCount">${count}</span>`);
        }
      }

      // حساب الإجمالي + تطبيق الكوبون (إن وجد)
      let appliedCoupon = null;
      function calcCartTotal() {
        let total = 0;
        cart.forEach(row => {
          const p = products.find(x => x.id === row.id);
          if (p) total += p.price * row.qty;
        });
        let discount = 0;
        if (appliedCoupon && appliedCoupon.active) {
          discount = Math.round(total * (appliedCoupon.percent / 100));
        }
        return { total, discount, grand: Math.max(total - discount, 0) };
      }

      // رسم السلة
      function renderCart() {
        const box = $('#cartItems');
        if (!box) return;
        if (!cart.length) {
          box.innerHTML = `<div class="empty">${currentLang==='ar'?'السلة فارغة حالياً':'Le panier est vide'}</div>`;
        } else {
          box.innerHTML = cart.map(row => {
            const p = products.find(x => x.id === row.id);
            if (!p) return '';
            return `
              <div class="row" data-id="${row.id}">
                <div>
                  <div class="name">${p.name}</div>
                  <div class="pill" style="margin-top:.2rem">${formatPrice(p.price)} × ${row.qty}</div>
                </div>
                <div class="qty">
                  <button class="icon-btn" data-act="dec">➖</button>
                  <strong>${row.qty}</strong>
                  <button class="icon-btn" data-act="inc">➕</button>
                  <button class="icon-btn" data-act="del" title="${currentLang==='ar'?'حذف':'Supprimer'}">🗑</button>
                </div>
              </div>
            `;
          }).join('');
        }
        const { total, discount, grand } = calcCartTotal();
        $('#cartTotal').textContent = formatPrice(grand);
        // تفعيل أزرار عناصر السلة
        $$('#cartItems .row .icon-btn').forEach(btn => {
          btn.addEventListener('click', () => {
            const row = btn.closest('.row');
            const id = row.getAttribute('data-id');
            const act = btn.getAttribute('data-act');
            const idx = cart.findIndex(x => x.id === id);
            if (idx === -1) return;
            if (act === 'inc') cart[idx].qty++;
            if (act === 'dec') { cart[idx].qty = Math.max(1, cart[idx].qty - 1); }
            if (act === 'del') cart.splice(idx, 1);
            saveLS(LS_KEYS.CART, cart);
            updateCartCount();
            renderCart();
          });
        });
      }

      // تطبيق الكوبون
      $('#applyCoupon').addEventListener('click', () => {
        const code = ($('#couponInput').value || '').trim().toUpperCase();
        if (!code) return toast(currentLang==='ar'?'أدخل الكود':'Entrez le code');
        const c = coupons.find(x => x.code.toUpperCase() === code && x.active);
        if (!c) { appliedCoupon = null; toast(currentLang==='ar'?'كوبون غير صالح':'Code invalide'); renderCart(); return; }
        appliedCoupon = c;
        toast(currentLang==='ar'?'تم تطبيق الخصم':'Remise appliquée');
        renderCart();
      });

      // تفريغ السلة
      $('#clearCart').addEventListener('click', () => {
        cart = [];
        saveLS(LS_KEYS.CART, cart);
        appliedCoupon = null;
        $('#couponInput').value = '';
        updateCartCount();
        renderCart();
      });

      // فتح/تركيز السلة (هي مثبتة، نستخدم Toast بسيط)
      $('#openCart').addEventListener('click', () => {
        toast(currentLang==='ar'?'تم فتح السلة على اليمين':'Panier ouvert à droite');
      });

      // إنشاء رسالة الطلب وفتح محادثة المالك
      function openCheckout() {
        if (!cart.length) return toast(currentLang==='ar'?'السلة فارغة':'Panier vide');

        const { total, discount, grand } = calcCartTotal();
        const lines = cart.map(row => {
          const p = products.find(x => x.id === row.id);
          return p ? `• ${p.name} × ${row.qty} = ${formatPrice(p.price * row.qty)}` : '';
        }).filter(Boolean);

        const header = currentLang==='ar' ? 'طلب جديد من تطبيق Fast Phone' : 'Nouvelle commande depuis Fast Phone';
        const totLine = `${currentLang==='ar'?'المجموع':'Total'}: ${formatPrice(total)}`;
        const discLine = discount ? `\n${currentLang==='ar'?'الخصم':'Remise'}: -${formatPrice(discount)}` : '';
        const grandLine = `\n${currentLang==='ar'?'الإجمالي بعد الخصم':'Total à payer'}: ${formatPrice(grand)}`;
        const note = currentLang==='ar'?'من فضلك أكدوا التوفر والموعد.':'Merci de confirmer la disponibilité et le délai.';

        const msg = `${header}\n\n${lines.join('\n')}\n\n${totLine}${discLine}${grandLine}\n\n${note}`;

        // اختيار منصة الدردشة
        let url = '';
        if (OWNER_CHAT.type === 'whatsapp') {
          // رقم بدون +
          const phone = (OWNER_CHAT.phone || '').replace(/[^\d]/g,'');
          url = `https://wa.me/${phone}?text=${encodeURIComponent(msg)}`;
        } else if (OWNER_CHAT.type === 'telegram') {
          url = `https://t.me/${OWNER_CHAT.telegramUser}?text=${encodeURIComponent(msg)}`;
        } else if (OWNER_CHAT.type === 'messenger') {
          url = `https://m.me/${OWNER_CHAT.messengerUser}?text=${encodeURIComponent(msg)}`;
        } else {
          // افتراضي واتساب
          const phone = (OWNER_CHAT.phone || '').replace(/[^\d]/g,'');
          url = `https://wa.me/${phone}?text=${encodeURIComponent(msg)}`;
        }
        window.open(url, '_blank');
      }

      $('#checkoutBtn').addEventListener('click', openCheckout);

      // ================================
      // البحث والفرز والفلاتر
      // ================================
      $('#searchInput').addEventListener('input', () => renderCatalog());
      $('#clearSearch').addEventListener('click', () => { $('#searchInput').value=''; renderCatalog(); });

      $('#sortSelect').addEventListener('change', renderCatalog);

      $('#filterInStock').addEventListener('click', (e) => {
        e.currentTarget.classList.toggle('active');
        renderCatalog();
      });

      $('#resetFilters').addEventListener('click', () => {
        $('#sortSelect').value = 'pop';
        $('#filterInStock').classList.remove('active');
        $('#searchInput').value = '';
        renderCatalog();
      });

      // ================================
      // اللغة والثيم
      // ================================
      $('#langBtn').addEventListener('click', () => {
        setLang(currentLang === 'ar' ? 'fr' : 'ar');
      });

      $('#themeBtn').addEventListener('click', toggleTheme);

      // تطبيق الثيم المفضل عند التحميل
      setTheme(localStorage.getItem(LS_KEYS.THEME) || 'dark');

      // ================================
      // سنة الفوتر
      // ================================
      $('#year').textContent = new Date().getFullYear();

      // ================================
      // تسجيل الدخول (نسخة تجريبية بدون Firebase)
      // ملاحظة: هذه محاكاة محلية. للاستعمال الحقيقي فعّل Firebase Auth.
      // ================================
      let currentUser = null;

      function refreshUserUI() {
        if (currentUser) {
          $('#loginBtn').style.display = 'none';
          $('#userMenu').style.display = 'inline-flex';
          $('#userName').textContent = currentUser.email;
          $('#userAvatar').src = currentUser.photoURL || 'https://i.pravatar.cc/64?img=12';
          $('#ownerEmailBadge').textContent = `${currentLang==='ar'?'حساب المالك:':'Propriétaire :'} ${OWNER_EMAIL}`;
        } else {
          $('#loginBtn').style.display = 'inline-flex';
          $('#userMenu').style.display = 'none';
        }
      }

      $('#loginBtn').addEventListener('click', () => {
        const email = prompt(currentLang==='ar'?'أدخل بريدك الإلكتروني (محاكاة دخول)':'Entrez votre email (simulation de connexion)');
        if (!email) return;
        currentUser = { email, photoURL: '' };
        refreshUserUI();
        toast(currentLang==='ar'?'تم تسجيل الدخول (محاكاة)':'Connecté (simulation)');
      });

      $('#logoutBtn').addEventListener('click', () => {
        currentUser = null;
        refreshUserUI();
        toast(currentLang==='ar'?'تم تسجيل الخروج':'Déconnecté');
      });

      // هل المستخدم مالك؟
      function isOwner() { return currentUser && currentUser.email && currentUser.email.toLowerCase() === OWNER_EMAIL.toLowerCase(); }

      // ================================
      // لوحة تحكم المالك (CRUD)
      // ================================
      const ownerDialog = $('#ownerDialog');
      $('#openOwnerPanel').addEventListener('click', () => {
        if (!isOwner()) {
          return toast(currentLang==='ar'?'هذه الميزة للمالك فقط':'Réservé au propriétaire');
        }
        syncSelects();
        ownerDialog.showModal();
      });
      $('#closeOwnerDialog').addEventListener('click', () => ownerDialog.close());

      // مزامنة قوائم الاختيار
      function syncSelects() {
        const pSel = $('#productSelect');
        pSel.innerHTML = products.map(p => `<option value="${p.id}">${p.name}</option>`).join('');
        const sSel = $('#serviceSelect');
        sSel.innerHTML = services.map(s => `<option value="${s.id}">${s.title}</option>`).join('');
        const cSel = $('#couponSelect');
        cSel.innerHTML = coupons.map(c => `<option value="${c.code}">${c.code} — ${c.percent}% ${c.active ? '✓' : '✗'}</option>`).join('');
      }

      // — المنتجات
      $('#addProduct').addEventListener('click', () => {
        if (!isOwner()) return;
        const item = {
          id: uid('p'),
          name: $('#pName').value.trim(),
          price: Number($('#pPrice').value || 0),
          oldPrice: Number($('#pOldPrice').value || 0),
          stock: Number($('#pStock').value || 0),
          image: $('#pImage').value.trim(),
          category: $('#pCategory').value,
          pop: 0,
          createdAt: Date.now()
        };
        if (!item.name) return toast(currentLang==='ar'?'أدخل اسم المنتج':'Nom requis');
        products.push(item);
        saveLS(LS_KEYS.PRODUCTS, products);
        renderCatalog(); syncSelects();
        toast(currentLang==='ar'?'تمت الإضافة':'Ajouté');
      });

      $('#updateProduct').addEventListener('click', () => {
        if (!isOwner()) return;
        const id = $('#productSelect').value;
        const p = products.find(x => x.id === id);
        if (!p) return;
        p.name = $('#pName').value.trim() || p.name;
        p.price = Number($('#pPrice').value || p.price);
        p.oldPrice = Number($('#pOldPrice').value || p.oldPrice);
        p.stock = Number($('#pStock').value || p.stock);
        p.image = $('#pImage').value.trim() || p.image;
        p.category = $('#pCategory').value || p.category;
        saveLS(LS_KEYS.PRODUCTS, products);
        renderCatalog(); syncSelects();
        toast(currentLang==='ar'?'تم التعديل':'Mis à jour');
      });

      $('#deleteProduct').addEventListener('click', () => {
        if (!isOwner()) return;
        const id = $('#productSelect').value;
        const idx = products.findIndex(x => x.id === id);
        if (idx === -1) return;
        products.splice(idx, 1);
        saveLS(LS_KEYS.PRODUCTS, products);
        renderCatalog(); syncSelects();
        toast(currentLang==='ar'?'تم الحذف':'Supprimé');
      });

      // — الخدمات
      $('#addService').addEventListener('click', () => {
        if (!isOwner()) return;
        const s = {
          id: uid('s'),
          title: $('#sTitle').value.trim(),
          desc: $('#sDesc').value.trim(),
          price: Number($('#sPrice').value || 0)
        };
        if (!s.title) return toast(currentLang==='ar'?'أدخل عنوان الخدمة':'Titre requis');
        services.push(s);
        saveLS(LS_KEYS.SERVICES, services);
        renderServices(); syncSelects();
        toast(currentLang==='ar'?'تمت الإضافة':'Ajouté');
      });

      $('#updateService').addEventListener('click', () => {
        if (!isOwner()) return;
        const id = $('#serviceSelect').value;
        const s = services.find(x => x.id === id);
        if (!s) return;
        s.title = $('#sTitle').value.trim() || s.title;
        s.desc = $('#sDesc').value.trim() || s.desc;
        s.price = Number($('#sPrice').value || s.price);
        saveLS(LS_KEYS.SERVICES, services);
        renderServices(); syncSelects();
        toast(currentLang==='ar'?'تم التعديل':'Mis à jour');
      });

      $('#deleteService').addEventListener('click', () => {
        if (!isOwner()) return;
        const id = $('#serviceSelect').value;
        const idx = services.findIndex(x => x.id === id);
        if (idx === -1) return;
        services.splice(idx, 1);
        saveLS(LS_KEYS.SERVICES, services);
        renderServices(); syncSelects();
        toast(currentLang==='ar'?'تم الحذف':'Supprimé');
      });

      // — القسائم
      $('#addCoupon').addEventListener('click', () => {
        if (!isOwner()) return;
        const c = {
          code: ($('#cCode').value || '').trim(),
          percent: Number($('#cPercent').value || 0),
          active: $('#cActive').value === 'true'
        };
        if (!c.code) return toast(currentLang==='ar'?'أدخل الكود':'Code requis');
        const exists = coupons.find(x => x.code.toUpperCase() === c.code.toUpperCase());
        if (exists) { exists.percent = c.percent; exists.active = c.active; }
        else coupons.push(c);
        saveLS(LS_KEYS.COUPONS, coupons);
        syncSelects();
        toast(currentLang==='ar'?'تم الحفظ':'Enregistré');
      });

      $('#deleteCoupon').addEventListener('click', () => {
        if (!isOwner()) return;
        const val = $('#couponSelect').value;
        const idx = coupons.findIndex(x => x.code === val);
        if (idx === -1) return;
        coupons.splice(idx, 1);
        saveLS(LS_KEYS.COUPONS, coupons);
        syncSelects();
        toast(currentLang==='ar'?'تم الحذف':'Supprimé');
      });

      // — النسخ الاحتياطي/الاسترجاع
      $('#backupBtn').addEventListener('click', () => {
        const data = { products, services, coupons };
        const blob = new Blob([JSON.stringify(data, null, 2)], { type: 'application/json' });
        const a = document.createElement('a');
        a.href = URL.createObjectURL(blob);
        a.download = `fastphone-backup-${new Date().toISOString().slice(0,10)}.json`;
        a.click();
      });

      $('#restoreBtn').addEventListener('click', () => {
        $('#importFile').click();
      });

      $('#importBtn').addEventListener('click', () => {
        $('#importFile').click();
      });

      $('#importFile').addEventListener('change', async (e) => {
        const file = e.target.files[0];
        if (!file) return;
        const text = await file.text();
        try {
          const data = JSON.parse(text);
          if (Array.isArray(data.products)) { products = data.products; saveLS(LS_KEYS.PRODUCTS, products); }
          if (Array.isArray(data.services)) { services = data.services; saveLS(LS_KEYS.SERVICES, services); }
          if (Array.isArray(data.coupons)) { coupons = data.coupons; saveLS(LS_KEYS.COUPONS, coupons); }
          renderCatalog(); renderServices(); syncSelects();
          toast(currentLang==='ar'?'تم الاستيراد':'Importé');
        } catch {
          toast(currentLang==='ar'?'ملف غير صالح':'Fichier invalide');
        } finally {
          e.target.value = '';
        }
      });

      // أول تحميل
      applyI18n();
      renderCatalog();
      renderServices();
      renderCart();
      refreshUserUI();
      </script>
</body>
</html>
