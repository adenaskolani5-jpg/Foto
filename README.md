<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>PasirPogorCell - Daftar Barang</title>
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet" />
    <style>
        /* ===== RESET & BASE ===== */
        * { margin:0; padding:0; box-sizing:border-box; }
        body {
            font-family:'Inter',-apple-system,BlinkMacSystemFont,sans-serif;
            min-height:100vh;
            display:flex;
            justify-content:center;
            align-items:flex-start;
            padding:0 20px 80px;
            background: linear-gradient(145deg, #0b2b1e 0%, #1a5a4a 30%, #1e6b7a 60%, #1a4a5a 100%);
            background-attachment: fixed;
        }
        body::before {
            content: '';
            position: fixed;
            top:0; left:0; width:100%; height:100%;
            background: radial-gradient(circle at 20% 30%, rgba(255,255,255,0.06) 0%, transparent 60%),
                        radial-gradient(circle at 80% 70%, rgba(0,255,200,0.04) 0%, transparent 50%);
            pointer-events: none;
            z-index:0;
        }
        .container {
            max-width:1240px;
            width:100%;
            margin:0 auto;
            position:relative;
            z-index:1;
        }

        /* ===== HEADER ===== */
        .header {
            text-align:center;
            padding:32px 0 28px;
            margin-bottom:32px;
            background: rgba(255,255,255,0.08);
            backdrop-filter: blur(12px);
            border-radius:20px;
            border:1px solid rgba(255,255,255,0.12);
            box-shadow:0 8px 32px rgba(0,0,0,0.2);
        }
        .header .logo {
            font-size:32px;
            font-weight:800;
            letter-spacing:-0.5px;
            color:#fff;
            text-shadow:0 2px 16px rgba(0,0,0,0.2);
        }
        .header .logo span { color:#7ae9c0; }
        .header .sub {
            font-size:15px;
            color:rgba(255,255,255,0.8);
            margin-top:2px;
            font-weight:400;
        }
        .header .info-row {
            display:flex;
            flex-wrap:wrap;
            justify-content:center;
            gap:12px 20px;
            margin-top:12px;
        }
        .header .info-badge {
            display:inline-flex;
            align-items:center;
            gap:6px;
            background:rgba(255,255,255,0.12);
            color:#fff;
            font-weight:500;
            font-size:13px;
            padding:5px 16px;
            border-radius:40px;
            backdrop-filter:blur(4px);
            border:1px solid rgba(255,255,255,0.08);
        }
        .header .info-badge .jam-icon { font-size:15px; }
        .header .btn-group {
            display:flex;
            flex-wrap:wrap;
            justify-content:center;
            gap:10px;
            margin-top:14px;
        }
        .header .wa-link, .header .order-link {
            display:inline-flex;
            align-items:center;
            gap:8px;
            color:#fff;
            font-weight:600;
            font-size:14px;
            padding:10px 28px;
            border-radius:40px;
            text-decoration:none;
            transition:0.2s;
            border:none;
            cursor:pointer;
            font-family:inherit;
        }
        .header .wa-link {
            background:#25d366;
            box-shadow:0 4px 14px rgba(37,211,102,0.35);
        }
        .header .wa-link:hover { background:#1ebe5c; transform:scale(1.02); }
        .header .order-link {
            background:linear-gradient(135deg, #f59e0b, #d97706);
            box-shadow:0 4px 14px rgba(245,158,11,0.35);
        }
        .header .order-link:hover { transform:scale(1.02); opacity:0.9; }

        /* ===== CONTROLS ===== */
        .controls {
            display:flex;
            flex-wrap:wrap;
            gap:14px;
            align-items:center;
            justify-content:space-between;
            margin-bottom:28px;
            background:rgba(255,255,255,0.85);
            backdrop-filter:blur(12px);
            padding:14px 20px;
            border-radius:16px;
            box-shadow:0 4px 20px rgba(0,0,0,0.08);
            border:1px solid rgba(255,255,255,0.3);
        }
        .controls-left { display:flex; flex-wrap:wrap; gap:12px; align-items:center; flex:1; }
        .controls-right { display:flex; flex-wrap:wrap; gap:10px; align-items:center; }
        .search-box { position:relative; flex:1; min-width:200px; max-width:340px; }
        .search-box input {
            width:100%;
            padding:10px 16px 10px 42px;
            border:1.5px solid #e2e6ec;
            border-radius:10px;
            font-size:14px;
            font-family:inherit;
            background:#f8f9fb;
            transition:0.2s;
            color:#1a2634;
            outline:none;
        }
        .search-box input:focus {
            border-color:#1a7a4a;
            background:#fff;
            box-shadow:0 0 0 3px rgba(26,122,74,0.15);
        }
        .search-box .icon {
            position:absolute;
            left:14px;
            top:50%;
            transform:translateY(-50%);
            color:#8a9bb5;
            font-size:16px;
            pointer-events:none;
        }
        .filter-group { display:flex; flex-wrap:wrap; gap:6px; }
        .filter-group .filter-btn {
            padding:8px 16px;
            border:1.5px solid #dce0e6;
            border-radius:30px;
            background:transparent;
            font-size:12px;
            font-weight:600;
            color:#3a4a5a;
            cursor:pointer;
            transition:0.2s;
            font-family:inherit;
            letter-spacing:0.3px;
            text-transform:uppercase;
        }
        .filter-group .filter-btn:hover { border-color:#1a7a4a; color:#1a7a4a; }
        .filter-group .filter-btn.active { background:#1a7a4a; border-color:#1a7a4a; color:#fff; }
        .filter-select {
            padding:8px 14px;
            border:1.5px solid #dce0e6;
            border-radius:30px;
            background:#f8f9fb;
            font-size:12px;
            font-weight:500;
            color:#1a2634;
            font-family:inherit;
            outline:none;
            cursor:pointer;
            transition:0.2s;
        }
        .filter-select:focus { border-color:#1a7a4a; }
        .filter-select:hover { border-color:#1a7a4a; }
        .result-info {
            font-size:13px;
            color:rgba(255,255,255,0.9);
            text-align:center;
            margin-bottom:18px;
            font-weight:500;
            text-shadow:0 1px 8px rgba(0,0,0,0.15);
        }

        /* ===== PRODUCT GRID ===== */
        .product-grid { display:grid; grid-template-columns:repeat(auto-fill,minmax(240px,1fr)); gap:24px; }

        /* ===== PRODUCT CARD ===== */
        .product-card {
            background:rgba(255,255,255,0.92);
            backdrop-filter:blur(8px);
            border-radius:16px;
            overflow:hidden;
            box-shadow:0 4px 20px rgba(0,0,0,0.08);
            transition:transform 0.25s,box-shadow 0.3s;
            border:1px solid rgba(255,255,255,0.3);
            display:flex;
            flex-direction:column;
            position:relative;
        }
        .product-card:hover {
            transform:translateY(-6px);
            box-shadow:0 16px 40px rgba(0,0,0,0.15);
            background:rgba(255,255,255,0.98);
        }
        .product-number {
            position:absolute;
            top:10px;
            right:10px;
            background:rgba(0,0,0,0.55);
            color:#fff;
            font-size:11px;
            font-weight:700;
            padding:2px 10px;
            border-radius:20px;
            z-index:2;
            letter-spacing:0.5px;
            backdrop-filter:blur(4px);
        }
        .product-image {
            width:100%;
            aspect-ratio:1/1;
            background:#f0f3f7;
            display:flex;
            align-items:center;
            justify-content:center;
            overflow:hidden;
            position:relative;
        }
        .product-image img {
            width:100%;
            height:100%;
            object-fit:cover;
            transition:transform 0.4s;
        }
        .product-card:hover .product-image img { transform:scale(1.04); }
        .product-image .badge {
            position:absolute;
            top:12px;
            left:12px;
            font-size:10px;
            font-weight:700;
            text-transform:uppercase;
            letter-spacing:0.5px;
            padding:4px 14px;
            border-radius:30px;
            color:#fff;
            z-index:1;
            box-shadow:0 2px 8px rgba(0,0,0,0.15);
        }
        .badge-stok { background:#1a7a4a; }
        .badge-habis { background:#94a3b8; }
        .badge-hot { background:#f59e0b; }

        .product-info { padding:16px 18px 18px; flex:1; display:flex; flex-direction:column; }
        .product-name { font-size:15px; font-weight:700; color:#0b1a2a; line-height:1.3; margin-bottom:2px; }
        .product-category { font-size:12px; color:#7a8a9a; font-weight:500; margin-bottom:8px; }
        .product-price-row { display:flex; align-items:baseline; gap:8px; flex-wrap:wrap; margin-top:auto; }
        .product-price { font-size:20px; font-weight:800; color:#0b2b1e; }
        .product-price .currency { font-size:13px; font-weight:600; color:#5e6f8d; }

        .product-stok { font-size:12px; font-weight:600; display:flex; align-items:center; gap:6px; margin-top:6px; }
        .product-stok .stok-angka { font-weight:700; }
        .product-stok .stok-tersedia { color:#1a7a4a; }
        .product-stok .stok-habis { color:#94a3b8; }

        .product-action { display:flex; gap:8px; margin-top:14px; }
        .btn-detail, .btn-wa {
            flex:1;
            padding:10px 0;
            border:none;
            border-radius:10px;
            font-size:12px;
            font-weight:700;
            font-family:inherit;
            cursor:pointer;
            transition:0.2s;
            text-align:center;
            text-decoration:none;
            letter-spacing:0.3px;
            text-transform:uppercase;
        }
        .btn-detail { background:#eef1f5; color:#1a2634; }
        .btn-detail:hover { background:#dce0e6; }
        .btn-wa { background:#25d366; color:#fff; }
        .btn-wa:hover { background:#1ebe5c; }

        /* ===== MODAL ===== */
        .modal-overlay {
            position:fixed;
            top:0; left:0;
            width:100%; height:100%;
            background:rgba(0,0,0,0.55);
            backdrop-filter:blur(8px);
            display:none;
            align-items:center;
            justify-content:center;
            z-index:1000;
            padding:20px;
        }
        .modal-overlay.active { display:flex; }
        .modal {
            background:#fff;
            max-width:560px;
            width:100%;
            border-radius:24px;
            padding:32px 30px 30px;
            box-shadow:0 40px 80px rgba(0,0,0,0.3);
            position:relative;
            max-height:92vh;
            overflow-y:auto;
        }
        .modal-close {
            position:absolute;
            top:14px;
            right:18px;
            font-size:28px;
            background:none;
            border:none;
            cursor:pointer;
            color:#8a9bb5;
            transition:0.2s;
            line-height:1;
        }
        .modal-close:hover { color:#1a2634; }
        .modal-image {
            width:100%;
            aspect-ratio:1/1;
            object-fit:contain;
            border-radius:12px;
            background:#f8f9fb;
            margin-bottom:16px;
        }
        .modal-name { font-size:22px; font-weight:800; color:#0b1a2a; margin-bottom:2px; }
        .modal-category { font-size:14px; color:#8a9bb5; font-weight:500; margin-bottom:6px; }
        .modal-price { font-size:28px; font-weight:800; color:#0b2b1e; margin:6px 0 12px; }
        .modal-price .currency { font-size:16px; font-weight:600; color:#5e6f8d; }
        .modal-stok { font-size:15px; font-weight:600; display:flex; align-items:center; gap:8px; margin-bottom:14px; }
        .modal-stok .stok-angka { font-weight:800; }
        .modal-stok .stok-tersedia { color:#1a7a4a; }
        .modal-stok .stok-habis { color:#94a3b8; }
        .modal-desc {
            background:#f8f9fb;
            border-radius:12px;
            padding:14px 18px;
            margin:12px 0 20px;
            color:#1a2634;
            font-size:14px;
            line-height:1.7;
            border-left:4px solid #1a7a4a;
        }
        .modal-desc:empty::before { content:"Tidak ada keterangan tambahan."; color:#aab3c9; font-style:italic; }
        .modal-wa {
            display:inline-flex;
            align-items:center;
            gap:10px;
            background:#25d366;
            color:#fff;
            font-weight:700;
            font-size:14px;
            padding:12px 30px;
            border-radius:40px;
            text-decoration:none;
            transition:0.2s;
            border:none;
            cursor:pointer;
            font-family:inherit;
        }
        .modal-wa:hover { background:#1ebe5c; }
        .modal-copy-btn {
            display:inline-flex;
            align-items:center;
            gap:8px;
            background:#f0f2f5;
            color:#1a2634;
            font-weight:600;
            font-size:13px;
            padding:10px 20px;
            border-radius:40px;
            text-decoration:none;
            transition:0.2s;
            border:none;
            cursor:pointer;
            font-family:inherit;
            margin-top:10px;
        }
        .modal-copy-btn:hover { background:#e2e6ec; }

        /* ===== ORDER MODAL ===== */
        .order-modal .modal {
            max-width:600px;
        }
        .order-modal .modal-title {
            font-size:24px;
            font-weight:800;
            color:#0b2b1e;
            margin-bottom:6px;
            display:flex;
            align-items:center;
            gap:10px;
        }
        .order-modal .modal-title span { font-size:28px; }
        .order-modal .modal-sub {
            color:#5e6f8d;
            font-size:14px;
            margin-bottom:20px;
        }
        .order-modal .order-rules {
            background: #fef9e7;
            border-left:4px solid #f59e0b;
            padding:14px 18px;
            border-radius:8px;
            margin-bottom:20px;
            font-size:13px;
            line-height:1.7;
            color:#1a2634;
        }
        .order-modal .order-rules strong { color:#d97706; }
        .order-modal .form-group {
            margin-bottom:16px;
        }
        .order-modal .form-group label {
            display:block;
            font-size:13px;
            font-weight:600;
            color:#1a2634;
            margin-bottom:4px;
        }
        .order-modal .form-group label .required {
            color:#dc3545;
            margin-left:2px;
        }
        .order-modal .form-group input,
        .order-modal .form-group textarea,
        .order-modal .form-group select {
            width:100%;
            padding:10px 14px;
            border:1.5px solid #e2e6ec;
            border-radius:10px;
            font-size:14px;
            font-family:inherit;
            background:#f8f9fb;
            transition:0.2s;
            color:#1a2634;
            outline:none;
        }
        .order-modal .form-group input:focus,
        .order-modal .form-group textarea:focus,
        .order-modal .form-group select:focus {
            border-color:#1a7a4a;
            background:#fff;
            box-shadow:0 0 0 3px rgba(26,122,74,0.12);
        }
        .order-modal .form-group textarea {
            resize:vertical;
            min-height:80px;
        }
        .order-modal .form-row {
            display:grid;
            grid-template-columns:1fr 1fr;
            gap:14px;
        }
        .order-modal .btn-submit {
            width:100%;
            padding:14px;
            background:linear-gradient(135deg, #f59e0b, #d97706);
            color:#fff;
            font-weight:700;
            font-size:15px;
            border:none;
            border-radius:12px;
            cursor:pointer;
            transition:0.2s;
            font-family:inherit;
            box-shadow:0 4px 14px rgba(245,158,11,0.35);
            margin-top:6px;
        }
        .order-modal .btn-submit:hover { transform:scale(1.01); opacity:0.9; }
        .order-modal .btn-submit:disabled {
            opacity:0.6;
            cursor:not-allowed;
            transform:none;
        }
        .order-modal .form-hint {
            font-size:12px;
            color:#8a9bb5;
            margin-top:4px;
        }
        @media (max-width:520px) {
            .order-modal .form-row { grid-template-columns:1fr; }
        }

        /* ===== WA FLOAT ===== */
        .wa-float {
            position:fixed;
            bottom:24px;
            right:24px;
            background:#25d366;
            color:#fff;
            width:58px;
            height:58px;
            border-radius:50%;
            display:flex;
            align-items:center;
            justify-content:center;
            box-shadow:0 6px 24px rgba(37,211,102,0.4);
            transition:transform 0.2s;
            text-decoration:none;
            z-index:999;
        }
        .wa-float:hover { transform:scale(1.08); }
        .wa-float svg { width:30px; height:30px; fill:#fff; }

        /* ===== FOOTER ===== */
        .footer {
            margin-top:48px;
            padding:28px 20px;
            border-radius:16px;
            background:rgba(255,255,255,0.06);
            backdrop-filter:blur(8px);
            border:1px solid rgba(255,255,255,0.08);
            text-align:center;
            font-size:13px;
            color:rgba(255,255,255,0.8);
        }
        .footer strong { color:#fff; }
        .footer .wa-link { color:#7ae9c0; font-weight:600; text-decoration:none; }
        .footer .wa-link:hover { text-decoration:underline; color:#aaffdd; }
        .footer .jam-footer {
            display:block;
            margin-top:4px;
            font-size:13px;
            color:rgba(255,255,255,0.7);
            letter-spacing:0.5px;
        }
        .footer .jam-footer .jam-icon { font-size:14px; }

        /* ===== RESPONSIVE ===== */
        @media (max-width:768px) {
            .controls { flex-direction:column; align-items:stretch; padding:14px 16px; }
            .controls-left { flex-direction:column; align-items:stretch; }
            .controls-right { justify-content:center; }
            .search-box { max-width:100%; }
            .filter-group { justify-content:center; }
            .product-grid { grid-template-columns:repeat(auto-fill,minmax(160px,1fr)); gap:16px; }
            .product-name { font-size:13px; }
            .product-price { font-size:17px; }
            .modal { padding:24px 18px; }
            .modal-name { font-size:19px; }
            .modal-price { font-size:24px; }
            .header .logo { font-size:26px; }
            .product-number { font-size:10px; padding:2px 8px; }
            .header { padding:24px 16px; }
            .header .btn-group { flex-direction:column; align-items:center; }
            .header .wa-link, .header .order-link { width:100%; justify-content:center; max-width:320px; }
        }
        @media (max-width:480px) {
            .product-grid { grid-template-columns:1fr 1fr; gap:12px; }
            .product-info { padding:12px 12px 14px; }
            .product-action { flex-direction:column; gap:6px; }
            .btn-detail, .btn-wa { padding:8px 0; font-size:11px; }
            .filter-group .filter-btn { padding:6px 12px; font-size:10px; }
            .filter-select { font-size:10px; padding:6px 12px; }
            .header { padding:20px 12px; }
            .header .logo { font-size:22px; }
            .product-number { font-size:9px; padding:1px 7px; top:6px; right:6px; }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- ===== HEADER ===== -->
        <header class="header">
            <div class="logo">Pasir<span>Pogor</span>Cell</div>
            <p class="sub">Elektronik · Aksesoris · Alat Tulis · Perlengkapan Kantor</p>
            <div class="info-row">
                <span class="info-badge"><span class="jam-icon">🕐</span> 06.30 - 21.30 WIB</span>
                <span class="info-badge">📱 0838-4484-3020</span>
            </div>
            <div class="btn-group">
                <a href="https://wa.me/6283844843020" target="_blank" class="wa-link">💬 Chat via WhatsApp</a>
                <button class="order-link" id="openOrderBtn">📦 Pesan Barang</button>
            </div>
        </header>

        <!-- ===== CONTROLS ===== -->
        <div class="controls">
            <div class="controls-left">
                <div class="search-box">
                    <span class="icon">🔍</span>
                    <input type="text" id="searchInput" placeholder="Cari barang..." />
                </div>
                <div class="filter-group" id="filterGroup">
                    <button class="filter-btn active" data-filter="Semua">Semua</button>
                    <button class="filter-btn" data-filter="Elektronik">Elektronik</button>
                    <button class="filter-btn" data-filter="Aksesoris">Aksesoris</button>
                    <button class="filter-btn" data-filter="Alat Tulis">Alat Tulis</button>
                    <button class="filter-btn" data-filter="Perlengkapan Kantor">Perlengkapan</button>
                </div>
            </div>
            <div class="controls-right">
                <select class="filter-select" id="sortSelect">
                    <option value="default">Urutkan</option>
                    <option value="asc">Termurah</option>
                    <option value="desc">Termahal</option>
                </select>
                <select class="filter-select" id="stokFilter">
                    <option value="semua">Semua Stok</option>
                    <option value="tersedia">Tersedia</option>
                    <option value="habis">Habis</option>
                </select>
            </div>
        </div>

        <div class="result-info" id="resultInfo">Menampilkan 0 barang</div>

        <!-- ===== PRODUCT GRID ===== -->
        <div class="product-grid" id="productGrid"></div>

        <!-- ===== FOOTER ===== -->
        <footer class="footer">
            <strong>PasirPogorCell</strong> — 
            WA: <a href="https://wa.me/6283844843020" target="_blank" class="wa-link">0838-4484-3020</a>
            <span class="jam-footer"><span class="jam-icon">🕐</span> Jam Operasional: 06.30 - 21.30 WIB</span>
        </footer>
    </div>

    <!-- ===== WA FLOAT ===== -->
    <a href="https://wa.me/6283844843020" target="_blank" class="wa-float" aria-label="Hubungi WhatsApp">
        <svg viewBox="0 0 24 24"><path d="M12.032 21.965c-2.007 0-3.866-.61-5.398-1.65l-4.23 1.388 1.426-4.148c-1.2-1.723-1.916-3.822-1.916-6.088 0-5.854 4.763-10.618 10.618-10.618 5.854 0 10.618 4.763 10.618 10.618 0 5.855-4.764 10.618-10.618 10.618zm0-19.236c-4.755 0-8.618 3.864-8.618 8.618 0 1.782.543 3.434 1.47 4.805l-.947 2.756 2.827-.928c1.314.846 2.904 1.344 4.618 1.344 4.755 0 8.618-3.864 8.618-8.618 0-4.754-3.863-8.618-8.618-8.618zm4.998 11.493c-.146-.246-.537-.394-.922-.437-.384-.043-.884-.04-1.142.054-.258.095-.462.338-.568.588-.106.25-.406.434-.69.324-.284-.11-1.16-.427-2.218-1.37-.82-.732-1.375-1.634-1.536-1.91-.16-.276-.017-.426.12-.563.123-.123.274-.321.411-.482.138-.16.184-.274.276-.457.092-.183.046-.343-.023-.48-.069-.137-.6-1.444-.822-1.978-.216-.52-.438-.433-.6-.44-.154-.008-.33-.01-.506-.01-.176 0-.462.066-.704.33-.242.264-.924.903-.924 2.203 0 1.3.946 2.557 1.078 2.734.132.177 1.86 2.84 4.506 3.984.63.272 1.12.435 1.504.556.632.201 1.207.173 1.662.105.507-.076 1.562-.638 1.782-1.254.22-.616.22-1.144.154-1.254z"/></svg>
    </a>

    <!-- ===== MODAL DETAIL ===== -->
    <div class="modal-overlay" id="modalOverlay">
        <div class="modal">
            <button class="modal-close" id="modalClose">&times;</button>
            <img class="modal-image" id="modalImage" src="" alt="Produk" />
            <div class="modal-name" id="modalName"></div>
            <div class="modal-category" id="modalCategory"></div>
            <div class="modal-price" id="modalPrice"></div>
            <div class="modal-stok" id="modalStok"></div>
            <div class="modal-desc" id="modalDescription"></div>
            <a href="#" id="modalWaLink" target="_blank" class="modal-wa">💬 Tanya via WhatsApp</a>
            <button class="modal-copy-btn" id="modalCopyBtn">📋 Salin Nama Barang</button>
        </div>
    </div>

    <!-- ===== MODAL PESAN BARANG ===== -->
    <div class="modal-overlay order-modal" id="orderModal">
        <div class="modal">
            <button class="modal-close" id="orderModalClose">&times;</button>
            <div class="modal-title"><span>📦</span> Pesan Barang</div>
            <div class="modal-sub">Mau pesan barang yang tidak tersedia? Kami bantu carikan!</div>
            
            <div class="order-rules">
                <strong>📋 Ketentuan Pre-Order:</strong><br />
                • ⏳ Waktu tunggu <strong>3-7 hari</strong> setelah order<br />
                • 💰 Pembayaran <strong>di muka (full)</strong> — tunai atau transfer<br />
                • ✅ Garansi barang jika tidak sesuai — <strong>tanpa repot</strong> mengembalikan sendiri<br />
                • 🛡️ Jaminan kualitas dari PasirPogorCell<br />
                • 📦 Bisa pesan <strong>barang apa saja</strong> (random / request)
            </div>

            <form id="orderForm">
                <div class="form-group">
                    <label>Nama Barang yang Dipesan <span class="required">*</span></label>
                    <input type="text" id="orderNamaBarang" placeholder="Contoh: Kipas Angin Miyako 16 inch" required />
                </div>
                <div class="form-group">
                    <label>Spesifikasi / Detail Barang</label>
                    <textarea id="orderSpesifikasi" placeholder="Warna, ukuran, merek, atau keterangan tambahan..."></textarea>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label>Harga yang Diharapkan</label>
                        <input type="number" id="orderHarga" placeholder="Contoh: 50000" />
                        <div class="form-hint">Kosongkan jika biarkan toko yang menentukan</div>
                    </div>
                    <div class="form-group">
                        <label>Jumlah <span class="required">*</span></label>
                        <input type="number" id="orderJumlah" placeholder="Contoh: 2" min="1" value="1" required />
                    </div>
                </div>
                <div class="form-row">
                    <div class="form-group">
                        <label>Nama Anda <span class="required">*</span></label>
                        <input type="text" id="orderNama" placeholder="Nama lengkap" required />
                    </div>
                    <div class="form-group">
                        <label>Nomor WhatsApp <span class="required">*</span></label>
                        <input type="tel" id="orderWa" placeholder="08xxxxxxxxxx" required />
                    </div>
                </div>
                <div class="form-group">
                    <label>Metode Pembayaran <span class="required">*</span></label>
                    <select id="orderMetode" required>
                        <option value="">Pilih metode...</option>
                        <option value="Tunai">Tunai (langsung ke toko)</option>
                        <option value="Transfer Bank">Transfer Bank</option>
                        <option value="E-Wallet">E-Wallet (OVO/DANA/GoPay)</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Catatan Tambahan</label>
                    <textarea id="orderCatatan" placeholder="Informasi lain yang perlu diketahui..."></textarea>
                </div>
                <button type="submit" class="btn-submit" id="orderSubmitBtn">📨 Kirim Pesanan via WhatsApp</button>
            </form>
        </div>
    </div>

    <script>
        // ============================================================
        // 1. DATA GAMBAR
        // ============================================================
        const PRODUK_IMAGES = {
            "Pulpen Amilio 0.5mm": "https://i.ibb.co.com/LTSMxB4/Pulpen-Amilio-0.5mm.jpg",
            "Pulpen Joyko 0.5mm": "https://i.ibb.co.com/60vFnXCG/Pulpen-Joyko-0.5mm.jpg",
            "Charger Robot Micro USB": "https://i.ibb.co.com/xS6JNsnk/Charger-Robot-Micro-USB.jpg",
            "Lem Korea": "https://i.ibb.co.com/GQ4WMsgS/Lem-Korea-Lem-Kertas.jpg",
            "Staples Joyko": "https://i.ibb.co.com/DHjtg2Q4/Staples-Joyko.jpg",
            "Gunting Montana STI 180": "https://i.ibb.co.com/gX2thmN/Gunting-Montana-STI-180.jpg",
            "Gunting Montana STI 165": "https://i.ibb.co.com/bYc6zkp/Gunting-Montana-STI-165.jpg",
            "Gunting Montana STI 145": "https://i.ibb.co.com/j9H3b92c/Gunting-Montana-STI-145.jpg",
            "Pensil Warna JOYKO (12 warna)": "https://i.ibb.co.com/DDw8q98r/Pensil-Warna-JOYKO-12-warna.jpg",
            "Refill Staples MONTANA": "https://i.ibb.co.com/xKQtvGDp/Refill-Staples-MONTANA.jpg",
            "Lakban Bening": "https://i.ibb.co.com/4wTqGbs8/Lakban-Bening.jpg",
            "Kabel Micro USB KIVEE": "https://i.ibb.co.com/0p7G66Jk/Kabel-Micro-USB-KIVEE.jpg",
            "Buku SIDU SKOLA 1 pack (10 buku)": "https://i.ibb.co.com/q39w5Bym/Buku-SIDU-SKOLA-1-pack-5-buku.jpg",
            "Kipas Mini MIISOO": "https://i.ibb.co.com/chNzj1Jj/Kipas-Mini-MIISOO.jpg",
            "Baterai ABC AAA (A3) (harga per 1pcs)": "https://i.ibb.co.com/fGtkYHKf/Baterai-ABC-A3-1-pak-isi-2.jpg",
            "Pulpen Joyko i-Tech 2, 0.28mm": "https://i.ibb.co.com/HT17jcX5/Pulpen-Joyko-i-Tech-2-0.28mm.jpg",
            "Lakban Hitam": "https://i.ibb.co.com/bjJ3ks0k/Lakban-Hitam.jpg",
            "Penghapus Joyko": "https://i.ibb.co.com/M57B1LDm/Penghapus-Joyko.jpg",
            "Buku CAMPUS 1 pack (10 buku)": "https://i.ibb.co.com/n8z4qWXv/Buku-CAMPUS-1-pack-5-buku.jpg",
            "Rautan pensil, JOYKO": "https://i.ibb.co.com/Rpk85fCP/Rautan-Pensil-JOYKO.jpg",
            "JOYKO Pensil P-88 2B": "https://i.ibb.co.com/N6nKxvFz/Pensil-2B-JOYKO.jpg",
            "JOYKO Penanda Berwarna Highlighter HL-88": "https://i.ibb.co.com/XTB3V5P/Penanda-JOYKO.jpg",
            "Deli I-Select Spidol Warna 12 Warna": "https://i.ibb.co.com/1JLJp88t/Spidol-warna-Deli.jpg",
            "Baterai ABC Biru Size AA 1.5V": "https://i.ibb.co.com/PsmqPZqf/Baterai-ABC-AAA.jpg",
            "Lakban Coklat Bening 45mm x 100 Yard": "https://i.ibb.co.com/27qNd9gH/Lakban-Coklat.jpg"
        };

        // ============================================================
        // 2. DATA PRODUK
        // ============================================================
        const PRODUK_DATA = {
            "Elektronik": [
                { nama: "Kipas Mini MIISOO", harga: 20000, labelType: "stok", stok: 2, description: "Kipas angin mini portabel, baterai 2000mAh, 3 kecepatan, silent." },
                { nama: "Baterai ABC Biru Size AA 1.5V", harga: 5000, labelType: "stok", stok: 25, description: "Baterai ABC, AAA." },
                { nama: "Baterai ABC AAA (A3) (harga per 1pcs)", harga: 5000, label: null, labelType: null, stok: 20, description: "Baterai alkaline ukuran A3 (AAA), tahan lama, isi 2 pcs." }
            ],
            "Aksesoris": [
                { nama: "Charger Robot Micro USB", harga: 30000, label: null, labelType: null, stok: 0, description: "Charger kabel micro USB panjang 1 meter, mendukung arus 2A fast charging." },
                { nama: "Kabel Micro USB KIVEE", harga: 15000, label: null, labelType: null, stok: 2, description: "Kabel micro USB." }
            ],
            "Alat Tulis": [
                { nama: "Pulpen Amilio 0.5mm", harga: 2000, label: null, labelType: null, stok: 12, description: "Pulpen gel hitam 0.5 mm, tinta cepat kering, nyaman digenggam." },
                { nama: "Pulpen Joyko 0.5mm", harga: 5000, label: null, labelType: null, stok: 13, description: "Pulpen standar 0.5 mm, tinta tidak mudah luntur, cocok untuk sekolah." },
                { nama: "JOYKO Pensil P-88 2B", harga: 2000, label: null, labelType: null, stok: 12, description: ">Tipe: 2B >Bentuk: Hexagonal Grip >Kayu berkualitas tinggi >For Computer Scanning (Untuk Dipindai Oleh Komputer) >Thick and Strong Lead (Isi Pensil yang Tebal dan Kuat) >For Drawing and Sketching (Untuk Menggambar dan Membuat Sketsa) >Smooth Writing (Lembut Untuk Ditulis)." },
                { nama: "Deli I-Select Spidol Warna 12 Warna", harga: 10000, label: null, labelType: null, stok: 7, description: "Merek: Deli. Informasi dan Spesifikasi Produk: - Kode SKU: EC169. - Catatan: REPACKAGING. - Material: Tip Serat Fiber dan PP Barrel. - Tip: Bullet 1mm-1.2mm. - Pilihan Varian 12, 18, 24 Warna. - Round Barrel. - Cocok digunakan untuk menulis, menggambar, dan mewarnai" },
                { nama: "Pensil Warna JOYKO (12 warna)", harga: 15000, labelType: "stok", stok: 4, description: "Set pensil warna 12 warna, pigmen cerah, batang kayu berkualitas." },
                { nama: "JOYKO Penanda Berwarna Highlighter HL-88", harga: 5000, labelType: "stok", stok: 7, description: "JOYKO Penanda Berwarna Highlighter HL-88." },
                { nama: "Buku SIDU SKOLA 1 pack (10 buku)", harga: 35000, labelType: "stok", stok: 6, description: "Paket 5 buku tulis 38 lembar, cover motif, kertas berkualitas." },
                { nama: "Rautan pensil, JOYKO", harga: 2000, labelType: "stok", stok: 22, description: "JOYKO Sharpener Rautan 1 Pack SP-362PTL" },
                { nama: "Pulpen Joyko i-Tech 2, 0.28mm", harga: 5000, label: null, labelType: null, stok: 18, description: "Pulpen gel tipis 0.28 mm, cocok untuk tulisan rapi dan detail." },
                { nama: "Penghapus Joyko", harga: 3000, label: null, labelType: null, stok: 10, description: "Penghapus putih, lembut, tidak meninggalkan bekas pada kertas." },
                { nama: "Buku CAMPUS 1 pack (10 buku)", harga: 40000, labelType: "stok", stok: 6, description: "Paket 5 buku tulis 48 lembar, ukuran A5, cover polos." }
            ],
            "Perlengkapan Kantor": [
                { nama: "Lem Korea", harga: 5000, label: null, labelType: null, stok: 61, description: "Lem serbaguna, daya rekat kuat." },
                { nama: "Staples Joyko", harga: 15000, label: null, labelType: null, stok: 5, description: "Staples ukuran sedang, kapasitas 20 lembar, body plastik kokoh." },
                { nama: "Lakban Coklat Bening 45mm x 100 Yard", harga: 10000, label: null, labelType: null, stok: 6, description: "Lakban Coklat 45mm x 100 Yard ini adalah solusi tepat untuk kebutuhan packing Anda. Dengan lebar 45 mm dan panjang 100 Yard, lakban ini memiliki daya rekat yang kuat dan tidak mudah sobek. Cocok untuk berbagai keperluan, baik untuk usaha online maupun kebutuhan sehari-hari." },
                { nama: "Gunting Montana STI 180", harga: 1000, label: null, labelType: null, stok: 8, description: "Gunting stainless steel, panjang 18 cm, pegangan ergonomis." },
                { nama: "Gunting Montana STI 165", harga: 8000, label: null, labelType: null, stok: 8, description: "Gunting serbaguna 16.5 cm, bilah tajam untuk kertas dan karton." },
                { nama: "Gunting Montana STI 145", harga: 5000, label: null, labelType: null, stok: 5, description: "Gunting kecil 14.5 cm, cocok untuk keperluan detail dan anak-anak." },
                { nama: "Refill Staples MONTANA", harga: 3000, label: null, labelType: null, stok: 23, description: "Isi staples ukuran 24/6, isi 100 pcs, cocok untuk staples standar." },
                { nama: "Lakban Bening", harga: 2000, label: null, labelType: null, stok: 11, description: "Lakban bening lebar 48 mm, transparan dan kuat." },
                { nama: "Lakban Hitam", harga: 2000, label: null, labelType: null, stok: 8, description: "Lakban hitam lebar 48 mm, untuk packing atau masking." }
            ]
        };

        // ============================================================
        // 3. MERGE
        // ============================================================
        function getAllProducts() {
            const result = [];
            let id = 1;
            Object.keys(PRODUK_DATA).forEach(kategori => {
                PRODUK_DATA[kategori].forEach(item => {
                    result.push({
                        id: id++,
                        ...item,
                        category: kategori,
                        image: PRODUK_IMAGES[item.nama] || "https://via.placeholder.com/400x400?text=Gambar+error"
                    });
                });
            });
            return result;
        }

        const products = getAllProducts();

        // ============================================================
        // 4. RENDER
        // ============================================================
        let currentFilter = "Semua";
        let currentSearch = "";
        let currentSort = "default";
        let currentStok = "semua";

        function renderProducts() {
            const grid = document.getElementById("productGrid");
            const info = document.getElementById("resultInfo");
            if (!grid) return;

            let filtered = products.filter(p => {
                const matchCategory = currentFilter === "Semua" || p.category === currentFilter;
                const searchLower = currentSearch.toLowerCase();
                const matchSearch = p.nama.toLowerCase().includes(searchLower) ||
                    p.category.toLowerCase().includes(searchLower) ||
                    (p.description && p.description.toLowerCase().includes(searchLower));
                const matchStok = currentStok === "semua" ||
                    (currentStok === "tersedia" && p.stok > 0) ||
                    (currentStok === "habis" && p.stok === 0);
                return matchCategory && matchSearch && matchStok;
            });

            if (currentSort === "asc") filtered.sort((a, b) => a.harga - b.harga);
            else if (currentSort === "desc") filtered.sort((a, b) => b.harga - a.harga);

            info.textContent = `Menampilkan ${filtered.length} barang`;

            if (filtered.length === 0) {
                grid.innerHTML = `
                    <div style="grid-column:1/-1; text-align:center; padding:60px 20px; color:rgba(255,255,255,0.8);">
                        <p style="font-size:18px; font-weight:600; margin-bottom:4px;">😕 Barang tidak ditemukan</p>
                        <p style="font-size:14px; opacity:0.7;">Coba kata kunci lain atau reset filter.</p>
                    </div>
                `;
                return;
            }

            let html = "";
            filtered.forEach((p, index) => {
                const formattedPrice = p.harga.toLocaleString("id-ID");
                const stokTersedia = p.stok > 0;
                const nomorUrut = String(index + 1).padStart(2, '0');

                let badgeHtml = "";
                if (p.label) {
                    let cls = p.labelType === "stok" ? "badge-stok" : "badge-hot";
                    badgeHtml = `<span class="badge ${cls}">${p.label}</span>`;
                } else if (!stokTersedia) {
                    badgeHtml = `<span class="badge badge-habis">Habis</span>`;
                }

                const stokText = stokTersedia ? `${p.stok} pcs` : "0 pcs (Habis)";
                const stokCls = stokTersedia ? "stok-tersedia" : "stok-habis";

                const waLink = `https://wa.me/6283844843020?text=Halo%20PasirPogorCell%2C%20saya%20tertarik%20dengan%20barang%20${encodeURIComponent(p.nama)}%20-%20Rp${formattedPrice}`;

                html += `
                    <div class="product-card" data-id="${p.id}">
                        <span class="product-number">#${nomorUrut}</span>
                        <div class="product-image">
                            <img src="${p.image}" alt="${p.nama}" loading="lazy" onerror="this.src='https://via.placeholder.com/400x400?text=Gambar+error'" />
                            ${badgeHtml}
                        </div>
                        <div class="product-info">
                            <div class="product-name">${p.nama}</div>
                            <div class="product-category">${p.category}</div>
                            <div class="product-price-row">
                                <div class="product-price">
                                    <span class="currency">Rp</span> ${formattedPrice}
                                </div>
                            </div>
                            <div class="product-stok">
                                <span>Stok: <span class="stok-angka ${stokCls}">${stokText}</span></span>
                            </div>
                            <div class="product-action">
                                <button class="btn-detail" data-id="${p.id}">Detail</button>
                                <a href="${waLink}" target="_blank" class="btn-wa">WA</a>
                            </div>
                        </div>
                    </div>
                `;
            });

            grid.innerHTML = html;
        }

        // ============================================================
        // 5. MODAL DETAIL
        // ============================================================
        const modalOverlay = document.getElementById("modalOverlay");
        const modalClose = document.getElementById("modalClose");
        const modalImage = document.getElementById("modalImage");
        const modalName = document.getElementById("modalName");
        const modalCategory = document.getElementById("modalCategory");
        const modalPrice = document.getElementById("modalPrice");
        const modalStok = document.getElementById("modalStok");
        const modalDescription = document.getElementById("modalDescription");
        const modalWaLink = document.getElementById("modalWaLink");
        const modalCopyBtn = document.getElementById("modalCopyBtn");

        function openModal(productId) {
            const p = products.find(prod => prod.id === productId);
            if (!p) return;
            modalImage.src = p.image;
            modalImage.alt = p.nama;
            modalImage.onerror = function() { this.src = 'https://via.placeholder.com/600x600?text=Gambar+error'; };
            modalName.textContent = p.nama;
            modalCategory.textContent = p.category;

            const formatted = p.harga.toLocaleString("id-ID");
            modalPrice.innerHTML = `<span class="currency">Rp</span> ${formatted}`;

            const stokTersedia = p.stok > 0;
            const stokText = stokTersedia ? `${p.stok} pcs` : "0 pcs (Habis)";
            const stokCls = stokTersedia ? "stok-tersedia" : "stok-habis";
            modalStok.innerHTML = `Stok: <span class="stok-angka ${stokCls}">${stokText}</span>`;

            modalDescription.textContent = p.description || "";
            modalWaLink.href = `https://wa.me/6283844843020?text=Halo%20PasirPogorCell%2C%20saya%20tertarik%20dengan%20barang%20${encodeURIComponent(p.nama)}%20-%20Rp${formatted}`;
            
            modalCopyBtn.onclick = function() {
                navigator.clipboard.writeText(p.nama).then(() => {
                    const originalText = modalCopyBtn.textContent;
                    modalCopyBtn.textContent = '✅ Tersalin!';
                    setTimeout(() => { modalCopyBtn.textContent = originalText; }, 2000);
                }).catch(() => {
                    alert('Gagal menyalin, silakan copy manual.');
                });
            };

            modalOverlay.classList.add("active");
        }

        function closeModal() { modalOverlay.classList.remove("active"); }

        document.addEventListener("click", function(e) {
            if (e.target.classList.contains("btn-detail")) {
                const id = parseInt(e.target.dataset.id);
                openModal(id);
            }
        });
        modalClose.addEventListener("click", closeModal);
        modalOverlay.addEventListener("click", function(e) {
            if (e.target === modalOverlay) closeModal();
        });

        // ============================================================
        // 6. ORDER MODAL
        // ============================================================
        const orderModal = document.getElementById("orderModal");
        const orderModalClose = document.getElementById("orderModalClose");
        const openOrderBtn = document.getElementById("openOrderBtn");
        const orderForm = document.getElementById("orderForm");
        const orderSubmitBtn = document.getElementById("orderSubmitBtn");

        function openOrderModal() {
            orderModal.classList.add("active");
        }

        function closeOrderModal() {
            orderModal.classList.remove("active");
        }

        openOrderBtn.addEventListener("click", openOrderModal);
        orderModalClose.addEventListener("click", closeOrderModal);
        orderModal.addEventListener("click", function(e) {
            if (e.target === orderModal) closeOrderModal();
        });

        orderForm.addEventListener("submit", function(e) {
            e.preventDefault();
            
            const namaBarang = document.getElementById("orderNamaBarang").value.trim();
            const spesifikasi = document.getElementById("orderSpesifikasi").value.trim();
            const harga = document.getElementById("orderHarga").value.trim();
            const jumlah = document.getElementById("orderJumlah").value.trim();
            const nama = document.getElementById("orderNama").value.trim();
            const wa = document.getElementById("orderWa").value.trim();
            const metode = document.getElementById("orderMetode").value;
            const catatan = document.getElementById("orderCatatan").value.trim();

            if (!namaBarang || !nama || !wa || !metode || !jumlah) {
                alert('Mohon isi semua field yang bertanda * (wajib)!');
                return;
            }

            // Build pesan WhatsApp
            let pesan = `📦 *PESANAN PRE-ORDER - PasirPogorCell*%0A%0A`;
            pesan += `📌 *Barang:* ${namaBarang}%0A`;
            if (spesifikasi) pesan += `📝 *Spesifikasi:* ${spesifikasi}%0A`;
            if (harga) pesan += `💰 *Harga yang diharapkan:* Rp ${parseInt(harga).toLocaleString('id-ID')}%0A`;
            pesan += `🔢 *Jumlah:* ${jumlah} pcs%0A`;
            pesan += `👤 *Nama:* ${nama}%0A`;
            pesan += `📱 *WhatsApp:* ${wa}%0A`;
            pesan += `💳 *Metode Pembayaran:* ${metode}%0A`;
            if (catatan) pesan += `📝 *Catatan:* ${catatan}%0A`;
            pesan += `%0A⏳ *Estimasi datang:* 3-7 hari%0A`;
            pesan += `💰 *Pembayaran:* di muka (full)%0A`;
            pesan += `✅ *Garansi:* kualitas terjamin & tidak sesuai bisa diklaim`;

            const waUrl = `https://wa.me/6283844843020?text=${pesan}`;
            window.open(waUrl, '_blank');

            // Reset form
            orderForm.reset();
            document.getElementById("orderJumlah").value = "1";
            
            // Close modal after short delay
            setTimeout(closeOrderModal, 500);
        });

        // ============================================================
        // 7. CONTROLS
        // ============================================================
        document.getElementById("searchInput").addEventListener("input", function() {
            currentSearch = this.value.trim();
            renderProducts();
        });

        document.getElementById("sortSelect").addEventListener("change", function() {
            currentSort = this.value;
            renderProducts();
        });

        document.getElementById("stokFilter").addEventListener("change", function() {
            currentStok = this.value;
            renderProducts();
        });

        document.querySelectorAll("#filterGroup .filter-btn").forEach(btn => {
            btn.addEventListener("click", function() {
                document.querySelectorAll("#filterGroup .filter-btn").forEach(b => b.classList.remove("active"));
                this.classList.add("active");
                currentFilter = this.dataset.filter;
                renderProducts();
            });
        });

        // ============================================================
        // 8. RENDER AWAL
        // ============================================================
        renderProducts();
    </script>
</body>
</html>