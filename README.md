<!doctype html>
<html lang="fr">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>GestaScreen DZ</title>
        <link
            href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@300;400;500;600&family=Playfair+Display:wght@600&display=swap"
            rel="stylesheet"
        />
        <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
        <style>
            * {
                margin: 0;
                padding: 0;
                box-sizing: border-box;
            }
            :root {
                --primary: #1a6b5a;
                --primary-light: #e8f5f1;
                --primary-mid: #2e8b76;
                --accent: #2563eb;
                --accent-light: #eef4ff;
                --danger: #dc2626;
                --danger-light: #fef2f2;
                --warn: #d97706;
                --warn-light: #fffbeb;
                --bg: #f4f7f6;
                --surface: #ffffff;
                --border: #e2eae7;
                --border-strong: #c5d5d0;
                --text: #1a2e29;
                --text-2: #4a6560;
                --text-3: #8ba8a2;
                --radius: 12px;
                --radius-sm: 8px;
                --radius-lg: 16px;
                --shadow:
                    0 1px 3px rgba(0, 0, 0, 0.07),
                    0 4px 12px rgba(0, 0, 0, 0.05);
                --shadow-lg: 0 4px 20px rgba(0, 0, 0, 0.1);
            }
            body {
                font-family: "DM Sans", sans-serif;
                background: var(--bg);
                color: var(--text);
                min-height: 100vh;
                font-size: 15px;
                line-height: 1.6;
            }
            h1,
            h2,
            h3 {
                font-family: "Playfair Display", serif;
                font-weight: 600;
            }
            .page {
                display: none;
                min-height: 100vh;
            }
            .page.active {
                display: block;
            }

            /* ===== LOGIN ===== */
            #page-login {
                display: none;
                align-items: center;
                justify-content: center;
                background: linear-gradient(
                    135deg,
                    #0f3d33 0%,
                    #1a6b5a 50%,
                    #2e8b76 100%
                );
                min-height: 100vh;
            }
            #page-login.active {
                display: flex;
            }
            .login-card {
                background: var(--surface);
                border-radius: var(--radius-lg);
                padding: 48px 40px;
                width: 100%;
                max-width: 420px;
                box-shadow: var(--shadow-lg);
            }
            .login-logo {
                text-align: center;
                margin-bottom: 32px;
            }
            .login-logo .logo-icon {
                width: 64px;
                height: 64px;
                border-radius: 50%;
                display: flex;
                align-items: center;
                justify-content: center;
                margin: 0 auto 12px;
                overflow: hidden;
            }
            .login-logo .logo-icon img {
                width: 100%;
                height: 100%;
                object-fit: contain;
            }
            .login-logo h1 {
                font-size: 24px;
                color: var(--primary);
                letter-spacing: -0.5px;
            }
            .login-logo p {
                font-size: 13px;
                color: var(--text-2);
                margin-top: 4px;
            }
            .form-group {
                margin-bottom: 18px;
            }
            .form-group label {
                display: block;
                font-size: 13px;
                font-weight: 500;
                color: var(--text-2);
                margin-bottom: 6px;
            }
            .form-control {
                width: 100%;
                padding: 11px 14px;
                border: 1.5px solid var(--border);
                border-radius: var(--radius-sm);
                font-family: inherit;
                font-size: 14px;
                color: var(--text);
                background: var(--bg);
                transition:
                    border-color 0.2s,
                    box-shadow 0.2s;
                outline: none;
            }
            .form-control:focus {
                border-color: var(--primary);
                box-shadow: 0 0 0 3px rgba(26, 107, 90, 0.12);
                background: var(--surface);
            }
            .btn {
                display: inline-flex;
                align-items: center;
                justify-content: center;
                gap: 8px;
                padding: 11px 20px;
                border-radius: var(--radius-sm);
                font-family: inherit;
                font-size: 14px;
                font-weight: 500;
                cursor: pointer;
                border: none;
                transition: all 0.15s;
                text-decoration: none;
            }
            .btn-primary {
                background: var(--primary);
                color: #fff;
            }
            .btn-primary:hover {
                background: #155247;
            }
            .btn-secondary {
                background: var(--surface);
                color: var(--text);
                border: 1.5px solid var(--border);
            }
            .btn-secondary:hover {
                background: var(--bg);
            }
            .btn-accent {
                background: var(--accent);
                color: #fff;
            }
            .btn-accent:hover {
                background: #1d4ed8;
            }
            .btn-danger {
                background: var(--danger);
                color: #fff;
            }
            .btn-danger:hover {
                background: #b91c1c;
            }
            .btn-ghost {
                background: transparent;
                color: var(--text-2);
                border: 1.5px solid var(--border);
            }
            .btn-ghost:hover {
                background: var(--bg);
            }
            .btn-full {
                width: 100%;
            }
            .btn-lg {
                padding: 13px 24px;
                font-size: 15px;
            }
            .btn-sm {
                padding: 7px 14px;
                font-size: 13px;
            }
            .error-msg {
                background: var(--danger-light);
                color: var(--danger);
                padding: 10px 14px;
                border-radius: var(--radius-sm);
                font-size: 13px;
                margin-bottom: 16px;
                display: none;
            }

            /* ===== LAYOUT ===== */
            .app-header {
                background: var(--surface);
                border-bottom: 1px solid var(--border);
                padding: 0 24px;
                height: 64px;
                display: flex;
                align-items: center;
                justify-content: space-between;
                position: sticky;
                top: 0;
                z-index: 100;
                box-shadow: 0 1px 8px rgba(0, 0, 0, 0.06);
            }
            .header-brand {
                display: flex;
                align-items: center;
                gap: 12px;
            }
            .header-logo {
                width: 120px;
                height: 40px;
                display: flex;
                align-items: center;
                justify-content: flex-start;
                overflow: visible;
                background: transparent;
            }
            .header-logo img {
                width: auto;
                height: 100%;
                object-fit: contain;
            }
            .header-name {
                font-family: "Playfair Display", serif;
                font-size: 18px;
                color: var(--primary);
                font-weight: 600;
            }
            .header-sub {
                font-size: 11px;
                color: var(--text-3);
                margin-top: -2px;
            }
            .header-actions {
                display: flex;
                align-items: center;
                gap: 10px;
            }
            .main-content {
                max-width: 1200px;
                margin: 0 auto;
                padding: 32px 24px;
            }

            /* ===== STAT CARDS ===== */
            .stat-grid {
                display: grid;
                grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
                gap: 16px;
                margin-bottom: 28px;
            }
            .stat-card {
                background: var(--surface);
                border-radius: var(--radius);
                padding: 20px 22px;
                border: 1px solid var(--border);
                box-shadow: var(--shadow);
            }
            .stat-card .stat-label {
                font-size: 12px;
                font-weight: 500;
                color: var(--text-2);
                text-transform: uppercase;
                letter-spacing: 0.6px;
                margin-bottom: 8px;
            }
            .stat-card .stat-value {
                font-size: 32px;
                font-family: "Playfair Display", serif;
                color: var(--text);
                line-height: 1;
            }
            .stat-card .stat-sub {
                font-size: 12px;
                color: var(--text-3);
                margin-top: 4px;
            }
            .stat-card.green {
                border-left: 4px solid var(--primary);
            }
            .stat-card.blue {
                border-left: 4px solid var(--accent);
            }
            .stat-card.orange {
                border-left: 4px solid var(--warn);
            }

            /* ===== SECTION HEADER ===== */
            .section-header {
                display: flex;
                align-items: center;
                justify-content: space-between;
                margin-bottom: 16px;
                flex-wrap: wrap;
                gap: 10px;
            }
            .section-title {
                font-size: 18px;
                color: var(--text);
            }
            .section-actions {
                display: flex;
                gap: 8px;
                flex-wrap: wrap;
            }

            /* ===== TABLE ===== */
            .table-card {
                background: var(--surface);
                border-radius: var(--radius);
                border: 1px solid var(--border);
                box-shadow: var(--shadow);
                overflow: hidden;
            }
            .table-search {
                padding: 14px 16px;
                border-bottom: 1px solid var(--border);
            }
            .table-search input {
                width: 100%;
                padding: 9px 14px;
                border: 1.5px solid var(--border);
                border-radius: var(--radius-sm);
                font-family: inherit;
                font-size: 14px;
                outline: none;
                color: var(--text);
                background: var(--bg);
            }
            .table-search input:focus {
                border-color: var(--primary);
            }
            .tbl-wrap {
                overflow-x: auto;
            }
            table {
                width: 100%;
                border-collapse: collapse;
                min-width: 600px;
            }
            thead tr {
                background: var(--bg);
            }
            th {
                padding: 11px 16px;
                text-align: left;
                font-size: 12px;
                font-weight: 600;
                color: var(--text-2);
                text-transform: uppercase;
                letter-spacing: 0.5px;
                border-bottom: 1px solid var(--border);
            }
            td {
                padding: 12px 16px;
                font-size: 14px;
                color: var(--text);
                border-bottom: 1px solid var(--border);
            }
            tr:last-child td {
                border-bottom: none;
            }
            tr:hover td {
                background: var(--primary-light);
            }
            .badge {
                display: inline-flex;
                align-items: center;
                padding: 3px 10px;
                border-radius: 20px;
                font-size: 12px;
                font-weight: 500;
            }
            .badge-positive {
                background: #dcfce7;
                color: #166534;
            }
            .badge-negative {
                background: #fee2e2;
                color: #991b1b;
            }
            .badge-pending {
                background: #fef3c7;
                color: #92400e;
            }
            .action-btns {
                display: flex;
                gap: 6px;
            }
            .icon-btn {
                width: 30px;
                height: 30px;
                border-radius: 6px;
                border: 1.5px solid var(--border);
                background: var(--surface);
                cursor: pointer;
                display: flex;
                align-items: center;
                justify-content: center;
                font-size: 14px;
                transition: all 0.15s;
            }
            .icon-btn:hover {
                background: var(--primary-light);
                border-color: var(--primary);
            }
            .icon-btn.del:hover {
                background: var(--danger-light);
                border-color: var(--danger);
            }
            .empty-state {
                text-align: center;
                padding: 60px 20px;
                color: var(--text-3);
            }
            .empty-state .empty-icon {
                font-size: 48px;
                margin-bottom: 12px;
            }
            .empty-state p {
                font-size: 15px;
            }

            /* ===== FORM PAGE ===== */
            .form-page-header {
                margin-bottom: 28px;
            }
            .form-page-header h2 {
                font-size: 24px;
                color: var(--text);
            }
            .form-page-header p {
                color: var(--text-2);
                font-size: 14px;
                margin-top: 4px;
            }
            .form-card {
                background: var(--surface);
                border-radius: var(--radius);
                border: 1px solid var(--border);
                box-shadow: var(--shadow);
                margin-bottom: 20px;
                overflow: hidden;
            }
            .form-section-title {
                padding: 16px 24px;
                background: var(--primary-light);
                border-bottom: 1px solid var(--border);
                font-size: 14px;
                font-weight: 600;
                color: var(--primary);
                display: flex;
                align-items: center;
                gap: 8px;
            }
            .form-section-title .sec-icon {
                font-size: 16px;
            }
            .form-grid {
                padding: 20px 24px;
                display: grid;
                grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
                gap: 16px 20px;
            }
            .form-group-inner {
                display: flex;
                flex-direction: column;
                gap: 5px;
            }
            .form-group-inner label {
                font-size: 13px;
                font-weight: 500;
                color: var(--text-2);
            }
            .form-group-inner .hint {
                font-size: 11px;
                color: var(--text-3);
                margin-top: 2px;
            }
            .form-control-sm {
                padding: 9px 12px;
                border: 1.5px solid var(--border);
                border-radius: var(--radius-sm);
                font-family: inherit;
                font-size: 14px;
                color: var(--text);
                background: var(--surface);
                outline: none;
                width: 100%;
                transition: border-color 0.2s;
            }
            .form-control-sm:focus {
                border-color: var(--primary);
                box-shadow: 0 0 0 3px rgba(26, 107, 90, 0.1);
            }
            select.form-control-sm {
                cursor: pointer;
            }
            .radio-group {
                display: flex;
                gap: 12px;
                flex-wrap: wrap;
                margin-top: 2px;
            }
            .radio-label {
                display: flex;
                align-items: center;
                gap: 6px;
                cursor: pointer;
                font-size: 14px;
                padding: 7px 12px;
                border: 1.5px solid var(--border);
                border-radius: var(--radius-sm);
                transition: all 0.15s;
                user-select: none;
            }
            .radio-label:hover {
                border-color: var(--primary);
                background: var(--primary-light);
            }
            .radio-label input {
                accent-color: var(--primary);
            }
            .checkbox-group {
                display: flex;
                flex-direction: column;
                gap: 6px;
                margin-top: 2px;
            }
            .checkbox-label {
                display: flex;
                align-items: center;
                gap: 7px;
                cursor: pointer;
                font-size: 14px;
                padding: 5px 2px;
            }
            .checkbox-label input {
                accent-color: var(--primary);
                width: 15px;
                height: 15px;
            }
            .auto-badge {
                display: inline-block;
                background: var(--accent-light);
                color: var(--accent);
                font-size: 11px;
                font-weight: 500;
                padding: 2px 8px;
                border-radius: 10px;
                margin-left: 6px;
            }
            .form-footer {
                padding: 20px 24px;
                border-top: 1px solid var(--border);
                display: flex;
                gap: 12px;
                justify-content: flex-end;
                flex-wrap: wrap;
            }
            .imc-display {
                padding: 9px 12px;
                border: 1.5px solid var(--border-strong);
                border-radius: var(--radius-sm);
                font-size: 14px;
                font-weight: 600;
                color: var(--primary);
                background: var(--primary-light);
                min-height: 40px;
                display: flex;
                align-items: center;
            }
            .dg-display {
                padding: 9px 12px;
                border-radius: var(--radius-sm);
                font-size: 14px;
                font-weight: 600;
                min-height: 40px;
                display: flex;
                align-items: center;
                gap: 6px;
            }
            .dg-pos {
                background: #fef2f2;
                color: #dc2626;
                border: 1.5px solid #fecaca;
            }
            .dg-neg {
                background: #f0fdf4;
                color: #166534;
                border: 1.5px solid #bbf7d0;
            }
            .dg-na {
                background: var(--bg);
                color: var(--text-3);
                border: 1.5px solid var(--border);
            }
            .full-span {
                grid-column: 1/-1;
            }

            /* ===== STATS ===== */
            .charts-grid {
                display: grid;
                grid-template-columns: 1fr 1fr;
                gap: 20px;
                margin-bottom: 20px;
            }
            @media (max-width: 700px) {
                .charts-grid {
                    grid-template-columns: 1fr;
                }
            }
            .chart-card {
                background: var(--surface);
                border-radius: var(--radius);
                border: 1px solid var(--border);
                box-shadow: var(--shadow);
                padding: 20px 24px;
            }
            .chart-card h3 {
                font-size: 15px;
                color: var(--text);
                margin-bottom: 16px;
            }
            .chart-wrap {
                position: relative;
                height: 260px;
            }
            .stats-summary {
                display: grid;
                grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
                gap: 14px;
                margin-bottom: 20px;
            }
            .stat-row {
                display: flex;
                align-items: center;
                justify-content: space-between;
                padding: 10px 14px;
                background: var(--bg);
                border-radius: var(--radius-sm);
                font-size: 14px;
            }
            .stat-row .lbl {
                color: var(--text-2);
            }
            .stat-row .val {
                font-weight: 600;
                color: var(--primary);
            }

            /* ===== MODAL ===== */
            .modal-overlay {
                display: none;
                position: fixed;
                inset: 0;
                background: rgba(0, 0, 0, 0.4);
                z-index: 500;
                align-items: center;
                justify-content: center;
                padding: 20px;
            }
            .modal-overlay.open {
                display: flex;
            }
            .modal {
                background: var(--surface);
                border-radius: var(--radius-lg);
                width: 100%;
                max-width: 600px;
                max-height: 90vh;
                overflow: hidden;
                display: flex;
                flex-direction: column;
                box-shadow: var(--shadow-lg);
            }
            .modal-header {
                padding: 20px 24px;
                border-bottom: 1px solid var(--border);
                display: flex;
                align-items: center;
                justify-content: space-between;
            }
            .modal-header h3 {
                font-size: 17px;
                color: var(--text);
            }
            .modal-close {
                width: 32px;
                height: 32px;
                border-radius: 6px;
                border: 1.5px solid var(--border);
                background: var(--surface);
                cursor: pointer;
                font-size: 16px;
                display: flex;
                align-items: center;
                justify-content: center;
                color: var(--text-2);
            }
            .modal-close:hover {
                background: var(--bg);
            }
            .modal-body {
                padding: 20px 24px;
                overflow-y: auto;
                flex: 1;
            }
            .modal-footer {
                padding: 16px 24px;
                border-top: 1px solid var(--border);
                display: flex;
                gap: 10px;
                justify-content: flex-end;
                flex-wrap: wrap;
            }
            .json-textarea {
                width: 100%;
                height: 200px;
                padding: 12px;
                border: 1.5px solid var(--border);
                border-radius: var(--radius-sm);
                font-family: "Courier New", monospace;
                font-size: 12px;
                resize: vertical;
                outline: none;
                color: var(--text);
                background: var(--bg);
            }
            .json-textarea:focus {
                border-color: var(--primary);
            }
            .import-note {
                font-size: 13px;
                color: var(--text-2);
                margin-bottom: 12px;
                line-height: 1.6;
            }
            .import-success {
                background: #f0fdf4;
                color: #166534;
                padding: 10px 14px;
                border-radius: var(--radius-sm);
                font-size: 13px;
                margin-top: 12px;
                display: none;
            }
            .import-error {
                background: var(--danger-light);
                color: var(--danger);
                padding: 10px 14px;
                border-radius: var(--radius-sm);
                font-size: 13px;
                margin-top: 12px;
                display: none;
            }
            .toast {
                position: fixed;
                bottom: 24px;
                right: 24px;
                background: #1a2e29;
                color: #fff;
                padding: 12px 20px;
                border-radius: var(--radius-sm);
                font-size: 14px;
                z-index: 9999;
                transform: translateY(80px);
                opacity: 0;
                transition: all 0.3s;
                pointer-events: none;
            }
            .toast.show {
                transform: translateY(0);
                opacity: 1;
            }
            .back-btn {
                display: inline-flex;
                align-items: center;
                gap: 6px;
                color: var(--text-2);
                font-size: 14px;
                margin-bottom: 16px;
                cursor: pointer;
                padding: 4px 0;
                border: none;
                background: none;
                font-family: inherit;
            }
            .back-btn:hover {
                color: var(--primary);
            }
            .confirm-modal-body {
                padding: 24px;
                text-align: center;
            }
            .confirm-modal-body .icon {
                font-size: 40px;
                margin-bottom: 12px;
            }
            .confirm-modal-body p {
                color: var(--text-2);
                font-size: 14px;
                margin-top: 6px;
            }

            /* ===== RESPONSIVE ===== */
            @media (max-width: 768px) {
                .main-content {
                    padding: 20px 16px;
                }
                .form-grid {
                    grid-template-columns: 1fr;
                }
                .header-name {
                    display: none;
                }
                .stat-grid {
                    grid-template-columns: 1fr 1fr;
                }
                .charts-grid {
                    grid-template-columns: 1fr;
                }
            }
            @media (max-width: 480px) {
                .stat-grid {
                    grid-template-columns: 1fr;
                }
                .section-header {
                    flex-direction: column;
                    align-items: flex-start;
                }
            }
            .nav-breadcrumb {
                font-size: 13px;
                color: var(--text-3);
                margin-bottom: 20px;
            }
            .nav-breadcrumb span {
                color: var(--text-2);
            }
        </style>
    </head>
    <body>
        <!-- TOAST -->
        <div class="toast" id="toast"></div>

        <!-- ===== PAGE: LOGIN ===== -->
        <div class="page" id="page-login">
            <div class="login-card">
                <div class="login-logo">
                    <div class="logo-icon">
                        <img src="logo.png" alt="DG Logo" />
                    </div>
                    <h1>GestaScreen DZ</h1>
                    <p>Système de surveillance du diabète gestationnel</p>
                </div>
                <div class="error-msg" id="login-error">
                    Identifiants incorrects. Réessayez.
                </div>
                <div class="form-group">
                    <label>Adresse e-mail</label>
                    <input
                        type="email"
                        class="form-control"
                        id="login-email"
                        placeholder="admin@gestascreen.dz"
                        autocomplete="username"
                    />
                </div>
                <div class="form-group">
                    <label>Mot de passe</label>
                    <input
                        type="password"
                        class="form-control"
                        id="login-pwd"
                        placeholder="••••••••"
                        autocomplete="current-password"
                    />
                </div>
                <button
                    class="btn btn-primary btn-full btn-lg"
                    onclick="doLogin()"
                >
                    Se connecter
                </button>
                <p
                    style="
                        text-align: center;
                        font-size: 12px;
                        color: var(--text-3);
                        margin-top: 16px;
                    "
                >
                    Utilisez n'importe quel e-mail et mot de passe valides
                </p>
            </div>
        </div>

        <!-- ===== PAGE: HOME / DASHBOARD ===== -->
        <div class="page" id="page-home">
            <header class="app-header">
                <div class="header-brand">
                    <div class="header-logo">
                        <img src="logo.png" alt="DG Logo" />
                    </div>
                    <div>
                        <div class="header-name">GestaScreen DZ</div>
                        <div class="header-sub">
                            Maternité · Diabète gestationnel
                        </div>
                    </div>
                </div>
                <div class="header-actions">
                    <button
                        class="btn btn-ghost btn-sm"
                        onclick="showImportModal()"
                    >
                        📥 Importer
                    </button>
                    <button
                        class="btn btn-secondary btn-sm"
                        onclick="goStats()"
                    >
                        📊 Statistiques
                    </button>
                    <button class="btn btn-danger btn-sm" onclick="doLogout()">
                        Déconnexion
                    </button>
                </div>
            </header>
            <main class="main-content">
                <div class="stat-grid" id="stat-grid"></div>
                <div class="section-header">
                    <h2 class="section-title">Liste des Patientes</h2>
                    <div class="section-actions">
                        <button
                            class="btn btn-primary"
                            onclick="goAddPatient()"
                        >
                            + Ajouter une patiente
                        </button>
                    </div>
                </div>
                <div class="table-card">
                    <div class="table-search">
                        <input
                            type="text"
                            placeholder="🔍  Rechercher par code, âge, résidence…"
                            id="search-input"
                            oninput="renderTable()"
                        />
                    </div>
                    <div class="tbl-wrap">
                        <table>
                            <thead>
                                <tr>
                                    <th>Code</th>
                                    <th>Âge</th>
                                    <th>Résidence</th>
                                    <th>IMC av.</th>
                                    <th>Glycémie (g/L)</th>
                                    <th>Âge gest. (SA)</th>
                                    <th>Diagnostic DG</th>
                                    <th>Actions</th>
                                </tr>
                            </thead>
                            <tbody id="patient-tbody"></tbody>
                        </table>
                    </div>
                </div>
            </main>
        </div>

        <!-- ===== PAGE: FORM (Add/Edit) ===== -->
        <div class="page" id="page-form">
            <header class="app-header">
                <div class="header-brand">
                    <div class="header-logo">
                        <img src="logo.png" alt="DG Logo" />
                    </div>
                    <div>
                        <div class="header-name">GestaScreen DZ</div>
                        <div class="header-sub">Formulaire patiente</div>
                    </div>
                </div>
                <div class="header-actions">
                    <button class="btn btn-danger btn-sm" onclick="doLogout()">
                        Déconnexion
                    </button>
                </div>
            </header>
            <main class="main-content">
                <button class="back-btn" onclick="goHome()">
                    ← Retour au tableau de bord
                </button>
                <div class="form-page-header">
                    <h2 id="form-title">Ajouter une patiente</h2>
                    <p>
                        Remplissez tous les champs pour enregistrer les données
                        de la patiente.
                    </p>
                </div>

                <!-- Section 1: Identification -->
                <div class="form-card">
                    <div class="form-section-title">
                        <span class="sec-icon">👤</span> Identification & Profil
                        sociodémographique
                    </div>
                    <div class="form-grid">
                        <div class="form-group-inner">
                            <label
                                >Code participante
                                <span style="color: var(--danger)"
                                    >*</span
                                ></label
                            >
                            <input
                                type="text"
                                class="form-control-sm"
                                id="f-code"
                                placeholder="ex: P-001"
                            />
                        </div>
                        <div class="form-group-inner">
                            <label
                                >Âge (ans)
                                <span style="color: var(--danger)"
                                    >*</span
                                ></label
                            >
                            <input
                                type="number"
                                class="form-control-sm"
                                id="f-age"
                                min="15"
                                max="60"
                                placeholder="ex: 28"
                            />
                        </div>
                        <div class="form-group-inner">
                            <label>Résidence</label>
                            <input
                                type="text"
                                class="form-control-sm"
                                id="f-residence"
                                placeholder="ex: Oran, Alger…"
                            />
                        </div>
                        <div class="form-group-inner">
                            <label>Niveau d'instruction</label>
                            <select class="form-control-sm" id="f-instruction">
                                <option value="">— Sélectionner —</option>
                                <option>Sans instruction</option>
                                <option>Primaire</option>
                                <option>Moyen</option>
                                <option>Secondaire</option>
                                <option>Universitaire</option>
                            </select>
                        </div>
                        <div class="form-group-inner">
                            <label>Profession</label>
                            <input
                                type="text"
                                class="form-control-sm"
                                id="f-profession"
                                placeholder="ex: Enseignante, Femme au foyer…"
                            />
                        </div>
                        <div class="form-group-inner">
                            <label>Situation matrimoniale</label>
                            <select class="form-control-sm" id="f-matrimoniale">
                                <option value="">— Sélectionner —</option>
                                <option>Mariée</option>
                                <option>Célibataire</option>
                                <option>Divorcée</option>
                                <option>Veuve</option>
                            </select>
                        </div>
                    </div>
                </div>

                <!-- Section 2: Antécédents -->
                <div class="form-card">
                    <div class="form-section-title">
                        <span class="sec-icon">🏥</span> Antécédents médicaux
                    </div>
                    <div class="form-grid">
                        <div class="form-group-inner">
                            <label>Diabète avant grossesse</label>
                            <div class="radio-group">
                                <label class="radio-label"
                                    ><input
                                        type="radio"
                                        name="diabete-avant"
                                        value="Oui"
                                    />
                                    Oui</label
                                >
                                <label class="radio-label"
                                    ><input
                                        type="radio"
                                        name="diabete-avant"
                                        value="Non"
                                        checked
                                    />
                                    Non</label
                                >
                            </div>
                        </div>
                        <div class="form-group-inner">
                            <label>ATCD familial de diabète</label>
                            <div class="checkbox-group" id="atcd-family">
                                <label class="checkbox-label"
                                    ><input type="checkbox" value="Père" />
                                    Père</label
                                >
                                <label class="checkbox-label"
                                    ><input type="checkbox" value="Mère" />
                                    Mère</label
                                >
                                <label class="checkbox-label"
                                    ><input type="checkbox" value="Sœur" />
                                    Sœur</label
                                >
                                <label class="checkbox-label"
                                    ><input type="checkbox" value="Frère" />
                                    Frère</label
                                >
                                <label class="checkbox-label"
                                    ><input type="checkbox" value="Aucun" />
                                    Aucun</label
                                >
                            </div>
                        </div>
                        <div class="form-group-inner">
                            <label>Maladie actuelle</label>
                            <div class="checkbox-group" id="maladie-actuelle">
                                <label class="checkbox-label"
                                    ><input
                                        type="checkbox"
                                        value="Hypertension"
                                    />
                                    Hypertension</label
                                >
                                <label class="checkbox-label"
                                    ><input type="checkbox" value="Thyroïde" />
                                    Thyroïde</label
                                >
                                <label class="checkbox-label"
                                    ><input type="checkbox" value="SOPK" />
                                    SOPK</label
                                >
                                <label class="checkbox-label"
                                    ><input type="checkbox" value="Aucune" />
                                    Aucune</label
                                >
                            </div>
                        </div>
                        <div class="form-group-inner">
                            <label>ATCD de diabète gestationnel</label>
                            <div class="radio-group">
                                <label class="radio-label"
                                    ><input
                                        type="radio"
                                        name="atcd-dg"
                                        value="Oui"
                                    />
                                    Oui</label
                                >
                                <label class="radio-label"
                                    ><input
                                        type="radio"
                                        name="atcd-dg"
                                        value="Non"
                                        checked
                                    />
                                    Non</label
                                >
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Section 3: Obstétrique -->
                <div class="form-card">
                    <div class="form-section-title">
                        <span class="sec-icon">🤰</span> Données obstétricales
                    </div>
                    <div class="form-grid">
                        <div class="form-group-inner">
                            <label>Nombre de grossesses</label>
                            <input
                                type="number"
                                class="form-control-sm"
                                id="f-nb-grossesses"
                                min="1"
                                max="20"
                                placeholder="ex: 2"
                            />
                        </div>
                        <div class="form-group-inner">
                            <label>Parité (nombre d'accouchements)</label>
                            <input
                                type="number"
                                class="form-control-sm"
                                id="f-parite"
                                min="0"
                                max="20"
                                placeholder="ex: 1"
                            />
                        </div>
                        <div class="form-group-inner">
                            <label>Poids bébés à la naissance (kg)</label>
                            <input
                                type="text"
                                class="form-control-sm"
                                id="f-poids-bebe"
                                placeholder="ex: 3.5 ou 4.2, 3.8"
                            />
                        </div>
                        <div class="form-group-inner">
                            <label>Âge gestationnel (SA)</label>
                            <input
                                type="number"
                                class="form-control-sm"
                                id="f-age-gest"
                                min="1"
                                max="45"
                                placeholder="ex: 28"
                            />
                        </div>
                        <div class="form-group-inner">
                            <label>Type de grossesse</label>
                            <div class="radio-group">
                                <label class="radio-label"
                                    ><input
                                        type="radio"
                                        name="type-grossesse"
                                        value="Simple"
                                        checked
                                    />
                                    Simple</label
                                >
                                <label class="radio-label"
                                    ><input
                                        type="radio"
                                        name="type-grossesse"
                                        value="Multiple"
                                    />
                                    Multiple</label
                                >
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Section 4: Hygiène de vie -->
                <div class="form-card">
                    <div class="form-section-title">
                        <span class="sec-icon">🌿</span> Hygiène de vie
                    </div>
                    <div class="form-grid">
                        <div class="form-group-inner">
                            <label>Activité physique</label>
                            <select class="form-control-sm" id="f-activite">
                                <option value="">— Sélectionner —</option>
                                <option>Sédentaire</option>
                                <option>Légère</option>
                                <option>Modérée</option>
                                <option>Intense</option>
                            </select>
                        </div>
                        <div class="form-group-inner">
                            <label>Habitudes alimentaires</label>
                            <select class="form-control-sm" id="f-alimentation">
                                <option value="">— Sélectionner —</option>
                                <option>Équilibrée</option>
                                <option>Riche en sucres</option>
                                <option>Riche en graisses</option>
                                <option>Mixte</option>
                            </select>
                        </div>
                        <div class="form-group-inner">
                            <label>Boissons sucrées</label>
                            <select class="form-control-sm" id="f-boissons">
                                <option value="">— Sélectionner —</option>
                                <option>Jamais</option>
                                <option>Rarement</option>
                                <option>Parfois</option>
                                <option>Souvent</option>
                                <option>Très souvent</option>
                            </select>
                        </div>
                    </div>
                </div>

                <!-- Section 5: Mesures anthropométriques -->
                <div class="form-card">
                    <div class="form-section-title">
                        <span class="sec-icon">📏</span> Mesures
                        anthropométriques
                    </div>
                    <div class="form-grid">
                        <div class="form-group-inner">
                            <label
                                >Taille (cm)
                                <span style="color: var(--danger)"
                                    >*</span
                                ></label
                            >
                            <input
                                type="number"
                                class="form-control-sm"
                                id="f-taille"
                                min="100"
                                max="220"
                                placeholder="ex: 165"
                                oninput="calcIMC()"
                            />
                        </div>
                        <div class="form-group-inner">
                            <label
                                >Poids avant grossesse (kg)
                                <span style="color: var(--danger)"
                                    >*</span
                                ></label
                            >
                            <input
                                type="number"
                                class="form-control-sm"
                                id="f-poids-avant"
                                min="30"
                                max="200"
                                placeholder="ex: 62"
                                oninput="calcIMC()"
                            />
                        </div>
                        <div class="form-group-inner">
                            <label>Poids actuel (kg)</label>
                            <input
                                type="number"
                                class="form-control-sm"
                                id="f-poids-actuel"
                                min="30"
                                max="220"
                                placeholder="ex: 74"
                            />
                        </div>
                        <div class="form-group-inner">
                            <label
                                >IMC avant grossesse
                                <span class="auto-badge"
                                    >Auto-calculé</span
                                ></label
                            >
                            <div class="imc-display" id="imc-display">—</div>
                            <input type="hidden" id="f-imc" />
                        </div>
                    </div>
                </div>

                <!-- Section 6: Diagnostic -->
                <div class="form-card">
                    <div class="form-section-title">
                        <span class="sec-icon">🔬</span> Diagnostic & Prise en
                        charge
                    </div>
                    <div class="form-grid">
                        <div class="form-group-inner">
                            <label
                                >Valeur glycémie (g/L)
                                <span style="color: var(--danger)"
                                    >*</span
                                ></label
                            >
                            <input
                                type="number"
                                class="form-control-sm"
                                id="f-glycemie"
                                step="0.01"
                                min="0"
                                max="5"
                                placeholder="ex: 0.85"
                                oninput="autoDiag()"
                            />
                        </div>
                        <div class="form-group-inner">
                            <label
                                >Diagnostic DG
                                <span class="auto-badge"
                                    >Auto-suggéré</span
                                ></label
                            >
                            <div class="dg-display dg-na" id="dg-display">
                                — Entrez la glycémie —
                            </div>
                            <input type="hidden" id="f-diagnostic" />
                            <div
                                class="hint"
                                style="
                                    margin-top: 4px;
                                    font-size: 11px;
                                    color: var(--text-3);
                                "
                            >
                                Seuil : glycémie ≥ 0.92 g/L → DG positif
                            </div>
                        </div>
                        <div class="form-group-inner">
                            <label
                                >Corriger le diagnostic
                                <span
                                    style="
                                        font-weight: 400;
                                        color: var(--text-3);
                                    "
                                    >(si nécessaire)</span
                                ></label
                            >
                            <div class="radio-group">
                                <label class="radio-label"
                                    ><input
                                        type="radio"
                                        name="diag-override"
                                        value="Oui"
                                        onchange="overrideDiag('Oui')"
                                    />
                                    DG Oui</label
                                >
                                <label class="radio-label"
                                    ><input
                                        type="radio"
                                        name="diag-override"
                                        value="Non"
                                        onchange="overrideDiag('Non')"
                                    />
                                    DG Non</label
                                >
                                <label class="radio-label"
                                    ><input
                                        type="radio"
                                        name="diag-override"
                                        value="auto"
                                        checked
                                        onchange="autoDiag()"
                                    />
                                    Automatique</label
                                >
                            </div>
                        </div>
                        <div class="form-group-inner">
                            <label>Prise en charge</label>
                            <select class="form-control-sm" id="f-prise-charge">
                                <option value="">— Sélectionner —</option>
                                <option>Insulinothérapie</option>
                                <option>Suivi médical régulier</option>
                                <option>Pas de prise en charge</option>
                            </select>
                        </div>
                        <div class="form-group-inner full-span">
                            <label>Complications associées</label>
                            <div
                                class="checkbox-group"
                                id="complications"
                                style="
                                    flex-direction: row;
                                    flex-wrap: wrap;
                                    gap: 8px;
                                "
                            >
                                <label class="checkbox-label"
                                    ><input
                                        type="checkbox"
                                        value="HTA gravidique"
                                    />
                                    HTA gravidique</label
                                >
                                <label class="checkbox-label"
                                    ><input
                                        type="checkbox"
                                        value="Hydramnios"
                                    />
                                    Hydramnios</label
                                >
                                <label class="checkbox-label"
                                    ><input
                                        type="checkbox"
                                        value="Macrosomie"
                                    />
                                    Macrosomie</label
                                >
                                <label class="checkbox-label"
                                    ><input type="checkbox" value="Aucune" />
                                    Aucune</label
                                >
                            </div>
                        </div>
                    </div>
                    <div class="form-footer">
                        <button class="btn btn-ghost" onclick="goHome()">
                            Annuler
                        </button>
                        <button
                            class="btn btn-primary btn-lg"
                            onclick="savePatient()"
                        >
                            💾 Enregistrer la patiente
                        </button>
                    </div>
                </div>
            </main>
        </div>

        <!-- ===== PAGE: STATS ===== -->
        <div class="page" id="page-stats">
            <header class="app-header">
                <div class="header-brand">
                    <div class="header-logo">
                        <img src="logo.png" alt="DG Logo" />
                    </div>
                    <div>
                        <div class="header-name">GestaScreen DZ</div>
                        <div class="header-sub">
                            Tableau de bord statistique
                        </div>
                    </div>
                </div>
                <div class="header-actions">
                    <button
                        class="btn btn-primary btn-sm"
                        onclick="exportStats()"
                    >
                        📤 Exporter
                    </button>
                    <button class="btn btn-danger btn-sm" onclick="doLogout()">
                        Déconnexion
                    </button>
                </div>
            </header>
            <main class="main-content">
                <button class="back-btn" onclick="goHome()">
                    ← Retour au tableau de bord
                </button>
                <div class="form-page-header">
                    <h2>Statistiques — Diabète Gestationnel</h2>
                    <p id="stats-subtitle">Analyse des données collectées</p>
                </div>
                <div class="stats-summary" id="stats-summary"></div>
                <div class="charts-grid">
                    <div class="chart-card">
                        <h3>Fréquence du DG</h3>
                        <div class="chart-wrap">
                            <canvas id="chart-dg"></canvas>
                        </div>
                    </div>
                    <div class="chart-card">
                        <h3>Répartition par tranche d'âge</h3>
                        <div class="chart-wrap">
                            <canvas id="chart-age"></canvas>
                        </div>
                    </div>
                    <div class="chart-card">
                        <h3>IMC avant grossesse</h3>
                        <div class="chart-wrap">
                            <canvas id="chart-imc"></canvas>
                        </div>
                    </div>
                    <div class="chart-card">
                        <h3>Antécédents familiaux de diabète</h3>
                        <div class="chart-wrap">
                            <canvas id="chart-atcd"></canvas>
                        </div>
                    </div>
                </div>
                <div class="charts-grid">
                    <div class="chart-card">
                        <h3>Activité physique</h3>
                        <div class="chart-wrap">
                            <canvas id="chart-activite"></canvas>
                        </div>
                    </div>
                    <div class="chart-card">
                        <h3>Complications associées</h3>
                        <div class="chart-wrap">
                            <canvas id="chart-complic"></canvas>
                        </div>
                    </div>
                </div>
            </main>
        </div>

        <!-- ===== MODAL: IMPORT ===== -->
        <div class="modal-overlay" id="modal-import">
            <div class="modal">
                <div class="modal-header">
                    <h3>📥 Importer des données patients</h3>
                    <button class="modal-close" onclick="closeImportModal()">
                        ✕
                    </button>
                </div>
                <div class="modal-body">
                    <p class="import-note">
                        Collez un tableau JSON de patientes ci-dessous. Les
                        données seront <strong>ajoutées</strong> aux données
                        existantes (sans suppression).
                    </p>
                    <textarea
                        class="json-textarea"
                        id="import-json"
                        placeholder='[{"code":"P-001","age":28,...},...]'
                    ></textarea>
                    <div class="import-success" id="import-success">
                        ✅ Importation réussie !
                    </div>
                    <div class="import-error" id="import-error"></div>
                </div>
                <div class="modal-footer">
                    <button class="btn btn-ghost" onclick="downloadTemplate()">
                        ⬇ Télécharger le modèle JSON
                    </button>
                    <button
                        class="btn btn-secondary"
                        onclick="closeImportModal()"
                    >
                        Annuler
                    </button>
                    <button class="btn btn-primary" onclick="importData()">
                        Importer
                    </button>
                </div>
            </div>
        </div>

        <!-- ===== MODAL: CONFIRM DELETE ===== -->
        <div class="modal-overlay" id="modal-confirm">
            <div class="modal" style="max-width: 400px">
                <div class="modal-header">
                    <h3>Confirmer la suppression</h3>
                    <button class="modal-close" onclick="closeConfirm()">
                        ✕
                    </button>
                </div>
                <div class="confirm-modal-body">
                    <div class="icon">🗑️</div>
                    <p>
                        <strong
                            >Voulez-vous vraiment supprimer cette patiente
                            ?</strong
                        >
                    </p>
                    <p>Cette action est irréversible.</p>
                </div>
                <div class="modal-footer" style="justify-content: center">
                    <button class="btn btn-ghost" onclick="closeConfirm()">
                        Annuler
                    </button>
                    <button class="btn btn-danger" id="confirm-del-btn">
                        Supprimer
                    </button>
                </div>
            </div>
        </div>

        <script>
            // ============================================================
            // DATA LAYER
            // ============================================================
            const STORAGE_KEY = "gestascreen_patients";
            const SESSION_KEY = "gestascreen_session";

            function getPatients() {
                try {
                    return JSON.parse(
                        localStorage.getItem(STORAGE_KEY) || "[]",
                    );
                } catch {
                    return [];
                }
            }
            function savePatients(arr) {
                localStorage.setItem(STORAGE_KEY, JSON.stringify(arr));
            }
            function isLoggedIn() {
                return !!localStorage.getItem(SESSION_KEY);
            }

            // ============================================================
            // ROUTING
            // ============================================================
            function showPage(id) {
                document
                    .querySelectorAll(".page")
                    .forEach((p) => p.classList.remove("active"));
                document.getElementById(id).classList.add("active");
                window.scrollTo(0, 0);
            }
            function goHome() {
                showPage("page-home");
                renderHome();
            }
            function goStats() {
                showPage("page-stats");
                renderStats();
            }
            function goAddPatient() {
                currentEditId = null;
                showPage("page-form");
                resetForm();
                document.getElementById("form-title").textContent =
                    "Ajouter une patiente";
            }
            function goEditPatient(id) {
                currentEditId = id;
                showPage("page-form");
                loadFormForEdit(id);
                document.getElementById("form-title").textContent =
                    "Modifier la patiente";
            }

            // ============================================================
            // AUTH
            // ============================================================
            function doLogin() {
                const e = document.getElementById("login-email").value.trim();
                const p = document.getElementById("login-pwd").value;
                const err = document.getElementById("login-error");
                if (!e || !p) {
                    err.style.display = "block";
                    err.textContent = "Veuillez remplir tous les champs.";
                    return;
                }
                // Accept any non-empty credentials
                err.style.display = "none";
                localStorage.setItem(SESSION_KEY, "1");
                goHome();
            }
            function doLogout() {
                localStorage.removeItem(SESSION_KEY);
                showPage("page-login");
            }
            document
                .getElementById("login-pwd")
                .addEventListener("keydown", (e) => {
                    if (e.key === "Enter") doLogin();
                });
            document
                .getElementById("login-email")
                .addEventListener("keydown", (e) => {
                    if (e.key === "Enter") doLogin();
                });

            // ============================================================
            // HOME DASHBOARD
            // ============================================================
            function renderHome() {
                const pts = getPatients();
                const pos = pts.filter((p) => p.diagnostic === "Oui").length;
                const neg = pts.filter((p) => p.diagnostic === "Non").length;
                document.getElementById("stat-grid").innerHTML = `
    <div class="stat-card green">
      <div class="stat-label">Total patientes</div>
      <div class="stat-value">${pts.length}</div>
      <div class="stat-sub">Enregistrées</div>
    </div>
    <div class="stat-card blue">
      <div class="stat-label">DG Positif</div>
      <div class="stat-value">${pos}</div>
      <div class="stat-sub">${pts.length ? Math.round((pos / pts.length) * 100) : 0}% des cas</div>
    </div>
    <div class="stat-card orange">
      <div class="stat-label">DG Négatif</div>
      <div class="stat-value">${neg}</div>
      <div class="stat-sub">${pts.length ? Math.round((neg / pts.length) * 100) : 0}% des cas</div>
    </div>
  `;
                renderTable();
            }

            function renderTable() {
                const pts = getPatients();
                const q =
                    (document.getElementById("search-input") || {}).value || "";
                const ql = q.toLowerCase();
                const filtered = pts.filter((p) => {
                    if (!ql) return true;
                    return (
                        (p.code || "").toLowerCase().includes(ql) ||
                        (p.age + "").includes(ql) ||
                        (p.residence || "").toLowerCase().includes(ql)
                    );
                });
                const tbody = document.getElementById("patient-tbody");
                if (!filtered.length) {
                    tbody.innerHTML = `<tr><td colspan="8"><div class="empty-state"><div class="empty-icon">📋</div><p>Aucune patiente trouvée</p></div></td></tr>`;
                    return;
                }
                tbody.innerHTML = filtered
                    .map((p) => {
                        const badge =
                            p.diagnostic === "Oui"
                                ? "badge-positive"
                                : p.diagnostic === "Non"
                                  ? "badge-negative"
                                  : "badge-pending";
                        const label =
                            p.diagnostic === "Oui"
                                ? "DG +"
                                : p.diagnostic === "Non"
                                  ? "DG −"
                                  : "—";
                        return `<tr>
      <td><strong>${esc(p.code || "—")}</strong></td>
      <td>${p.age || "—"} ans</td>
      <td>${esc(p.residence || "—")}</td>
      <td>${p.imc ? parseFloat(p.imc).toFixed(1) : "—"}</td>
      <td>${p.glycemie || "—"}</td>
      <td>${p.ageGestationnel || "—"} SA</td>
      <td><span class="badge ${badge}">${label}</span></td>
      <td><div class="action-btns">
        <button class="icon-btn" title="Modifier" onclick="goEditPatient('${p.id}')">✏️</button>
        <button class="icon-btn del" title="Supprimer" onclick="confirmDelete('${p.id}')">🗑️</button>
      </div></td>
    </tr>`;
                    })
                    .join("");
            }

            function esc(s) {
                const d = document.createElement("div");
                d.textContent = s;
                return d.innerHTML;
            }

            // ============================================================
            // DELETE
            // ============================================================
            let deleteTargetId = null;
            function confirmDelete(id) {
                deleteTargetId = id;
                document.getElementById("modal-confirm").classList.add("open");
            }
            function closeConfirm() {
                document
                    .getElementById("modal-confirm")
                    .classList.remove("open");
                deleteTargetId = null;
            }
            document.getElementById("confirm-del-btn").onclick = function () {
                if (!deleteTargetId) return;
                const pts = getPatients().filter(
                    (p) => p.id !== deleteTargetId,
                );
                savePatients(pts);
                closeConfirm();
                toast("Patiente supprimée.");
                renderHome();
            };

            // ============================================================
            // FORM
            // ============================================================
            let currentEditId = null;

            function resetForm() {
                [
                    "f-code",
                    "f-age",
                    "f-residence",
                    "f-instruction",
                    "f-profession",
                    "f-matrimoniale",
                    "f-nb-grossesses",
                    "f-parite",
                    "f-poids-bebe",
                    "f-age-gest",
                    "f-activite",
                    "f-alimentation",
                    "f-boissons",
                    "f-taille",
                    "f-poids-avant",
                    "f-poids-actuel",
                    "f-glycemie",
                    "f-prise-charge",
                ].forEach((id) => {
                    const el = document.getElementById(id);
                    if (el) el.value = "";
                });
                document
                    .querySelectorAll('input[name="diabete-avant"]')
                    .forEach((r) => (r.checked = r.value === "Non"));
                document
                    .querySelectorAll('input[name="atcd-dg"]')
                    .forEach((r) => (r.checked = r.value === "Non"));
                document
                    .querySelectorAll('input[name="type-grossesse"]')
                    .forEach((r) => (r.checked = r.value === "Simple"));
                document
                    .querySelectorAll('input[name="diag-override"]')
                    .forEach((r) => (r.checked = r.value === "auto"));
                document
                    .querySelectorAll(
                        "#atcd-family input,#maladie-actuelle input,#complications input",
                    )
                    .forEach((c) => (c.checked = false));
                document.getElementById("imc-display").textContent = "—";
                document.getElementById("f-imc").value = "";
                setDGDisplay("", "");
            }

            function loadFormForEdit(id) {
                resetForm();
                const p = getPatients().find((x) => x.id === id);
                if (!p) return;
                const set = (fid, val) => {
                    const el = document.getElementById(fid);
                    if (el && val !== undefined && val !== null) el.value = val;
                };
                set("f-code", p.code);
                set("f-age", p.age);
                set("f-residence", p.residence);
                set("f-instruction", p.instruction);
                set("f-profession", p.profession);
                set("f-matrimoniale", p.matrimoniale);
                set("f-nb-grossesses", p.nbGrossesses);
                set("f-parite", p.parite);
                set("f-poids-bebe", p.poidsBebe);
                set("f-age-gest", p.ageGestationnel);
                set("f-activite", p.activite);
                set("f-alimentation", p.alimentation);
                set("f-boissons", p.boissons);
                set("f-taille", p.taille);
                set("f-poids-avant", p.poidsAvant);
                set("f-poids-actuel", p.poidsActuel);
                set("f-glycemie", p.glycemie);
                set("f-prise-charge", p.priseCharge);
                // Radios
                document
                    .querySelectorAll('input[name="diabete-avant"]')
                    .forEach((r) => (r.checked = r.value === p.diabeteAvant));
                document
                    .querySelectorAll('input[name="atcd-dg"]')
                    .forEach((r) => (r.checked = r.value === p.atcdDG));
                document
                    .querySelectorAll('input[name="type-grossesse"]')
                    .forEach((r) => (r.checked = r.value === p.typeGrossesse));
                // Checkboxes
                const setChecks = (groupId, arr) => {
                    document
                        .querySelectorAll(`#${groupId} input`)
                        .forEach(
                            (c) => (c.checked = (arr || []).includes(c.value)),
                        );
                };
                setChecks("atcd-family", p.atcdFamily);
                setChecks("maladie-actuelle", p.maladieActuelle);
                setChecks("complications", p.complications);
                // IMC
                if (p.imc) {
                    document.getElementById("imc-display").textContent =
                        parseFloat(p.imc).toFixed(2) + " kg/m²";
                    document.getElementById("f-imc").value = p.imc;
                }
                // Diagnostic
                setDGDisplay(p.diagnostic, p.glycemie);
                document.getElementById("f-diagnostic").value =
                    p.diagnostic || "";
                if (p.diagOverride) {
                    document
                        .querySelectorAll('input[name="diag-override"]')
                        .forEach(
                            (r) => (r.checked = r.value === p.diagOverride),
                        );
                }
            }

            function calcIMC() {
                const t = parseFloat(document.getElementById("f-taille").value);
                const w = parseFloat(
                    document.getElementById("f-poids-avant").value,
                );
                const disp = document.getElementById("imc-display");
                if (t > 0 && w > 0) {
                    const imc = w / ((t / 100) * (t / 100));
                    const imcR = parseFloat(imc.toFixed(2));
                    disp.textContent = imcR + " kg/m²";
                    document.getElementById("f-imc").value = imcR;
                } else {
                    disp.textContent = "—";
                    document.getElementById("f-imc").value = "";
                }
            }

            function autoDiag() {
                const override = document.querySelector(
                    'input[name="diag-override"]:checked',
                );
                if (override && override.value !== "auto") return;
                const g = parseFloat(
                    document.getElementById("f-glycemie").value,
                );
                if (isNaN(g)) {
                    setDGDisplay("", "");
                    document.getElementById("f-diagnostic").value = "";
                    return;
                }
                const diag = g >= 0.92 ? "Oui" : "Non";
                setDGDisplay(diag, g);
                document.getElementById("f-diagnostic").value = diag;
            }

            function overrideDiag(val) {
                setDGDisplay(val, document.getElementById("f-glycemie").value);
                document.getElementById("f-diagnostic").value = val;
            }

            function setDGDisplay(diag, g) {
                const el = document.getElementById("dg-display");
                if (!diag) {
                    el.className = "dg-display dg-na";
                    el.textContent = "— Entrez la glycémie —";
                    return;
                }
                if (diag === "Oui") {
                    el.className = "dg-display dg-pos";
                    el.innerHTML = "🔴 DG Positif (≥ 0.92 g/L)";
                } else {
                    el.className = "dg-display dg-neg";
                    el.innerHTML = "🟢 DG Négatif (< 0.92 g/L)";
                }
            }

            function getChecked(groupId) {
                return [
                    ...document.querySelectorAll(`#${groupId} input:checked`),
                ].map((c) => c.value);
            }
            function getRadio(name) {
                const r = document.querySelector(
                    `input[name="${name}"]:checked`,
                );
                return r ? r.value : "";
            }

            function savePatient() {
                const code = document.getElementById("f-code").value.trim();
                const age = document.getElementById("f-age").value;
                const glycemie = document.getElementById("f-glycemie").value;
                const taille = document.getElementById("f-taille").value;
                const poidsAvant =
                    document.getElementById("f-poids-avant").value;
                const diag = document.getElementById("f-diagnostic").value;

                if (!code) {
                    toast("⚠ Le code participante est requis.");
                    return;
                }
                if (!age) {
                    toast("⚠ L'âge est requis.");
                    return;
                }
                if (!taille || !poidsAvant) {
                    toast(
                        "⚠ La taille et le poids avant grossesse sont requis.",
                    );
                    return;
                }
                if (!glycemie) {
                    toast("⚠ La valeur de glycémie est requise.");
                    return;
                }

                // Check for duplicate code (on add)
                const pts = getPatients();
                if (!currentEditId && pts.find((p) => p.code === code)) {
                    toast("⚠ Ce code participante existe déjà.");
                    return;
                }

                const patient = {
                    id:
                        currentEditId ||
                        "p_" +
                            Date.now() +
                            "_" +
                            Math.random().toString(36).slice(2, 7),
                    code,
                    age: parseInt(age) || null,
                    residence: document.getElementById("f-residence").value,
                    instruction: document.getElementById("f-instruction").value,
                    profession: document.getElementById("f-profession").value,
                    matrimoniale:
                        document.getElementById("f-matrimoniale").value,
                    diabeteAvant: getRadio("diabete-avant"),
                    atcdFamily: getChecked("atcd-family"),
                    maladieActuelle: getChecked("maladie-actuelle"),
                    nbGrossesses:
                        parseInt(
                            document.getElementById("f-nb-grossesses").value,
                        ) || null,
                    parite:
                        parseInt(document.getElementById("f-parite").value) ||
                        null,
                    poidsBebe: document.getElementById("f-poids-bebe").value,
                    atcdDG: getRadio("atcd-dg"),
                    ageGestationnel:
                        parseInt(document.getElementById("f-age-gest").value) ||
                        null,
                    typeGrossesse: getRadio("type-grossesse"),
                    activite: document.getElementById("f-activite").value,
                    alimentation:
                        document.getElementById("f-alimentation").value,
                    boissons: document.getElementById("f-boissons").value,
                    taille: parseFloat(taille) || null,
                    poidsAvant: parseFloat(poidsAvant) || null,
                    poidsActuel:
                        parseFloat(
                            document.getElementById("f-poids-actuel").value,
                        ) || null,
                    imc: document.getElementById("f-imc").value || null,
                    glycemie: parseFloat(glycemie) || null,
                    diagnostic: diag || "Non",
                    diagOverride: getRadio("diag-override"),
                    priseCharge:
                        document.getElementById("f-prise-charge").value,
                    complications: getChecked("complications"),
                    createdAt: currentEditId
                        ? (pts.find((p) => p.id === currentEditId) || {})
                              .createdAt || new Date().toISOString()
                        : new Date().toISOString(),
                    updatedAt: new Date().toISOString(),
                };

                let updated;
                if (currentEditId) {
                    updated = pts.map((p) =>
                        p.id === currentEditId ? patient : p,
                    );
                } else {
                    updated = [...pts, patient];
                }
                savePatients(updated);
                toast(
                    currentEditId
                        ? "✅ Patiente modifiée avec succès."
                        : "✅ Patiente ajoutée avec succès.",
                );
                goHome();
            }

            // ============================================================
            // STATISTICS
            // ============================================================
            let chartInstances = {};
            function renderStats() {
                const pts = getPatients();
                document.getElementById("stats-subtitle").textContent =
                    `Basé sur ${pts.length} patiente(s) enregistrée(s)`;
                const pos = pts.filter((p) => p.diagnostic === "Oui").length;
                const neg = pts.filter((p) => p.diagnostic === "Non").length;
                const avgAge = pts.length
                    ? Math.round(
                          pts.reduce((a, p) => a + (p.age || 0), 0) /
                              pts.length,
                      )
                    : 0;
                const avgGly = pts.length
                    ? (
                          pts.reduce((a, p) => a + (p.glycemie || 0), 0) /
                          pts.length
                      ).toFixed(2)
                    : 0;
                document.getElementById("stats-summary").innerHTML = `
    <div class="stat-row"><span class="lbl">Total patientes</span><span class="val">${pts.length}</span></div>
    <div class="stat-row"><span class="lbl">DG Positif</span><span class="val">${pos} (${pts.length ? Math.round((pos / pts.length) * 100) : 0}%)</span></div>
    <div class="stat-row"><span class="lbl">DG Négatif</span><span class="val">${neg} (${pts.length ? Math.round((neg / pts.length) * 100) : 0}%)</span></div>
    <div class="stat-row"><span class="lbl">Âge moyen</span><span class="val">${avgAge} ans</span></div>
    <div class="stat-row"><span class="lbl">Glycémie moyenne</span><span class="val">${avgGly} g/L</span></div>
  `;
                // Destroy old charts
                Object.values(chartInstances).forEach(
                    (c) => c.destroy && c.destroy(),
                );
                chartInstances = {};
                if (!pts.length) return;

                const primary = "#1A6B5A";
                const accent = "#2563EB";
                const warn = "#D97706";
                const danger = "#DC2626";

                // Chart 1: DG Pie
                chartInstances.dg = new Chart(
                    document.getElementById("chart-dg"),
                    {
                        type: "doughnut",
                        data: {
                            labels: ["DG Positif", "DG Négatif"],
                            datasets: [
                                {
                                    data: [pos, neg],
                                    backgroundColor: [danger, primary],
                                    borderWidth: 2,
                                    borderColor: "#fff",
                                },
                            ],
                        },
                        options: {
                            responsive: true,
                            maintainAspectRatio: false,
                            plugins: {
                                legend: { position: "bottom" },
                                tooltip: {
                                    callbacks: {
                                        label: (ctx) =>
                                            `${ctx.label}: ${ctx.raw} (${pts.length ? Math.round((ctx.raw / pts.length) * 100) : 0}%)`,
                                    },
                                },
                            },
                        },
                    },
                );

                // Chart 2: Age groups
                const ageBuckets = {
                    "<20": 0,
                    "20-24": 0,
                    "25-29": 0,
                    "30-34": 0,
                    "35-39": 0,
                    "≥40": 0,
                };
                pts.forEach((p) => {
                    const a = p.age || 0;
                    if (a < 20) ageBuckets["<20"]++;
                    else if (a < 25) ageBuckets["20-24"]++;
                    else if (a < 30) ageBuckets["25-29"]++;
                    else if (a < 35) ageBuckets["30-34"]++;
                    else if (a < 40) ageBuckets["35-39"]++;
                    else ageBuckets["≥40"]++;
                });
                chartInstances.age = new Chart(
                    document.getElementById("chart-age"),
                    {
                        type: "bar",
                        data: {
                            labels: Object.keys(ageBuckets),
                            datasets: [
                                {
                                    label: "Patientes",
                                    data: Object.values(ageBuckets),
                                    backgroundColor: accent,
                                    borderRadius: 6,
                                },
                            ],
                        },
                        options: {
                            responsive: true,
                            maintainAspectRatio: false,
                            plugins: { legend: { display: false } },
                            scales: {
                                y: {
                                    beginAtZero: true,
                                    ticks: { stepSize: 1 },
                                },
                            },
                        },
                    },
                );

                // Chart 3: IMC categories
                const imcBuckets = {
                    "Insuffisance (<18.5)": 0,
                    "Normal (18.5-24.9)": 0,
                    "Surpoids (25-29.9)": 0,
                    "Obésité (≥30)": 0,
                };
                pts.forEach((p) => {
                    const i = parseFloat(p.imc) || 0;
                    if (i < 18.5) imcBuckets["Insuffisance (<18.5)"]++;
                    else if (i < 25) imcBuckets["Normal (18.5-24.9)"]++;
                    else if (i < 30) imcBuckets["Surpoids (25-29.9)"]++;
                    else if (i > 0) imcBuckets["Obésité (≥30)"]++;
                });
                chartInstances.imc = new Chart(
                    document.getElementById("chart-imc"),
                    {
                        type: "bar",
                        data: {
                            labels: Object.keys(imcBuckets),
                            datasets: [
                                {
                                    label: "Patientes",
                                    data: Object.values(imcBuckets),
                                    backgroundColor: [
                                        accent,
                                        primary,
                                        warn,
                                        danger,
                                    ],
                                    borderRadius: 6,
                                },
                            ],
                        },
                        options: {
                            responsive: true,
                            maintainAspectRatio: false,
                            plugins: { legend: { display: false } },
                            scales: {
                                y: {
                                    beginAtZero: true,
                                    ticks: { stepSize: 1 },
                                },
                            },
                        },
                    },
                );

                // Chart 4: ATCD family
                const atcdCount = {};
                pts.forEach((p) =>
                    (p.atcdFamily || []).forEach((f) => {
                        atcdCount[f] = (atcdCount[f] || 0) + 1;
                    }),
                );
                chartInstances.atcd = new Chart(
                    document.getElementById("chart-atcd"),
                    {
                        type: "doughnut",
                        data: {
                            labels: Object.keys(atcdCount) || ["—"],
                            datasets: [
                                {
                                    data: Object.values(atcdCount) || [1],
                                    backgroundColor: [
                                        primary,
                                        accent,
                                        warn,
                                        danger,
                                        "#6B7280",
                                    ],
                                    borderWidth: 2,
                                    borderColor: "#fff",
                                },
                            ],
                        },
                        options: {
                            responsive: true,
                            maintainAspectRatio: false,
                            plugins: { legend: { position: "bottom" } },
                        },
                    },
                );

                // Chart 5: Activité physique
                const actCount = {};
                pts.forEach((p) => {
                    if (p.activite)
                        actCount[p.activite] = (actCount[p.activite] || 0) + 1;
                });
                chartInstances.activite = new Chart(
                    document.getElementById("chart-activite"),
                    {
                        type: "bar",
                        data: {
                            labels: Object.keys(actCount) || ["—"],
                            datasets: [
                                {
                                    label: "Patientes",
                                    data: Object.values(actCount) || [0],
                                    backgroundColor: primary,
                                    borderRadius: 6,
                                },
                            ],
                        },
                        options: {
                            responsive: true,
                            maintainAspectRatio: false,
                            plugins: { legend: { display: false } },
                            scales: {
                                y: {
                                    beginAtZero: true,
                                    ticks: { stepSize: 1 },
                                },
                            },
                        },
                    },
                );

                // Chart 6: Complications
                const compCount = {};
                pts.forEach((p) =>
                    (p.complications || []).forEach((c) => {
                        compCount[c] = (compCount[c] || 0) + 1;
                    }),
                );
                chartInstances.complic = new Chart(
                    document.getElementById("chart-complic"),
                    {
                        type: "bar",
                        data: {
                            labels: Object.keys(compCount) || ["—"],
                            datasets: [
                                {
                                    label: "Patientes",
                                    data: Object.values(compCount) || [0],
                                    backgroundColor: [
                                        danger,
                                        warn,
                                        accent,
                                        primary,
                                    ],
                                    borderRadius: 6,
                                },
                            ],
                        },
                        options: {
                            responsive: true,
                            maintainAspectRatio: false,
                            plugins: { legend: { display: false } },
                            scales: {
                                y: {
                                    beginAtZero: true,
                                    ticks: { stepSize: 1 },
                                },
                            },
                        },
                    },
                );
            }

            function exportStats() {
                toast("📤 Exporté avec succès ! (simulation)");
            }

            // ============================================================
            // IMPORT / EXPORT
            // ============================================================
            function showImportModal() {
                document.getElementById("import-json").value = "";
                document.getElementById("import-success").style.display =
                    "none";
                document.getElementById("import-error").style.display = "none";
                document.getElementById("modal-import").classList.add("open");
            }
            function closeImportModal() {
                document
                    .getElementById("modal-import")
                    .classList.remove("open");
            }

            function importData() {
                const raw = document.getElementById("import-json").value.trim();
                const suc = document.getElementById("import-success");
                const err = document.getElementById("import-error");
                suc.style.display = "none";
                err.style.display = "none";
                if (!raw) {
                    err.style.display = "block";
                    err.textContent = "❌ Veuillez coller des données JSON.";
                    return;
                }
                let arr;
                try {
                    arr = JSON.parse(raw);
                } catch (e) {
                    err.style.display = "block";
                    err.textContent = "❌ JSON invalide : " + e.message;
                    return;
                }
                if (!Array.isArray(arr)) {
                    err.style.display = "block";
                    err.textContent =
                        "❌ Les données doivent être un tableau JSON [ {...}, {...} ].";
                    return;
                }
                const existing = getPatients();
                const existCodes = new Set(existing.map((p) => p.code));
                let added = 0,
                    skipped = 0;
                arr.forEach((p) => {
                    const id =
                        p.id ||
                        "imp_" +
                            Date.now() +
                            "_" +
                            Math.random().toString(36).slice(2, 7);
                    const code = p.code || id;
                    if (existCodes.has(code)) {
                        skipped++;
                        return;
                    }
                    existing.push({
                        ...p,
                        id,
                        code,
                        createdAt: p.createdAt || new Date().toISOString(),
                        updatedAt: new Date().toISOString(),
                    });
                    existCodes.add(code);
                    added++;
                });
                savePatients(existing);
                suc.style.display = "block";
                suc.textContent = `✅ ${added} patiente(s) importée(s). ${skipped} ignorée(s) (code déjà existant).`;
                renderHome();
            }

            const TEMPLATE = [
                {
                    code: "P-001",
                    age: 30,
                    residence: "Oran",
                    instruction: "Universitaire",
                    profession: "Enseignante",
                    matrimoniale: "Mariée",
                    diabeteAvant: "Non",
                    atcdFamily: ["Mère"],
                    maladieActuelle: ["Aucune"],
                    nbGrossesses: 2,
                    parite: 1,
                    poidsBebe: "3.4",
                    atcdDG: "Non",
                    ageGestationnel: 28,
                    typeGrossesse: "Simple",
                    activite: "Légère",
                    alimentation: "Mixte",
                    boissons: "Parfois",
                    taille: 163,
                    poidsAvant: 68,
                    poidsActuel: 76,
                    imc: 25.6,
                    glycemie: 0.95,
                    diagnostic: "Oui",
                    diagOverride: "auto",
                    priseCharge: "Suivi médical régulier",
                    complications: ["Aucune"],
                },
                {
                    code: "P-002",
                    age: 24,
                    residence: "Alger",
                    instruction: "Secondaire",
                    profession: "Femme au foyer",
                    matrimoniale: "Mariée",
                    diabeteAvant: "Non",
                    atcdFamily: ["Aucun"],
                    maladieActuelle: ["Aucune"],
                    nbGrossesses: 1,
                    parite: 0,
                    poidsBebe: "",
                    atcdDG: "Non",
                    ageGestationnel: 32,
                    typeGrossesse: "Simple",
                    activite: "Sédentaire",
                    alimentation: "Équilibrée",
                    boissons: "Rarement",
                    taille: 160,
                    poidsAvant: 58,
                    poidsActuel: 66,
                    imc: 22.7,
                    glycemie: 0.85,
                    diagnostic: "Non",
                    diagOverride: "auto",
                    priseCharge: "Pas de prise en charge",
                    complications: ["Aucune"],
                },
            ];

            function downloadTemplate() {
                const blob = new Blob([JSON.stringify(TEMPLATE, null, 2)], {
                    type: "application/json",
                });
                const a = document.createElement("a");
                a.href = URL.createObjectURL(blob);
                a.download = "gestascreen_modele.json";
                a.click();
            }

            // ============================================================
            // TOAST
            // ============================================================
            function toast(msg) {
                const t = document.getElementById("toast");
                t.textContent = msg;
                t.classList.add("show");
                setTimeout(() => t.classList.remove("show"), 3200);
            }

            // ============================================================
            // INIT
            // ============================================================
            (function init() {
                if (isLoggedIn()) {
                    goHome();
                } else {
                    showPage("page-login");
                }
            })();
        </script>
    </body>
</html>
