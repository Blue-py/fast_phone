<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Fast Phone | المتجر والخدمات</title>
  <meta name="description" content="تطبيق ويب لمحل Fast Phone: عرض المنتجات والخدمات، تسجيل الدخول بجوجل (محاكاة)، سلة المشتريات، والطلب عبر محادثة المالك. يدعم العربية والفرنسية - وضع داكن افتراضي." />
  <meta name="theme-color" content="#0ea5e9" />
  <style>
    /* ================ Base (Dark) ================ */
    *,*::before,*::after{box-sizing:border-box}html,body{height:100%}body{margin:0;font-family:ui-sans-serif,system-ui,-apple-system,"Segoe UI",Roboto,"Noto Kufi Arabic","Cairo",Tahoma,Arial;color:#e2e8f0;background:#071023;line-height:1.5;-webkit-font-smoothing:antialiased}
    .container{width:min(1100px,94vw);margin-inline:auto;padding:1rem}
    header{position:sticky;top:0;background:linear-gradient(180deg,rgba(2,6,23,.9),rgba(2,6,23,.6));backdrop-filter:saturate(160%) blur(12px);border-bottom:1px solid rgba(148,163,184,.06);z-index:50}
    .nav{display:grid;grid-template-columns:1fr auto 1fr;align-items:center;gap:1rem;padding:.85rem 0}
    .brand{display:flex;align-items:center;gap:.6rem;font-weight:800}
    .logo{width:38px;height:38px;border-radius:10px;background:linear-gradient(135deg,#06b6d4,#7dd3fc);display:grid;place-items:center;color:#001018;font-weight:900}
    .searchbar{display:flex;align-items:center;justify-content:center;gap:.6rem}
    input[type="search"]{width:min(520px,40vw);padding:.6rem .9rem;border-radius:999px;border:1px solid rgba(148,163,184,.08);background:#0f1724;color:var(--text,#e2e8f0);outline:none}
    .actions{display:flex;justify-content:flex-end;align-items:center;gap:.5rem}
    .btn{display:inline-flex;align-items:center;gap:.5rem;padding:.55rem .9rem;border-radius:999px;border:1px solid rgba(148,163,184,.06);background:#0f1724;color:var(--text,#e2e8f0);cursor:pointer}
    .btn.primary{background:linear-gradient(135deg,#06b6d4,#38bdf8);color:#001018;font-weight:700;border-color:transparent}
    .chip{font-size:.85rem;padding:.3rem .6rem;border-radius:999px;border:1px solid rgba(148,163,184,.06);color:#94a3b8}
    main{padding:1.1rem 0 4rem}
    .hero{display:grid;grid-template-columns:1.1fr .9fr;gap:1.4rem;align-items:center;margin:1rem 0 2rem}
    .card{background:linear-gradient(180deg, rgba(2,6,23,.25), rgba(2,6,23,.45));border:1px solid rgba(148,163,184,.06);border-radius:14px;padding:1.1rem;box-shadow:0 8px 22px rgba(0,0,0,.45)}
    .stats{display:flex;gap:1rem;flex-wrap:wrap;margin-top:.8rem}
    .stat{background:#071226;border-radius:12px;padding:.7rem 1rem;min-width:130px;border:1px solid rgba(148,163,184,.04)}
    .grid.two-col{display:grid;grid-template-columns:1.2fr .8fr;gap:1rem}
    .section-title{display:flex;align-items:center;justify-content:space-between;margin:1rem 0 .6rem}
    .catalog{display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:.8rem}
    .product{display:flex;flex-direction:column}
    .thumb{aspect-ratio:1/1;border-radius:12px 12px 0 0;overflow:hidden;background:#041226;display:grid;place-items:center}
    .product .body{padding:.8rem;display:flex;flex-direction:column;gap:.45rem}
    .price{color:#86efac;font-weight:800}
    .old{color:#94a3b8;text-decoration:line-through;margin-inline-start:.4rem}
    .actions .btn{padding:.45rem .7rem;border-radius:10px}
    .services{display:grid;grid-template-columns:repeat(auto-fill,minmax(260px,1fr));gap:.8rem}
    .service{display:flex;gap:.8rem;padding:.9rem}
    .cart{position:sticky;top:78px;align-self:start}
    .cart .head{display:flex;align-items:center;justify-content:space-between;padding:.8rem 1rem;border-bottom:1px dashed rgba(148,163,184,.04)}
    .items{max-height:52vh;overflow:auto;padding:.6rem;display:flex;flex-direction:column;gap:.6rem}
    .row{display:grid;grid-template-columns:1fr auto;gap:.6rem;align-items:center;padding:.6rem .7rem;border-radius:10px;border:1px dashed rgba(148,163,184,.04);background:transparent}
    .pill{font-size:.85rem;padding:.35rem .7rem;border-radius:999px;border:1px dashed rgba(148,163,184,.04);color:#94a3b8}
    .empty{color:#94a3b8;text-align:center;padding:2rem .6rem}
    footer{margin-top:2rem;padding:1rem 0 2rem;color:#94a3b8;border-top:1px dashed rgba(148,163,184,.04);font-size:.95rem;display:grid;gap:.4rem}
    dialog{border:none;border-radius:14px;width:min(860px,96vw);background:#0f1724;color:var(--text,#e2e8f0);box-shadow:0 12px 30px rgba(0,0,0,.6)}
    dialog::backdrop{background:rgba(2,6,23,.6);backdrop-filter:blur(2px)}
    .modal-body{padding:1rem;display:grid;gap:.8rem}
    .field{display:grid;gap:.25rem}
    .field input,.field textarea,.field select{background:#071226;border:1px solid rgba(148,163,184,.04);color:var(--text,#e2e8f0);padding:.6rem .7rem;border-radius:10px}
    .icon-btn{display:inline-grid;place-items:center;width:34px;height:34px;border-radius:10px;border:1px solid rgba(148,163,184,.04);background:#071226;cursor:pointer}
    @media (max-width:920px){.hero{grid-template-columns:1fr}.grid.two-col{grid-template-columns:1fr}}
  </style>
</head>
<body>
  <!-- Header -->
  <header>
    <div class="container nav">
      <div class="brand">
        <div class="logo">⚡️</div>
        <div>
          <div style="font-size:1.05rem" data-i18n="brandTitle">Fast Phone</div>
          <small data-i18n="brandSubtitle" style="color:#94a3b8">متجر وخدمات صيانة الهواتف</small>
        </div>
      </div>

      <div class="searchbar">
        <input id="searchInput" type="search" placeholder="ابحث عن منتج أو خدمة…" data-i18n-placeholder="searchPlaceholder" />
        <button class="btn" id="clearSearch" title="مسح البحث">✖</button>
      </div>

      <div class="actions">
        <span class="chip" id="storeStatus" data-i18n="statusOnline">الحالة: متصل</span>
        <button class="btn" id="langBtn" title="Language / اللغة" aria-label="Language Toggle"><span id="langLabel">العربية</span> 🌐</button>
        <button class="btn" id="themeBtn" title="تبديل الوضع" aria-label="Theme Toggle"><span id="themeLabel" data-i18n="theme">الوضع</span> <span id="themeIcon">🌙</span></button>
        <button class="btn" id="loginBtn" data-i18n="login">دخول (محاكاة)</button>
        <div id="userMenu" style="display:none;align-items:center;gap:.6rem;">
          <img id="userAvatar" src="" alt="" style="width:34px;height:34px;border-radius:50%;border:1px solid rgba(148,163,184,.04)" />
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
        <h1><span data-i18n="welcome">مرحبًا بك في</span> <span style="color:#06b6d4">Fast Phone</span> ⚡️</h1>
        <p data-i18n="heroText">اطلب المنتجات المتوفرة وشاهد خدمات الصيانة لدينا. عند الضغط على "طلب" ستُفتح محادثة مع صاحب المحل برسالة جاهزة. المالك فقط يمكنه إدارة العناصر.</p>
        <div class="stats">
          <div class="stat"><div class="pill" data-i18n="avgRepair">متوسط زمن الإصلاح</div><div style="font-size:1.15rem;font-weight:800">2–24h</div></div>
          <div class="stat"><div class="pill" data-i18n="warranty">ضمان الصيانة</div><div style="font-size:1.15rem;font-weight:800">30 يوم</div></div>
          <div class="stat"><div class="pill" data-i18n="payment">طرق الدفع</div><div style="font-size:1.15rem;font-weight:800">نقدي / CIB</div></div>
        </div>
      </div>

      <div class="card" style="display:grid;align-content:center;gap:.8rem;">
        <div class="alert" style="background:#071226;padding:.6rem;border-radius:10px;border:1px solid rgba(148,163,184,.04)"><strong data-i18n="reminder">تذكير:</strong> <span data-i18n="reminderDetail">فعّل تسجيل الدخول بجوجل بإضافة إعدادات Firebase الخاصة بك.</span></div>
        <div style="display:flex;gap:.6rem;flex-wrap:wrap;">
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
          <div class="filters" style="display:flex;align-items:center;gap:.5rem">
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

        <div class="section-title" style="margin-top:1.2rem;">
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
          <div class="foot" style="padding:.9rem">
            <div style="display:flex;justify-content:space-between;align-items:center;">
              <span data-i18n="total">الإجمالي</span>
              <strong id="cartTotal">0 د.ج</strong>
            </div>
            <div style="display:flex;gap:.5rem;flex-wrap:wrap;margin-top:.6rem;">
              <input id="couponInput" class="pill" placeholder="كوبون خصم" data-i18n-placeholder="couponPlaceholder" />
              <button class="btn" id="applyCoupon" data-i18n="applyCoupon">تطبيق</button>
              <button class="btn primary" id="checkoutBtn" data-i18n="checkout">طلب</button>
            </div>
            <div class="badge" id="cartNote" data-i18n="cartNote" style="margin-top:.6rem">ستتم عملية الطلب عبر محادثة مع المالك.</div>
          </div>
        </div>
      </aside>
    </section>

    <footer class="container footer">
      <div>© <span id="year"></span> Fast Phone — <span data-i18n="footer">كل الحقوق محفوظة.</span></div>
      <div class="chip">v1.0</div>
    </footer>
  </main>

  <!-- Owner/Admin Panel -->
  <dialog id="ownerDialog">
    <div class="modal-body">
      <div style="display:flex;justify-content:space-between;align-items:center;">
        <h3 style="font-size:1.05rem" data-i18n="ownerPanel">لوحة تحكم المالك</h3>
        <button class="icon-btn" id="closeOwnerDialog">✖</button>
      </div>

      <div class="badge" id="ownerEmailBadge">—</div>

      <div style="display:grid;grid-template-columns:1fr 1fr;gap:.8rem">
        <section class="card" style="padding:.8rem">
          <h4 data-i18n="manageProducts">إدارة المنتجات</h4>
          <div class="field"><label data-i18n="pName">اسم المنتج</label><input id="pName" /></div>
          <div class="field"><label data-i18n="pPrice">السعر (د.ج)</label><input id="pPrice" type="number" min="0" /></div>
          <div class="field"><label data-i18n="pOldPrice">سعر قديم (اختياري)</label><input id="pOldPrice" type="number" min="0" /></div>
          <div class="field"><label data-i18n="pStock">المخزون</label><input id="pStock" type="number" min="0" /></div>
          <div class="field"><label data-i18n="pImage">رابط الصورة</label><input id="pImage" placeholder="https://..." /></div>
          <div class="field"><label data-i18n="pCategory">الفئة</label>
            <select id="pCategory">
              <option value="accessories" data-i18n="catAccessories">إكسسوارات</option>
              <option value="spare" data-i18n="catSpare">قطع غيار</option>
              <option value="phones" data-i18n="catPhones">هواتف</option>
            </select>
          </div>
          <div style="display:flex;gap:.5rem;margin-top:.5rem;flex-wrap:wrap;">
            <button class="btn success" id="addProduct" data-i18n="add">إضافة</button>
            <button class="btn" id="updateProduct" data-i18n="update">تعديل</button>
            <button class="btn" id="deleteProduct" data-i18n="delete">حذف</button>
          </div>
          <div class="field" style="margin-top:.6rem"><label data-i18n="selectProduct">اختر منتجًا للتعديل</label><select id="productSelect"></select></div>
        </section>

        <section class="card" style="padding:.8rem">
          <h4 data-i18n="manageServices">إدارة الخدمات</h4>
          <div class="field"><label data-i18n="sTitle">عنوان الخدمة</label><input id="sTitle" /></div>
          <div class="field"><label data-i18n="sDesc">وصف</label><textarea id="sDesc"></textarea></div>
          <div class="field"><label data-i18n="sPrice">سعر تقريبي (د.ج)</label><input id="sPrice" type="number" min="0" /></div>
          <div style="display:flex;gap:.5rem;margin-top:.4rem;flex-wrap:wrap;">
            <button class="btn success" id="addService" data-i18n="add">إضافة</button>
            <button class="btn" id="updateService" data-i18n="update">تعديل</button>
            <button class="btn" id="deleteService" data-i18n="delete">حذف</button>
          </div>
          <div class="field" style="margin-top:.6rem"><label data-i18n="selectService">اختر خدمة للتعديل</label><select id="serviceSelect"></select></div>
        </section>
      </div>

      <section class="card" style="padding:.8rem;margin-top:.6rem">
        <h4 data-i18n="coupons">قسائم الخصم</h4>
        <div style="display:grid;grid-template-columns:repeat(3,1fr);gap:.6rem;">
          <div class="field"><label data-i18n="cCode">الكود</label><input id="cCode" /></div>
          <div class="field"><label data-i18n="cPercent">نسبة الخصم %</label><input id="cPercent" type="number" min="0" max="100" /></div>
          <div class="field"><label data-i18n="cActive">مفعل؟</label><select id="cActive"><option value="true" data-i18n="yes">نعم</option><option value="false" data-i18n="no">لا</option></select></div>
        </div>
        <div style="display:flex;gap:.5rem;margin-top:.6rem;align-items:end;">
          <button class="btn success" id="addCoupon" data-i18n="add">إضافة</button>
          <button class="btn" id="deleteCoupon" data-i18n="delete">حذف</button>
        </div>
        <div class="field" style="margin-top:.6rem"><label data-i18n="existingCoupons">القسائم الحالية</label><select id="couponSelect"></select></div>
      </section>

      <section class="card" style="padding:.8rem;margin-top:.6rem;display:grid;gap:.6rem;">
        <h4 data-i18n="data">البيانات</h4>
        <div style="display:flex;gap:.5rem;flex-wrap:wrap;">
          <button class="btn" id="exportBtn" data-i18n="export">تصدير JSON</button>
          <input type="file" id="importFile" accept="application/json" style="display:none;" />
          <button class="btn" id="importBtn" data-i18n="import">استيراد JSON</button>
        </div>
      </section>
    </div>
  </dialog>

  <!-- ========================= SCRIPT ========================= -->
  <script>
    // ========================= Config =========================
    const OWNER_EMAIL = "owner@example.com"; // يمكن تغييره لاحقًا
    const OWNER_CHAT = {
      type: "whatsapp",
      phone: "213657340489", // تم ضبطه حسب طلبك
      telegramUser: "fastphone_owner",
      messengerUser: "fastphone.page"
    };

    const LS_KEYS = {
      CART: "ff_cart",
      PRODUCTS: "ff_products",
      SERVICES: "ff_services",
      COUPONS: "ff_coupons",
      THEME: "ff_theme",
      LANG: "ff_lang"
    };

    const CURRENCY = "د.ج";

    // ========================= I18N =========================
    const I18N = {
      ar: {
        brandTitle: "Fast Phone",
        brandSubtitle: "متجر وخدمات صيانة الهواتف",
        statusOnline: "الحالة: متصل",
        theme: "الوضع",
        login: "دخول (محاكاة)",
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
        login: "Connexion (simulation)",
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

    // ========================= Helpers =========================
    const $ = (s, ctx=document) => ctx.querySelector(s);
    const $$ = (s, ctx=document) => Array.from(ctx.querySelectorAll(s));
    function uid(pref='id'){ return pref + '_' + Math.random().toString(36).slice(2,9); }
    function saveLS(k,v){ localStorage.setItem(k, JSON.stringify(v)); }
    function loadLS(k, fallback){ try{ const v=JSON.parse(localStorage.getItem(k)); return v ?? fallback; }catch{ return fallback; } }
    function toast(msg){ const t=document.createElement('div'); t.textContent=msg; Object.assign(t.style,{position:'fixed',bottom:'16px',right:'16px',padding:'10px 14px',background:'#0b1324',border:'1px solid rgba(148,163,184,.06)',borderRadius:'12px',boxShadow:'0 8px 22px rgba(0,0,0,.6)',zIndex:9999,color:'#e2e8f0'}); document.body.appendChild(t); setTimeout(()=>t.remove(),2200) }

    function formatPrice(num){ return `${Number(num||0).toLocaleString(currentLang)} ${CURRENCY}`; }

    // ========================= State (with localStorage) =========================
    let currentLang = localStorage.getItem(LS_KEYS.LANG) || 'ar';
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

    // ========================= Rendering =========================
    function productCard(p){
      const outOfStock = p.stock <= 0;
      return `
      <article class="card product" data-id="${p.id}" data-name="${p.name.toLowerCase()}" data-category="${p.category}">
        <div class="thumb">
          <img src="${p.image}" alt="${p.name}" loading="lazy" style="width:100%;height:100%;object-fit:cover" />
        </div>
        <div class="body">
          <div class="name" style="font-weight:800">${p.name}</div>
          <div class="meta" style="display:flex;justify-content:space-between;align-items:center">
            <div>
              <span class="price">${formatPrice(p.price)}</span>
              ${p.oldPrice? `<span class="old">${formatPrice(p.oldPrice)}</span>` : ''}
            </div>
            <span class="badge" style="color:#94a3b8">${currentLang==='ar'?'المخزون':'Stock'}: ${p.stock}</span>
          </div>
          <div class="actions" style="margin-top:.5rem;display:flex;gap:.5rem">
            <button class="btn" data-action="add" ${outOfStock?'disabled':''}>${currentLang==='ar'?'إضافة للسلة':'Ajouter'}</button>
            <button class="btn primary" data-action="buy" ${outOfStock?'disabled':''}>${currentLang==='ar'?'طلب':'Commander'}</button>
          </div>
        </div>
      </article>`;
    }

    function renderCatalog(){
      const catalog = $('#catalog');
      if(!catalog) return;
      const query = ($('#searchInput')?.value || '').toLowerCase().trim();
      const inStock = $('#filterInStock')?.classList.contains('active');
      const sort = $('#sortSelect')?.value || 'pop';
      let list = [...products];
      if(query) list = list.filter(p => p.name.toLowerCase().includes(query));
      if(inStock) list = list.filter(p => p.stock > 0);
      if(sort === 'pop') list.sort((a,b)=> b.pop - a.pop);
      if(sort === 'new') list.sort((a,b)=> b.createdAt - a.createdAt);
      if(sort === 'price-asc') list.sort((a,b)=> a.price - b.price);
      if(sort === 'price-desc') list.sort((a,b)=> b.price - a.price);

      catalog.innerHTML = list.map(productCard).join('') || `<div class="empty">${currentLang==='ar'?'لا نتائج':'Aucun résultat'}</div>`;

      // bind product buttons
      $$('#catalog .product .actions .btn').forEach(btn=>{
        btn.addEventListener('click', ()=>{
          const card = btn.closest('.product');
          const id = card.getAttribute('data-id');
          const item = products.find(p=>p.id===id);
          if(!item) return;
          const action = btn.getAttribute('data-action');
          if(action === 'add') addToCart(item.id,1);
          if(action === 'buy') { addToCart(item.id,1); openCheckout(); }
        });
      });
    }

    function serviceCard(s){
      return `
      <article class="card service">
        <div class="icon" style="font-size:22px">🔧</div>
        <div style="min-width:0">
          <div class="title" style="font-weight:800">${s.title}</div>
          <div class="desc" style="color:#94a3b8">${s.desc}</div>
          <div class="price" style="margin-top:.3rem;font-weight:800;color:#86efac">${formatPrice(s.price)}</div>
        </div>
      </article>`;
    }

    function renderServices(){
      const wrap = $('#services');
      if(!wrap) return;
      wrap.innerHTML = services.map(serviceCard).join('');
    }

    // ========================= Cart =========================
    function addToCart(productId, qty=1){
      const p = products.find(x=>x.id===productId);
      if(!p || p.stock <= 0) return toast(currentLang==='ar'?'غير متوفر':'Indisponible');
      const row = cart.find(x=>x.id===productId);
      if(row) row.qty += qty; else cart.push({ id: productId, qty });
      saveLS(LS_KEYS.CART, cart);
      updateCartCount(); renderCart(); toast(currentLang==='ar'?'أضيف إلى السلة':'Ajouté au panier');
    }

    function updateCartCount(){
      const count = cart.reduce((n,x)=>n+x.qty,0);
      $('#cartCount').textContent = count;
      const dict = I18N[currentLang] ?? I18N.ar;
      const btn = $('#openCart');
      if(btn) btn.innerHTML = (dict.cartButton || 'سلة ({{count}})').replace('{{count}}', `<span id="cartCount">${count}</span>`);
    }

    let appliedCoupon = null;
    function calcCartTotal(){
      let total = 0;
      cart.forEach(row=>{
        const p = products.find(x=>x.id===row.id);
        if(p) total += p.price * row.qty;
      });
      let discount = 0;
      if(appliedCoupon && appliedCoupon.active) discount = Math.round(total * (appliedCoupon.percent/100));
      return { total, discount, grand: Math.max(total-discount,0) };
    }

    function renderCart(){
      const box = $('#cartItems');
      if(!box) return;
      if(!cart.length){
        box.innerHTML = `<div class="empty">${currentLang==='ar'?'السلة فارغة حالياً':'Le panier est vide'}</div>`;
      } else {
        box.innerHTML = cart.map(row=>{
          const p = products.find(x=>x.id===row.id);
          if(!p) return '';
          return `
          <div class="row" data-id="${row.id}">
            <div>
              <div class="name" style="font-weight:800">${p.name}</div>
              <div class="pill" style="margin-top:.2rem">${formatPrice(p.price)} × ${row.qty}</div>
            </div>
            <div class="qty" style="display:flex;align-items:center;gap:.4rem">
              <button class="icon-btn" data-act="dec">➖</button>
              <strong>${row.qty}</strong>
              <button class="icon-btn" data-act="inc">➕</button>
              <button class="icon-btn" data-act="del" title="${currentLang==='ar'?'حذف':'Supprimer'}">🗑</button>
            </div>
          </div>`;
        }).join('');
      }

      const { total, discount, grand } = calcCartTotal();
      $('#cartTotal').textContent = formatPrice(grand);

      $$('#cartItems .row .icon-btn').forEach(btn=>{
        btn.addEventListener('click', ()=>{
          const rowEl = btn.closest('.row');
          const id = rowEl.getAttribute('data-id');
          const act = btn.getAttribute('data-act');
          const idx = cart.findIndex(x=>x.id===id);
          if(idx === -1) return;
          if(act === 'inc') cart[idx].qty++;
          if(act === 'dec') cart[idx].qty = Math.max(1, cart[idx].qty - 1);
          if(act === 'del') cart.splice(idx,1);
          saveLS(LS_KEYS.CART, cart);
          updateCartCount(); renderCart();
        });
      });
    }

    // ========================= Coupon & Cart Actions =========================
    $('#applyCoupon').addEventListener('click', ()=>{
      const code = ($('#couponInput').value || '').trim().toUpperCase();
      if(!code) return toast(currentLang==='ar'?'أدخل الكود':'Entrez le code');
      const c = coupons.find(x=>x.code.toUpperCase()===code && x.active);
      if(!c){ appliedCoupon = null; toast(currentLang==='ar'?'كوبون غير صالح':'Code invalide'); renderCart(); return; }
      appliedCoupon = c; toast(currentLang==='ar'?'تم تطبيق الخصم':'Remise appliquée'); renderCart();
    });

    $('#clearCart').addEventListener('click', ()=>{
      cart = []; saveLS(LS_KEYS.CART, cart); appliedCoupon = null; $('#couponInput').value=''; updateCartCount(); renderCart();
    });

    $('#openCart').addEventListener('click', ()=>{ toast(currentLang==='ar'?'تم فتح السلة على اليمين':'Panier ouvert à droite'); });

    function openCheckout(){
      if(!cart.length) return toast(currentLang==='ar'?'السلة فارغة':'Panier vide');
      const { total, discount, grand } = calcCartTotal();
      const lines = cart.map(row=>{
        const p = products.find(x=>x.id===row.id);
        return p ? `• ${p.name} × ${row.qty} = ${formatPrice(p.price * row.qty)}` : '';
      }).filter(Boolean);
      const header = currentLang==='ar' ? 'طلب جديد من تطبيق Fast Phone' : 'Nouvelle commande depuis Fast Phone';
      const totLine = `${currentLang==='ar'?'المجموع':'Total'}: ${formatPrice(total)}`;
      const discLine = discount ? `\n${currentLang==='ar'?'الخصم':'Remise'}: -${formatPrice(discount)}` : '';
      const grandLine = `\n${currentLang==='ar'?'الإجمالي بعد الخصم':'Total à payer'}: ${formatPrice(grand)}`;
      const note = currentLang==='ar'?'من فضلك أكدوا التوفر والموعد.':'Merci de confirmer la disponibilité et le délai.';
      const msg = `${header}\n\n${lines.join('\n')}\n\n${totLine}${discLine}${grandLine}\n\n${note}`;

      let url = '';
      if(OWNER_CHAT.type === 'whatsapp'){ const phone = (OWNER_CHAT.phone||'').replace(/[^\d]/g,''); url = `https://wa.me/${phone}?text=${encodeURIComponent(msg)}`; }
      else if(OWNER_CHAT.type === 'telegram'){ url = `https://t.me/${OWNER_CHAT.telegramUser}?text=${encodeURIComponent(msg)}`; }
      else if(OWNER_CHAT.type === 'messenger'){ url = `https://m.me/${OWNER_CHAT.messengerUser}?text=${encodeURIComponent(msg)}`; }
      else { const phone = (OWNER_CHAT.phone||'').replace(/[^\d]/g,''); url = `https://wa.me/${phone}?text=${encodeURIComponent(msg)}`; }

      window.open(url, '_blank');
    }
    $('#checkoutBtn').addEventListener('click', openCheckout);

    // ========================= Filters & Search =========================
    $('#searchInput').addEventListener('input', ()=>renderCatalog());
    $('#clearSearch').addEventListener('click', ()=>{ $('#searchInput').value=''; renderCatalog(); });
    $('#sortSelect').addEventListener('change', renderCatalog);
    $('#filterInStock').addEventListener('click', (e)=>{ e.currentTarget.classList.toggle('active'); renderCatalog(); });
    $('#resetFilters').addEventListener('click', ()=>{ $('#sortSelect').value='pop'; $('#filterInStock').classList.remove('active'); $('#searchInput').value=''; renderCatalog(); });

    // ========================= Theme & Language =========================
    function setTheme(mode){
      if(mode === 'light') document.body.classList.add('light'); else document.body.classList.remove('light');
      localStorage.setItem(LS_KEYS.THEME, mode); $('#themeIcon').textContent = mode === 'light' ? '☀️' : '🌙';
    }
    function toggleTheme(){ const cur = localStorage.getItem(LS_KEYS.THEME) || 'dark'; setTheme(cur === 'dark' ? 'light' : 'dark'); }
    $('#themeBtn').addEventListener('click', toggleTheme);
    setTheme(localStorage.getItem(LS_KEYS.THEME) || 'dark');

    function applyI18n(){
      const dict = I18N[currentLang] || I18N.ar;
      $$('[data-i18n]').forEach(el => { const key = el.getAttribute('data-i18n'); if(dict[key]) el.textContent = dict[key]; });
      $$('[data-i18n-placeholder]').forEach(el => { const key = el.getAttribute('data-i18n-placeholder'); if(dict[key]) el.placeholder = dict[key]; });
      $$('option[data-i18n]').forEach(el => { const key = el.getAttribute('data-i18n'); if(dict[key]) el.textContent = dict[key]; });
      document.documentElement.lang = currentLang; document.documentElement.dir = currentLang === 'ar' ? 'rtl' : 'ltr';
      $('#langLabel').textContent = currentLang === 'ar' ? 'العربية' : 'Français';
      updateCartCount(); renderCatalog(); renderServices();
    }
    function setLang(lang){ currentLang = lang; localStorage.setItem(LS_KEYS.LANG, lang); applyI18n(); }

    $('#langBtn').addEventListener('click', ()=> setLang(currentLang === 'ar' ? 'fr' : 'ar'));

    // ========================= Footer Year =========================
    $('#year').textContent = new Date().getFullYear();

    // ========================= Auth (Simulation) =========================
    let currentUser = null;
    function refreshUserUI(){
      if(currentUser){
        $('#loginBtn').style.display = 'none';
        $('#userMenu').style.display = 'inline-flex';
        $('#userName').textContent = currentUser.email;
        $('#userAvatar').src = currentUser.photoURL || 'https://i.pravatar.cc/64?img=12';
        $('#ownerEmailBadge').textContent = `${currentLang==='ar'?'حساب المالك:':'Propriétaire :'} ${OWNER_EMAIL}`;
      } else {
        $('#loginBtn').style.display = 'inline-flex';
        $('#userMenu').style.display = 'none';
        $('#ownerEmailBadge').textContent = '—';
      }
    }
    $('#loginBtn').addEventListener('click', ()=>{
      const email = prompt(currentLang==='ar'?'أدخل بريدك الإلكتروني (محاكاة)':'Entrez votre email (simulation)');
      if(!email) return;
      currentUser = { email, photoURL: '' };
      refreshUserUI(); toast(currentLang==='ar'?'تم تسجيل الدخول (محاكاة)':'Connecté (simulation)');
    });
    $('#logoutBtn').addEventListener('click', ()=>{ currentUser = null; refreshUserUI(); toast(currentLang==='ar'?'تم تسجيل الخروج':'Déconnecté'); });
    function isOwner(){ return currentUser && currentUser.email && currentUser.email.toLowerCase() === OWNER_EMAIL.toLowerCase(); }

    // ========================= Owner Panel (CRUD) =========================
    const ownerDialog = $('#ownerDialog');
    $('#openOwnerPanel').addEventListener('click', ()=>{
      if(!isOwner()) return toast(currentLang==='ar'?'هذه الميزة للمالك فقط':'Réservé au propriétaire');
      syncSelects(); ownerDialog.showModal();
    });
    $('#closeOwnerDialog').addEventListener('click', ()=> ownerDialog.close());

    function syncSelects(){
      const pSel = $('#productSelect');
      pSel.innerHTML = products.map(p => `<option value="${p.id}">${p.name}</option>`).join('');
      const sSel = $('#serviceSelect');
      sSel.innerHTML = services.map(s => `<option value="${s.id}">${s.title}</option>`).join('');
      const cSel = $('#couponSelect');
      cSel.innerHTML = coupons.map(c => `<option value="${c.code}">${c.code} — ${c.percent}% ${c.active ? '✓' : '✗'}</option>`).join('');
    }

    $('#addProduct').addEventListener('click', ()=>{
      if(!isOwner()) return;
      const item = {
        id: uid('p'),
        name: $('#pName').value.trim(),
        price: Number($('#pPrice').value || 0),
        oldPrice: Number($('#pOldPrice').value || 0),
        stock: Number($('#pStock').value || 0),
        image: $('#pImage').value.trim() || 'https://images.unsplash.com/photo-1511707171634-5f897ff02aa9?auto=format&fit=crop&w=800&q=60',
        category: $('#pCategory').value,
        pop: 0,
        createdAt: Date.now()
      };
      if(!item.name) return toast(currentLang==='ar'?'أدخل اسم المنتج':'Nom requis');
      products.push(item); saveLS(LS_KEYS.PRODUCTS, products); renderCatalog(); syncSelects(); toast(currentLang==='ar'?'تمت الإضافة':'Ajouté');
    });

    $('#updateProduct').addEventListener('click', ()=>{
      if(!isOwner()) return;
      const id = $('#productSelect').value; const p = products.find(x=>x.id===id); if(!p) return;
      p.name = $('#pName').value.trim() || p.name;
      p.price = Number($('#pPrice').value || p.price);
      p.oldPrice = Number($('#pOldPrice').value || p.oldPrice);
      p.stock = Number($('#pStock').value || p.stock);
      p.image = $('#pImage').value.trim() || p.image;
      p.category = $('#pCategory').value || p.category;
      saveLS(LS_KEYS.PRODUCTS, products); renderCatalog(); syncSelects(); toast(currentLang==='ar'?'تم التعديل':'Mis à jour');
    });

    $('#deleteProduct').addEventListener('click', ()=>{
      if(!isOwner()) return;
      const id = $('#productSelect').value; const idx = products.findIndex(x=>x.id===id); if(idx===-1) return;
      products.splice(idx,1); saveLS(LS_KEYS.PRODUCTS, products); renderCatalog(); syncSelects(); toast(currentLang==='ar'?'تم الحذف':'Supprimé');
    });

    // Services CRUD
    $('#addService').addEventListener('click', ()=>{
      if(!isOwner()) return;
      const s = { id: uid('s'), title: $('#sTitle').value.trim(), desc: $('#sDesc').value.trim(), price: Number($('#sPrice').value || 0) };
      if(!s.title) return toast(currentLang==='ar'?'أدخل عنوان الخدمة':'Titre requis');
      services.push(s); saveLS(LS_KEYS.SERVICES, services); renderServices(); syncSelects(); toast(currentLang==='ar'?'تمت الإضافة':'Ajouté');
    });
    $('#updateService').addEventListener('click', ()=>{
      if(!isOwner()) return;
      const id = $('#serviceSelect').value; const s = services.find(x=>x.id===id); if(!s) return;
      s.title = $('#sTitle').value.trim() || s.title; s.desc = $('#sDesc').value.trim() || s.desc; s.price = Number($('#sPrice').value || s.price);
      saveLS(LS_KEYS.SERVICES, services); renderServices(); syncSelects(); toast(currentLang==='ar'?'تم التعديل':'Mis à jour');
    });
    $('#deleteService').addEventListener('click', ()=>{
      if(!isOwner()) return;
      const id = $('#serviceSelect').value; const idx = services.findIndex(x=>x.id===id); if(idx===-1) return;
      services.splice(idx,1); saveLS(LS_KEYS.SERVICES, services); renderServices(); syncSelects(); toast(currentLang==='ar'?'تم الحذف':'Supprimé');
    });

    // Coupons CRUD
    $('#addCoupon').addEventListener('click', ()=>{
      if(!isOwner()) return;
      const c = { code: ($('#cCode').value || '').trim(), percent: Number($('#cPercent').value || 0), active: $('#cActive').value === 'true' };
      if(!c.code) return toast(currentLang==='ar'?'أدخل الكود':'Code requis');
      const exists = coupons.find(x=>x.code.toUpperCase()===c.code.toUpperCase());
      if(exists){ exists.percent = c.percent; exists.active = c.active; } else coupons.push(c);
      saveLS(LS_KEYS.COUPONS, coupons); syncSelects(); toast(currentLang==='ar'?'تم الحفظ':'Enregistré');
    });

    $('#deleteCoupon').addEventListener('click', ()=>{
      if(!isOwner()) return;
      const val = $('#couponSelect').value; const idx = coupons.findIndex(x=>x.code===val); if(idx===-1) return;
      coupons.splice(idx,1); saveLS(LS_KEYS.COUPONS, coupons); syncSelects(); toast(currentLang==='ar'?'تم الحذف':'Supprimé');
    });

    // Export/Import (backup/restore)
    $('#backupBtn').addEventListener('click', ()=>{
      const data = { products, services, coupons };
      const blob = new Blob([JSON.stringify(data, null, 2)], { type:'application/json' });
      const a = document.createElement('a'); a.href = URL.createObjectURL(blob);
      a.download = `fastphone-backup-${new Date().toISOString().slice(0,10)}.json`; a.click();
    });

    $('#restoreBtn').addEventListener('click', ()=> $('#importFile').click());
    $('#importBtn').addEventListener('click', ()=> $('#importFile').click());

    $('#importFile').addEventListener('change', async (e)=>{
      const file = e.target.files[0]; if(!file) return;
      const text = await file.text();
      try{
        const data = JSON.parse(text);
        if(Array.isArray(data.products)){ products = data.products; saveLS(LS_KEYS.PRODUCTS, products); }
        if(Array.isArray(data.services)){ services = data.services; saveLS(LS_KEYS.SERVICES, services); }
        if(Array.isArray(data.coupons)){ coupons = data.coupons; saveLS(LS_KEYS.COUPONS, coupons); }
        renderCatalog(); renderServices(); syncSelects(); toast(currentLang==='ar'?'تم الاستيراد':'Importé');
      }catch{
        toast(currentLang==='ar'?'ملف غير صالح':'Fichier invalide');
      }finally{ e.target.value=''; }
    });

    // ========================= Init =========================
    applyI18n(); renderCatalog(); renderServices(); renderCart(); refreshUserUI();
  </script>
</body>
</html>
