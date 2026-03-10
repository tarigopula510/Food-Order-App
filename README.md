<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FeastTogether — Intuitive Online Food Ordering</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@500;600;700&family=DM+Sans:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
:root {
  --rose:#e8637a; --rose-light:#f5d0d8; --rose-pale:#fdf0f2;
  --peach:#f4a26a; --peach-pale:#fef5ec;
  --sage:#6aab7a; --sage-pale:#eef6f1;
  --sky:#6aaccc; --sky-pale:#eaf4fa;
  --plum:#8b6bbf; --plum-pale:#f2eefa;
  --gold:#c9933a; --gold-pale:#fdf4e3;
  --ink:#1e1a1a; --ink-mid:#4a4040; --ink-soft:#7a6e6e;
  --border:#ede8e8; --canvas:#faf8f6; --white:#ffffff;
  --shadow:0 2px 16px rgba(30,26,26,0.08);
  --shadow-hover:0 8px 32px rgba(30,26,26,0.14);
  --r:16px; --r-sm:10px; --r-lg:24px;
}
*,*::before,*::after{margin:0;padding:0;box-sizing:border-box;}
html{scroll-behavior:smooth;}
body{font-family:'DM Sans',sans-serif;background:var(--canvas);color:var(--ink);font-size:15px;line-height:1.6;-webkit-font-smoothing:antialiased;}
img{display:block;max-width:100%;}
button{cursor:pointer;font-family:'DM Sans',sans-serif;}
input{font-family:'DM Sans',sans-serif;}
::-webkit-scrollbar{width:5px;}
::-webkit-scrollbar-track{background:var(--canvas);}
::-webkit-scrollbar-thumb{background:var(--rose-light);border-radius:3px;}

/* PAGES */
.page{display:none;}
.page.active{display:block;}

/* ─── LOGIN ─── */
#loginPage{min-height:100vh;display:flex;}
.login-split{display:grid;grid-template-columns:1.1fr 0.9fr;width:100%;min-height:100vh;}
.login-visual{position:relative;overflow:hidden;background:#1a1010;}
.lv-grid{display:grid;grid-template-columns:1fr 1fr;grid-template-rows:1fr 1fr 1fr;height:100%;gap:3px;}
.lv-img{width:100%;height:100%;object-fit:cover;filter:brightness(0.82) saturate(1.1);}
.lv-span2{grid-column:span 2;}
.lv-overlay{position:absolute;inset:0;background:linear-gradient(160deg,rgba(232,99,122,0.22),rgba(139,107,191,0.18));pointer-events:none;}
.lv-brand{position:absolute;bottom:48px;left:48px;color:#fff;z-index:2;}
.lv-brand h1{font-family:'Playfair Display',serif;font-size:2.6rem;font-weight:700;line-height:1.15;text-shadow:0 2px 12px rgba(0,0,0,0.35);}
.lv-brand p{font-size:0.95rem;opacity:0.88;margin-top:6px;font-weight:300;letter-spacing:0.02em;}
.lv-badge{position:absolute;top:36px;left:36px;background:rgba(255,255,255,0.15);backdrop-filter:blur(12px);border:1px solid rgba(255,255,255,0.25);padding:10px 18px;border-radius:40px;color:#fff;font-size:0.82rem;font-weight:600;letter-spacing:0.05em;}
.login-form-panel{display:flex;flex-direction:column;justify-content:center;padding:64px 56px;background:var(--white);}
.form-logo{font-family:'Playfair Display',serif;font-size:1.5rem;font-weight:600;color:var(--rose);margin-bottom:48px;}
.login-tabs{display:flex;border:1.5px solid var(--border);border-radius:var(--r-sm);overflow:hidden;margin-bottom:36px;width:fit-content;}
.ltab{padding:10px 28px;border:none;background:transparent;font-size:0.88rem;font-weight:600;color:var(--ink-soft);}
.ltab.active{background:var(--rose);color:#fff;}
.lform-title{font-family:'Playfair Display',serif;font-size:1.9rem;color:var(--ink);margin-bottom:6px;}
.lform-sub{color:var(--ink-soft);font-size:0.88rem;margin-bottom:32px;}
.fgroup{margin-bottom:20px;}
.fgroup label{display:block;font-size:0.8rem;font-weight:600;letter-spacing:0.06em;text-transform:uppercase;color:var(--ink-mid);margin-bottom:8px;}
.fgroup input{width:100%;padding:13px 16px;border:1.5px solid var(--border);border-radius:var(--r-sm);background:var(--canvas);font-size:0.95rem;color:var(--ink);outline:none;transition:border-color 0.2s,box-shadow 0.2s;}
.fgroup input:focus{border-color:var(--rose);box-shadow:0 0 0 3px rgba(232,99,122,0.1);background:var(--white);}
.btn-primary{width:100%;padding:14px;background:var(--rose);color:#fff;border:none;border-radius:var(--r-sm);font-size:0.95rem;font-weight:600;letter-spacing:0.02em;box-shadow:0 4px 14px rgba(232,99,122,0.28);}
.btn-primary:hover{background:#d45570;}
.form-alt{text-align:center;margin-top:18px;font-size:0.85rem;color:var(--ink-soft);}
.form-alt a{color:var(--rose);font-weight:600;cursor:pointer;text-decoration:none;}
.form-alt a:hover{text-decoration:underline;}
.lform-section{display:none;}
.lform-section.active{display:block;}
.login-stats{display:flex;gap:32px;margin-top:40px;padding-top:32px;border-top:1.5px solid var(--border);}
.lstat-num{font-family:'Playfair Display',serif;font-size:1.4rem;font-weight:700;color:var(--rose);}
.lstat-lbl{font-size:0.78rem;color:var(--ink-soft);margin-top:2px;}

/* ─── NAV ─── */
nav{position:sticky;top:0;z-index:100;background:rgba(250,248,246,0.96);backdrop-filter:blur(16px);border-bottom:1.5px solid var(--border);height:66px;display:flex;align-items:center;padding:0 40px;gap:40px;}
.nav-logo{font-family:'Playfair Display',serif;font-size:1.3rem;font-weight:600;color:var(--rose);white-space:nowrap;flex-shrink:0;}
.nav-links{display:flex;gap:2px;flex:1;}
.nav-link{padding:7px 16px;border:none;background:transparent;font-size:0.86rem;font-weight:500;color:var(--ink-soft);border-radius:var(--r-sm);}
.nav-link:hover{background:var(--rose-pale);color:var(--rose);}
.nav-link.active{background:var(--rose-pale);color:var(--rose);font-weight:600;}
.nav-right{display:flex;align-items:center;gap:12px;margin-left:auto;}
.nav-chip{display:flex;align-items:center;gap:8px;background:var(--canvas);border:1.5px solid var(--border);padding:7px 14px;border-radius:40px;font-size:0.83rem;font-weight:500;color:var(--ink-mid);}
.nav-av{width:26px;height:26px;border-radius:50%;background:var(--rose);color:#fff;font-size:0.72rem;font-weight:700;display:flex;align-items:center;justify-content:center;}
.nav-cart{display:flex;align-items:center;gap:8px;background:var(--rose);color:#fff;border:none;padding:9px 20px;border-radius:40px;font-size:0.86rem;font-weight:600;}
.nav-cart:hover{background:#d45570;}
.cart-badge{background:#fff;color:var(--rose);border-radius:50%;width:20px;height:20px;font-size:0.72rem;font-weight:700;display:flex;align-items:center;justify-content:center;}

/* ─── HERO ─── */
.hero{display:grid;grid-template-columns:1fr 1fr;min-height:480px;background:var(--rose-pale);overflow:hidden;}
.hero-content{padding:72px 64px;display:flex;flex-direction:column;justify-content:center;}
.hero-eyebrow{font-size:0.78rem;font-weight:600;letter-spacing:0.12em;text-transform:uppercase;color:var(--rose);margin-bottom:16px;display:flex;align-items:center;gap:8px;}
.hero-eyebrow::before{content:'';display:inline-block;width:28px;height:1.5px;background:var(--rose);}
.hero h1{font-family:'Playfair Display',serif;font-size:3rem;font-weight:700;line-height:1.18;color:var(--ink);margin-bottom:20px;}
.hero h1 em{color:var(--rose);font-style:normal;}
.hero-sub{color:var(--ink-soft);font-size:1rem;max-width:400px;margin-bottom:36px;}
.hero-search{display:flex;max-width:420px;border:1.5px solid var(--border);border-radius:var(--r-sm);overflow:hidden;background:var(--white);box-shadow:var(--shadow);}
.hero-search input{flex:1;padding:13px 18px;border:none;outline:none;font-size:0.9rem;background:transparent;color:var(--ink);}
.hero-search button{background:var(--rose);color:#fff;border:none;padding:13px 22px;font-size:0.88rem;font-weight:600;}
.hero-stats{display:flex;gap:32px;margin-top:40px;}
.hstat-num{font-family:'Playfair Display',serif;font-size:1.5rem;font-weight:700;color:var(--ink);}
.hstat-lbl{font-size:0.78rem;color:var(--ink-soft);}
.hero-photos{position:relative;overflow:hidden;}
.hero-photos-grid{display:grid;grid-template-columns:1fr 1fr;grid-template-rows:1fr 1fr;height:100%;gap:3px;}
.hero-photos-grid img{width:100%;height:100%;object-fit:cover;}
.hp-tall{grid-row:span 2;}

/* ─── SECTIONS ─── */
.section{padding:56px 64px;}
.section+.section{padding-top:0;}
.section-eyebrow{font-size:0.75rem;font-weight:600;letter-spacing:0.1em;text-transform:uppercase;color:var(--rose);margin-bottom:6px;}
.section-title{font-family:'Playfair Display',serif;font-size:1.75rem;font-weight:600;color:var(--ink);margin-bottom:0;}
.section-title span{color:var(--rose);}

/* ─── CATEGORIES ─── */
.cat-strip{display:flex;gap:10px;overflow-x:auto;padding-bottom:4px;margin-bottom:32px;scrollbar-width:none;margin-top:20px;}
.cat-strip::-webkit-scrollbar{display:none;}
.cat-pill{display:flex;align-items:center;gap:8px;padding:9px 20px;border-radius:40px;border:1.5px solid var(--border);background:var(--white);font-size:0.84rem;font-weight:500;color:var(--ink-mid);white-space:nowrap;flex-shrink:0;}
.cat-pill:hover{border-color:var(--rose);color:var(--rose);}
.cat-pill.active{background:var(--rose);border-color:var(--rose);color:#fff;font-weight:600;}

/* ─── MENU CARDS ─── */
.menu-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(250px,1fr));gap:20px;}
.menu-card{background:var(--white);border-radius:var(--r);overflow:hidden;border:1.5px solid var(--border);box-shadow:var(--shadow);position:relative;}
.menu-card:hover{box-shadow:var(--shadow-hover);transform:translateY(-3px);transition:box-shadow 0.25s,transform 0.25s;}
.mc-img-wrap{position:relative;height:176px;overflow:hidden;background:var(--canvas);}
.mc-img{position:absolute;inset:0;width:100%;height:100%;object-fit:cover;z-index:1;}
.mc-badge{position:absolute;top:12px;left:12px;padding:4px 10px;border-radius:40px;font-size:0.72rem;font-weight:600;}
.badge-veg{background:#d4edd8;color:#2c7a38;}
.badge-nonveg{background:#fde0e0;color:#b02020;}
.badge-new{position:absolute;top:12px;right:12px;background:var(--gold);color:#fff;padding:4px 10px;border-radius:40px;font-size:0.7rem;font-weight:700;letter-spacing:0.05em;}
.mc-body{padding:16px 18px 18px;}
.mc-name{font-weight:600;font-size:0.95rem;color:var(--ink);margin-bottom:5px;line-height:1.3;}
.mc-desc{font-size:0.8rem;color:var(--ink-soft);line-height:1.5;margin-bottom:14px;display:-webkit-box;-webkit-line-clamp:2;-webkit-box-orient:vertical;overflow:hidden;}
.mc-footer{display:flex;align-items:center;justify-content:space-between;}
.mc-price{font-family:'Playfair Display',serif;font-size:1.05rem;font-weight:600;color:var(--ink);}
.mc-price sup{font-size:0.65em;vertical-align:super;font-family:'DM Sans',sans-serif;font-weight:600;}
.mc-add{padding:8px 18px;background:var(--rose);color:#fff;border:none;border-radius:var(--r-sm);font-size:0.82rem;font-weight:600;}
.mc-add:hover{background:#d45570;}
.qty-ctrl{display:flex;align-items:center;gap:10px;background:var(--rose-pale);border-radius:var(--r-sm);padding:4px 10px;}
.qty-btn{width:24px;height:24px;border-radius:50%;border:1.5px solid var(--rose);background:transparent;color:var(--rose);font-size:1rem;font-weight:700;display:flex;align-items:center;justify-content:center;line-height:1;}
.qty-btn:hover{background:var(--rose);color:#fff;}
.qty-num{font-weight:700;font-size:0.9rem;color:var(--rose);min-width:18px;text-align:center;}

/* ─── PROFILE BAR ─── */
.profile-bar{display:none;align-items:center;gap:16px;background:var(--white);border:1.5px solid var(--border);border-radius:var(--r);padding:16px 22px;margin-bottom:24px;box-shadow:var(--shadow);}
.pb-av{width:44px;height:44px;border-radius:50%;background:var(--rose);color:#fff;font-size:1rem;display:flex;align-items:center;justify-content:center;flex-shrink:0;font-weight:700;}
.pb-label{font-size:0.75rem;color:var(--ink-soft);margin-bottom:4px;letter-spacing:0.04em;}
.pb-name{font-weight:700;font-size:0.92rem;}
.pb-tags{display:flex;flex-wrap:wrap;gap:6px;margin-top:6px;}
.pb-tag{padding:3px 12px;background:var(--rose-pale);color:var(--rose);border-radius:20px;font-size:0.74rem;font-weight:600;}
.sug-retake{padding:8px 16px;background:var(--plum);color:#fff;border:none;border-radius:var(--r-sm);font-size:0.8rem;font-weight:600;margin-left:auto;flex-shrink:0;}

/* ─── SUGGESTED BANNER ─── */
.sug-banner{display:flex;align-items:center;gap:20px;background:var(--plum-pale);border:1.5px solid #c9b8e8;border-radius:var(--r);padding:20px 24px;margin-bottom:24px;}
.sug-icon{width:48px;height:48px;background:var(--plum);border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:1.4rem;flex-shrink:0;}
.sug-text h4{font-weight:700;font-size:0.92rem;color:var(--plum);}
.sug-text p{font-size:0.8rem;color:var(--ink-soft);margin-top:2px;}

/* ─── CART ─── */
.cart-overlay{position:fixed;inset:0;background:rgba(30,26,26,0.42);z-index:200;display:none;}
.cart-overlay.open{display:block;}
.cart-drawer{position:fixed;top:0;right:0;width:400px;height:100%;background:var(--white);z-index:201;display:flex;flex-direction:column;box-shadow:-4px 0 32px rgba(30,26,26,0.12);transform:translateX(100%);transition:transform 0.3s cubic-bezier(0.4,0,0.2,1);}
.cart-drawer.open{transform:translateX(0);}
.cart-head{padding:24px 28px 20px;border-bottom:1.5px solid var(--border);display:flex;align-items:center;justify-content:space-between;}
.cart-head h3{font-family:'Playfair Display',serif;font-size:1.25rem;color:var(--ink);}
.cart-close-btn{width:32px;height:32px;border-radius:50%;border:1.5px solid var(--border);background:var(--canvas);color:var(--ink-soft);font-size:1rem;display:flex;align-items:center;justify-content:center;}
.cart-close-btn:hover{background:var(--rose-pale);color:var(--rose);}
.cart-body{flex:1;overflow-y:auto;padding:20px 28px;}
.cart-empty{text-align:center;padding:60px 20px;color:var(--ink-soft);}
.cart-empty-icon{width:64px;height:64px;background:var(--rose-pale);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:1.8rem;margin:0 auto 16px;}
.cart-empty h4{font-size:0.95rem;color:var(--ink-mid);margin-bottom:4px;}
.cart-item{display:flex;gap:14px;padding:14px 0;border-bottom:1px solid var(--border);align-items:center;}
.ci-thumb{width:58px;height:52px;border-radius:var(--r-sm);object-fit:cover;background:var(--canvas);flex-shrink:0;}
.ci-info{flex:1;}
.ci-name{font-weight:600;font-size:0.88rem;line-height:1.3;}
.ci-price{font-size:0.82rem;color:var(--rose);font-weight:600;margin-top:2px;}
.ci-qty{display:flex;align-items:center;gap:8px;}
.ci-del{background:none;border:none;color:var(--border);font-size:1.1rem;padding:2px;line-height:1;}
.ci-del:hover{color:#d45570;}
.cart-foot{padding:20px 28px 28px;border-top:1.5px solid var(--border);}
.cart-row{display:flex;justify-content:space-between;font-size:0.85rem;color:var(--ink-soft);padding:4px 0;}
.cart-row.total{font-size:1rem;font-weight:700;color:var(--ink);border-top:1px solid var(--border);margin-top:8px;padding-top:12px;}
.cart-row.total span:last-child{color:var(--rose);}
.cart-savings{background:var(--sage-pale);color:var(--sage);font-size:0.78rem;font-weight:600;padding:8px 14px;border-radius:var(--r-sm);margin:12px 0 14px;text-align:center;}
.btn-outline-teal{width:100%;padding:12px;background:var(--sage-pale);color:var(--sage);border:1.5px solid #b4d8c0;border-radius:var(--r-sm);font-size:0.88rem;font-weight:600;margin-top:8px;}
.btn-outline-teal:hover{background:#d4edd8;}

/* ─── TRACKING ─── */
.tracking-wrap{display:grid;grid-template-columns:1fr 1fr;gap:28px;max-width:960px;}
.t-card{background:var(--white);border:1.5px solid var(--border);border-radius:var(--r-lg);padding:32px;box-shadow:var(--shadow);}
.t-card h3{font-family:'Playfair Display',serif;font-size:1.2rem;margin-bottom:6px;}
.t-card .sub{font-size:0.82rem;color:var(--ink-soft);margin-bottom:24px;}
.search-bar{display:flex;border:1.5px solid var(--border);border-radius:var(--r-sm);overflow:hidden;margin-bottom:28px;background:var(--white);}
.search-bar input{flex:1;padding:12px 16px;border:none;outline:none;font-size:0.9rem;color:var(--ink);background:transparent;}
.search-bar button{padding:12px 20px;background:var(--rose);color:#fff;border:none;font-size:0.85rem;font-weight:600;}
.track-steps{display:flex;flex-direction:column;}
.track-step{display:flex;gap:16px;padding-bottom:24px;position:relative;}
.track-step:not(:last-child)::after{content:'';position:absolute;left:15px;top:36px;bottom:0;width:2px;background:var(--border);}
.track-step.done::after{background:var(--sage);}
.ts-dot{width:32px;height:32px;border-radius:50%;border:2px solid var(--border);background:var(--white);display:flex;align-items:center;justify-content:center;flex-shrink:0;font-size:0.9rem;position:relative;z-index:1;}
.track-step.done .ts-dot{background:var(--sage);border-color:var(--sage);color:#fff;font-size:0.75rem;}
.track-step.active .ts-dot{background:var(--rose);border-color:var(--rose);color:#fff;font-size:0.75rem;box-shadow:0 0 0 4px rgba(232,99,122,0.18);}
.ts-info h4{font-weight:600;font-size:0.9rem;line-height:1.3;}
.ts-info p{font-size:0.78rem;color:var(--ink-soft);margin-top:2px;}
.oscard{background:var(--rose-pale);border-radius:var(--r);padding:20px;margin-bottom:20px;}
.oscard-row{display:flex;justify-content:space-between;font-size:0.85rem;padding:5px 0;color:var(--ink-mid);}
.oscard-row.total{font-weight:700;color:var(--ink);padding-top:12px;border-top:1px solid var(--rose-light);}
.rider-img{width:100%;height:140px;object-fit:cover;border-radius:var(--r);margin-bottom:16px;}
.rider-row{display:flex;align-items:center;gap:12px;}
.rider-name{font-weight:600;font-size:0.9rem;}
.rider-rating{font-size:0.78rem;color:var(--ink-soft);}
.rider-call{margin-left:auto;padding:8px 16px;background:var(--sage);color:#fff;border:none;border-radius:var(--r-sm);font-size:0.8rem;font-weight:600;}
.map-img{width:100%;height:160px;object-fit:cover;border-radius:var(--r);margin-bottom:12px;opacity:0.85;}

/* ─── QUIZ ─── */
.quiz-wrap{max-width:660px;}
.q-prog-track{height:4px;background:var(--border);border-radius:2px;margin-bottom:36px;overflow:hidden;}
.q-prog-fill{height:100%;background:var(--rose);border-radius:2px;}
.q-step-label{font-size:0.78rem;font-weight:600;color:var(--ink-soft);letter-spacing:0.06em;text-transform:uppercase;margin-bottom:8px;}
.q-title{font-family:'Playfair Display',serif;font-size:1.5rem;font-weight:600;color:var(--ink);margin-bottom:28px;line-height:1.35;}
.quiz-options{display:grid;grid-template-columns:1fr 1fr;gap:14px;margin-bottom:36px;}
.quiz-opt{padding:20px 18px;border:1.5px solid var(--border);border-radius:var(--r);background:var(--white);text-align:left;cursor:pointer;}
.quiz-opt:hover{border-color:var(--rose);background:var(--rose-pale);}
.quiz-opt.selected{border-color:var(--rose);background:var(--rose-pale);box-shadow:0 0 0 3px rgba(232,99,122,0.12);}
.qopt-icon{font-size:1.8rem;margin-bottom:10px;display:block;}
.qopt-label{font-weight:600;font-size:0.88rem;color:var(--ink);}
.qopt-sub{font-size:0.78rem;color:var(--ink-soft);margin-top:3px;}
.quiz-nav{display:flex;align-items:center;justify-content:space-between;}
.btn-ghost{padding:11px 24px;border:1.5px solid var(--border);background:var(--white);border-radius:var(--r-sm);font-size:0.88rem;font-weight:600;color:var(--ink-soft);}
.btn-ghost:hover{border-color:var(--ink-mid);color:var(--ink);}
.btn-rose{padding:11px 28px;background:var(--rose);color:#fff;border:none;border-radius:var(--r-sm);font-size:0.9rem;font-weight:600;box-shadow:0 4px 14px rgba(232,99,122,0.28);}
.btn-rose:hover{background:#d45570;}
.quiz-result{display:none;}
.qr-strip{display:flex;flex-wrap:wrap;gap:8px;margin-bottom:28px;}
.qr-badge{padding:7px 16px;border-radius:40px;font-size:0.8rem;font-weight:600;border:1.5px solid transparent;}
.qr-badge.rose{background:var(--rose-pale);border-color:var(--rose-light);color:var(--rose);}
.qr-badge.sage{background:var(--sage-pale);border-color:#b4d8c0;color:var(--sage);}
.qr-badge.plum{background:var(--plum-pale);border-color:#c9b8e8;color:var(--plum);}
.qr-badge.peach{background:var(--peach-pale);border-color:#f5ccaa;color:var(--peach);}
.qr-badge.sky{background:var(--sky-pale);border-color:#a8d8ea;color:var(--sky);}
.recipe-grid{display:grid;grid-template-columns:1fr 1fr;gap:16px;margin-bottom:28px;}
.recipe-card{background:var(--white);border:1.5px solid var(--border);border-radius:var(--r);overflow:hidden;box-shadow:var(--shadow);}
.recipe-card-img{width:100%;height:120px;object-fit:cover;background:var(--canvas);}
.recipe-card-body{padding:14px 16px;}
.rc-title{font-weight:700;font-size:0.9rem;margin-bottom:4px;}
.rc-desc{font-size:0.78rem;color:var(--ink-soft);margin-bottom:8px;line-height:1.4;}
.rc-step{font-size:0.75rem;color:var(--ink-mid);font-style:italic;margin-bottom:8px;line-height:1.4;}
.recipe-tag{display:inline-block;padding:3px 10px;background:var(--rose-pale);color:var(--rose);border-radius:20px;font-size:0.7rem;font-weight:600;margin-right:4px;}
.recipe-tag.green{background:var(--sage-pale);color:var(--sage);}
.quiz-result-actions{display:flex;gap:12px;}
.quiz-result-actions button{flex:1;}

/* ─── GROUP ORDER ─── */
.group-wrap{display:grid;grid-template-columns:1.2fr 0.8fr;gap:28px;max-width:1000px;}
.g-card{background:var(--white);border:1.5px solid var(--border);border-radius:var(--r-lg);padding:32px;box-shadow:var(--shadow);}
.g-card h3{font-family:'Playfair Display',serif;font-size:1.15rem;margin-bottom:20px;color:var(--ink);padding-bottom:14px;border-bottom:1.5px solid var(--border);}
.session-hdr{display:flex;align-items:center;justify-content:space-between;margin-bottom:8px;}
.session-title{font-family:'Playfair Display',serif;font-size:1.35rem;color:var(--ink);}
.session-code{background:var(--plum-pale);color:var(--plum);padding:7px 16px;border-radius:40px;font-size:0.82rem;font-weight:700;letter-spacing:0.1em;}
.session-meta{font-size:0.82rem;color:var(--ink-soft);margin-bottom:24px;}
.invite-row{display:flex;gap:8px;margin-bottom:28px;}
.invite-row input{flex:1;padding:10px 14px;border:1.5px solid var(--border);border-radius:var(--r-sm);font-size:0.83rem;color:var(--ink-soft);background:var(--canvas);outline:none;}
.invite-row button{padding:10px 18px;background:var(--plum);color:#fff;border:none;border-radius:var(--r-sm);font-size:0.82rem;font-weight:600;}
.invite-row button:hover{background:#7455a8;}
.members-list{display:flex;flex-direction:column;gap:12px;margin-bottom:24px;}
.member-row{display:flex;align-items:center;gap:14px;padding:14px 16px;background:var(--canvas);border:1.5px solid var(--border);border-radius:var(--r);}
.member-av{width:40px;height:40px;border-radius:50%;background:var(--rose-pale);display:flex;align-items:center;justify-content:center;font-size:1.1rem;flex-shrink:0;border:2px solid var(--rose-light);}
.member-av.plum{background:var(--plum-pale);border-color:#c9b8e8;}
.member-av.sage{background:var(--sage-pale);border-color:#b4d8c0;}
.member-av.peach{background:var(--peach-pale);border-color:#f5ccaa;}
.member-name{font-weight:600;font-size:0.88rem;}
.member-items{font-size:0.78rem;color:var(--ink-soft);margin-top:2px;}
.member-amt{margin-left:auto;font-family:'Playfair Display',serif;font-size:1rem;font-weight:700;color:var(--ink);}
.add-member-btn{width:100%;padding:11px;border:1.5px dashed var(--border);background:transparent;border-radius:var(--r-sm);font-size:0.85rem;font-weight:600;color:var(--ink-soft);margin-bottom:20px;}
.add-member-btn:hover{border-color:var(--plum);color:var(--plum);background:var(--plum-pale);}
.split-table{width:100%;border-collapse:collapse;margin-bottom:20px;}
.split-table tr{border-bottom:1px solid var(--border);}
.split-table tr:last-child{border-bottom:none;font-weight:700;}
.split-table td{padding:10px 0;font-size:0.85rem;color:var(--ink-mid);}
.split-table td:last-child{text-align:right;font-weight:600;color:var(--ink);}
.split-table .tr-total td{color:var(--rose);font-size:0.95rem;padding-top:14px;border-top:1.5px solid var(--border);}
.g-actions{display:flex;gap:10px;}
.g-actions button{flex:1;padding:12px;border-radius:var(--r-sm);font-size:0.88rem;font-weight:600;border:none;}
.g-btn-main{background:var(--rose);color:#fff;box-shadow:0 4px 14px rgba(232,99,122,0.25);}
.g-btn-main:hover{background:#d45570;}
.g-btn-alt{background:var(--sage-pale);color:var(--sage);border:1.5px solid #b4d8c0 !important;}
.g-btn-alt:hover{background:#d4edd8;}
.how-step{display:flex;gap:12px;align-items:flex-start;margin-bottom:16px;}
.how-step:last-child{margin-bottom:0;}
.how-num{width:28px;height:28px;background:var(--rose-pale);border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:0.78rem;font-weight:700;color:var(--rose);flex-shrink:0;}
.how-label{font-weight:600;font-size:0.87rem;}
.how-sub{font-size:0.78rem;color:var(--ink-soft);}

/* ─── MODAL ─── */
.modal-overlay{position:fixed;inset:0;background:rgba(30,26,26,0.5);z-index:300;display:none;align-items:center;justify-content:center;padding:20px;}
.modal-overlay.open{display:flex;}
.modal-box{background:var(--white);border-radius:var(--r-lg);padding:48px 40px;max-width:440px;width:100%;text-align:center;position:relative;box-shadow:0 24px 64px rgba(30,26,26,0.18);}
.modal-close{position:absolute;top:16px;right:16px;width:32px;height:32px;border-radius:50%;border:1.5px solid var(--border);background:var(--canvas);color:var(--ink-soft);display:flex;align-items:center;justify-content:center;font-size:0.9rem;}
.modal-close:hover{color:var(--rose);border-color:var(--rose);}
.modal-icon{width:72px;height:72px;border-radius:50%;margin:0 auto 20px;display:flex;align-items:center;justify-content:center;font-size:2rem;}
.modal-icon.green{background:var(--sage-pale);}
.modal-icon.rose{background:var(--rose-pale);}
.modal-box h3{font-family:'Playfair Display',serif;font-size:1.5rem;margin-bottom:10px;}
.modal-box p{font-size:0.88rem;color:var(--ink-soft);margin-bottom:28px;line-height:1.6;}

/* ─── TOAST ─── */
.toast{position:fixed;bottom:28px;left:50%;transform:translateX(-50%) translateY(80px);background:var(--ink);color:#fff;padding:12px 22px;border-radius:40px;font-size:0.86rem;font-weight:500;z-index:500;opacity:0;transition:transform 0.3s,opacity 0.3s;box-shadow:0 8px 24px rgba(30,26,26,0.25);white-space:nowrap;}
.toast.show{transform:translateX(-50%) translateY(0);opacity:1;}
.toast.success{background:var(--sage);}
.toast.error{background:#c0392b;}

/* ─── RESPONSIVE ─── */
@media(max-width:900px){
  .login-split{grid-template-columns:1fr;}
  .login-visual{display:none;}
  .login-form-panel{padding:48px 32px;}
  .hero{grid-template-columns:1fr;}
  .hero-photos{display:none;}
  .hero-content{padding:48px 32px;}
  .hero h1{font-size:2.2rem;}
  .section{padding:40px 24px;}
  .tracking-wrap,.group-wrap{grid-template-columns:1fr;}
  nav{padding:0 20px;gap:16px;}
  .cart-drawer{width:100%;}
}
@media(max-width:600px){
  .hero h1{font-size:1.8rem;}
  .quiz-options{grid-template-columns:1fr;}
  .recipe-grid{grid-template-columns:1fr;}
  .menu-grid{grid-template-columns:repeat(auto-fill,minmax(200px,1fr));}
}
</style>
</head>
<body>

<!-- LOGIN PAGE -->
<div id="loginPage" class="page active">
  <div class="login-split">
    <div class="login-visual">
      <div class="lv-grid">
        <img class="lv-img hp-tall" src="https://images.unsplash.com/photo-1546069901-ba9599a7e63c?w=600&h=900&fit=crop&q=85" alt="food bowl">
        <img class="lv-img" src="https://images.unsplash.com/photo-1565299624946-b28f40a0ae38?w=600&h=400&fit=crop&q=85" alt="pizza">
        <img class="lv-img" src="https://images.unsplash.com/photo-1551782450-17144efb9c50?w=600&h=400&fit=crop&q=85" alt="burger">
      </div>
      <div class="lv-overlay"></div>
      <div class="lv-badge">Trusted by 50,000+ food lovers</div>
      <div class="lv-brand">
        <h1>Discover.<br>Order.<br>Enjoy.</h1>
        <p>Curated food experiences, delivered to your door.</p>
      </div>
    </div>
    <div class="login-form-panel">
      <div class="form-logo">FeastTogether</div>
      <div class="login-tabs">
        <button class="ltab active" onclick="switchLoginTab('login')">Sign In</button>
        <button class="ltab" onclick="switchLoginTab('signup')">Create Account</button>
      </div>
      <!-- Login -->
      <div class="lform-section active" id="lsLogin">
        <div class="lform-title">Welcome back</div>
        <div class="lform-sub">Sign in to your account to continue ordering</div>
        <div class="fgroup"><label>Email Address</label><input type="email" id="loginEmail" placeholder="you@example.com"></div>
        <div class="fgroup"><label>Password</label><input type="password" id="loginPassword" placeholder="Enter your password"></div>
        <button class="btn-primary" onclick="doLogin()">Sign In</button>
        <div class="form-alt" style="margin-top:14px;">New to FeastTogether? <a onclick="switchLoginTab('signup')">Create a free account</a></div>
      </div>
      <!-- Signup -->
      <div class="lform-section" id="lsSignup">
        <div class="lform-title">Join FeastTogether</div>
        <div class="lform-sub">Create your account — it's completely free</div>
        <div class="fgroup"><label>Full Name</label><input type="text" id="signupName" placeholder="Your full name"></div>
        <div class="fgroup"><label>Email Address</label><input type="email" id="signupEmail" placeholder="you@example.com"></div>
        <div class="fgroup"><label>Password</label><input type="password" id="signupPassword" placeholder="Minimum 6 characters"></div>
        <button class="btn-primary" onclick="doSignup()">Create Account</button>
        <div class="form-alt" style="margin-top:14px;">Already have an account? <a onclick="switchLoginTab('login')">Sign in</a></div>
      </div>
      <div class="login-stats">
        <div><div class="lstat-num">200+</div><div class="lstat-lbl">Menu Items</div></div>
        <div><div class="lstat-num">30 min</div><div class="lstat-lbl">Avg Delivery</div></div>
        <div><div class="lstat-num">4.9★</div><div class="lstat-lbl">Avg Rating</div></div>
      </div>
    </div>
  </div>
</div>

<!-- MAIN APP -->
<div id="mainApp" class="page">
  <nav>
    <div class="nav-logo">FeastTogether</div>
    <div class="nav-links">
      <button class="nav-link active" onclick="showSection('menu')">Menu</button>
      <button class="nav-link" onclick="showSection('tracking')">Track Order</button>
      <button class="nav-link" onclick="showSection('quiz')">Taste Quiz</button>
      <button class="nav-link" onclick="showSection('group')">Group Order</button>
    </div>
    <div class="nav-right">
      <div class="nav-chip"><div class="nav-av" id="navAv">F</div><span id="navUser">Foodie</span></div>
      <button class="nav-cart" onclick="toggleCart()">Cart <span class="cart-badge" id="cartBadge">0</span></button>
    </div>
  </nav>

  <!-- MENU -->
  <div id="secMenu">
    <div class="hero">
      <div class="hero-content">
        <div class="hero-eyebrow">Intuitive Online Food Ordering</div>
        <h1>What would you like to <em>eat today?</em></h1>
        <p class="hero-sub">Explore freshly curated menus — from artisan pastries to hearty mains — and get it delivered fast.</p>
        <div class="hero-search">
          <input type="text" id="searchInput" placeholder="Search dishes, cuisines, ingredients…" oninput="filterMenu()">
          <button onclick="filterMenu()">Search</button>
        </div>
        <div class="hero-stats">
          <div><div class="hstat-num">30+</div><div class="hstat-lbl">Menu items</div></div>
          <div><div class="hstat-num">6</div><div class="hstat-lbl">Categories</div></div>
          <div><div class="hstat-num">Free</div><div class="hstat-lbl">On ₹299+</div></div>
        </div>
      </div>
      <div class="hero-photos">
        <div class="hero-photos-grid">
          <img class="hp-tall" src="https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?w=500&h=700&fit=crop&q=85" alt="butter chicken">
          <img src="https://images.unsplash.com/photo-1565958011703-44f9829ba187?w=500&h=350&fit=crop&q=85" alt="cake">
          <img src="https://images.unsplash.com/photo-1495474472287-4d71bcdd2085?w=500&h=350&fit=crop&q=85" alt="coffee">
        </div>
      </div>
    </div>
    <div class="section">
      <div class="profile-bar" id="profileBar">
        <div class="pb-av" id="pbAv">F</div>
        <div><div class="pb-label">Your Taste Profile</div><div class="pb-name" id="pbName">Personalised picks enabled</div><div class="pb-tags" id="pbTags"></div></div>
        <button class="sug-retake" onclick="showSection('quiz')">Edit Profile</button>
      </div>
      <div id="sugSection" style="display:none;">
        <div class="sug-banner">
          <div class="sug-icon">🎯</div>
          <div class="sug-text"><h4>Personalised Picks for You</h4><p>Based on your taste quiz — these dishes match your profile perfectly.</p></div>
          <button class="sug-retake" onclick="showSection('quiz')">Edit Profile</button>
        </div>
        <div class="menu-grid" id="sugGrid" style="margin-bottom:40px;"></div>
        <div class="section-eyebrow" style="margin-bottom:6px;">Full Menu</div>
        <div class="section-title" style="margin-bottom:0;">All <span>Items</span></div>
      </div>
      <div class="section-eyebrow" id="menuEyebrow" style="margin-bottom:6px;margin-top:20px;">Browse</div>
      <div class="section-title" id="menuTitle">Our <span>Menu</span></div>
      <div class="cat-strip">
        <button class="cat-pill active" data-cat="all" onclick="filterByCategory(this,'all')">🍽️ All Items</button>
        <button class="cat-pill" data-cat="pastries" onclick="filterByCategory(this,'pastries')">🥐 Pastries</button>
        <button class="cat-pill" data-cat="beverages" onclick="filterByCategory(this,'beverages')">☕ Beverages</button>
        <button class="cat-pill" data-cat="mains" onclick="filterByCategory(this,'mains')">🍛 Main Course</button>
        <button class="cat-pill" data-cat="snacks" onclick="filterByCategory(this,'snacks')">🍟 Snacks</button>
        <button class="cat-pill" data-cat="desserts" onclick="filterByCategory(this,'desserts')">🍰 Desserts</button>
        <button class="cat-pill" data-cat="healthy" onclick="filterByCategory(this,'healthy')">🥗 Healthy</button>
      </div>
      <div class="menu-grid" id="menuGrid"></div>
    </div>
  </div>

  <!-- TRACKING -->
  <div id="secTracking" style="display:none;">
    <div class="section">
      <div class="section-eyebrow">Live Status</div>
      <div class="section-title" style="margin-bottom:28px;">Track Your <span>Order</span></div>
      <div class="tracking-wrap">
        <div class="t-card">
          <h3>Order Status</h3>
          <p class="sub">Enter your order ID to see real-time updates</p>
          <div class="search-bar">
            <input type="text" id="trackInput" placeholder="e.g. FT-2024-001" value="FT-2024-001">
            <button onclick="doTrack()">Track</button>
          </div>
          <div id="trackResult" style="display:none;">
            <div class="oscard">
              <div class="oscard-row"><span>Order ID</span><span style="font-weight:700;">#FT-2024-001</span></div>
              <div class="oscard-row"><span>Placed</span><span>Today, 12:30 PM</span></div>
              <div class="oscard-row"><span>Estimated Delivery</span><span>1:10 – 1:20 PM</span></div>
              <div class="oscard-row total"><span>Total Paid</span><span style="color:var(--rose);">₹ 487</span></div>
            </div>
            <div class="track-steps">
              <div class="track-step done"><div class="ts-dot">✓</div><div class="ts-info"><h4>Order Placed</h4><p>Received at 12:30 PM</p></div></div>
              <div class="track-step done"><div class="ts-dot">✓</div><div class="ts-info"><h4>Order Confirmed</h4><p>Restaurant accepted your order</p></div></div>
              <div class="track-step active"><div class="ts-dot">🍳</div><div class="ts-info"><h4>Preparing Your Meal</h4><p>Chef is working on your order right now</p></div></div>
              <div class="track-step"><div class="ts-dot"></div><div class="ts-info"><h4>Out for Delivery</h4><p>Rider will pick up shortly</p></div></div>
              <div class="track-step"><div class="ts-dot"></div><div class="ts-info"><h4>Delivered</h4><p>Enjoy your meal!</p></div></div>
            </div>
          </div>
        </div>
        <div style="display:flex;flex-direction:column;gap:20px;">
          <div class="t-card">
            <h3>Delivery Partner</h3>
            <p class="sub">Your assigned delivery expert</p>
            <div id="riderInfo" style="display:none;">
              <img class="rider-img" src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=600&h=280&fit=crop&q=80" alt="delivery partner">
              <div class="rider-row">
                <div><div class="rider-name">Ravi Kumar</div><div class="rider-rating">⭐ 4.9 • 1,240 deliveries • 3 km away</div></div>
                <button class="rider-call" onclick="showToast('Calling Ravi Kumar…')">📞 Call</button>
              </div>
            </div>
            <div id="riderWait" style="text-align:center;padding:20px;color:var(--ink-soft);font-size:0.85rem;">Track your order first to see rider details.</div>
          </div>
          <div class="t-card" id="mapCard" style="display:none;">
            <h3>Live Map</h3>
            <img class="map-img" src="https://images.unsplash.com/photo-1569336415962-a4bd9f69c8bf?w=600&h=220&fit=crop&q=80" alt="map view">
            <div style="font-size:0.82rem;color:var(--ink-soft);">Rider location updates every 30 seconds</div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- QUIZ -->
  <div id="secQuiz" style="display:none;">
    <div class="section">
      <div class="section-eyebrow">Discover Your Palate</div>
      <div class="section-title" style="margin-bottom:8px;">Taste Profile <span>Quiz</span></div>
      <p style="color:var(--ink-soft);margin-bottom:36px;max-width:500px;">Answer 5 quick questions and we'll suggest personalised dishes and recipes that match your exact taste preferences.</p>
      <div class="quiz-wrap">
        <div class="q-prog-track"><div class="q-prog-fill" id="qFill" style="width:20%"></div></div>
        <div id="quizBody"></div>
        <div class="quiz-result" id="quizResult"></div>
      </div>
    </div>
  </div>

  <!-- GROUP -->
  <div id="secGroup" style="display:none;">
    <div class="section">
      <div class="section-eyebrow">Social Dining</div>
      <div class="section-title" style="margin-bottom:8px;">Group Order &amp; <span>Bill Split</span></div>
      <p style="color:var(--ink-soft);margin-bottom:36px;max-width:520px;">Order together, split fairly. Invite friends, each person adds their items, and the bill is calculated automatically.</p>
      <div class="group-wrap">
        <div class="g-card">
          <div class="session-hdr"><div class="session-title">Saturday Squad Lunch</div><div class="session-code">FEAST42</div></div>
          <div class="session-meta">4 members active • Session expires in 23 mins</div>
          <div style="font-size:0.78rem;font-weight:600;letter-spacing:0.06em;text-transform:uppercase;color:var(--ink-soft);margin-bottom:10px;">Invite Link</div>
          <div class="invite-row">
            <input type="text" value="feasttogether.app/group/FEAST42" readonly>
            <button onclick="copyInvite()">Copy</button>
          </div>
          <div style="font-size:0.78rem;font-weight:600;letter-spacing:0.06em;text-transform:uppercase;color:var(--ink-soft);margin-bottom:12px;">Members</div>
          <div class="members-list" id="membersList"></div>
          <button class="add-member-btn" onclick="addGroupMember()">+ Add Member</button>
          <div class="g-actions">
            <button class="g-btn-main" onclick="showSection('menu')">Add My Items</button>
            <button class="g-btn-alt" onclick="confirmGroupOrder()">Place Group Order</button>
          </div>
        </div>
        <div style="display:flex;flex-direction:column;gap:20px;">
          <div class="g-card">
            <h3>Bill Split Summary</h3>
            <table class="split-table" id="splitTable"></table>
            <div style="background:var(--sage-pale);border-radius:var(--r-sm);padding:14px 16px;">
              <div style="font-size:0.82rem;font-weight:600;color:var(--sage);">Equal split calculated automatically</div>
              <div style="font-size:0.78rem;color:var(--ink-soft);margin-top:3px;">Each person's share will be charged via their saved payment method.</div>
            </div>
          </div>
          <div class="g-card">
            <h3>How Group Ordering Works</h3>
            <div class="how-step"><div class="how-num">1</div><div><div class="how-label">Share the session link</div><div class="how-sub">Friends join using the code or link</div></div></div>
            <div class="how-step"><div class="how-num">2</div><div><div class="how-label">Everyone adds their items</div><div class="how-sub">Each member browses and adds independently</div></div></div>
            <div class="how-step"><div class="how-num">3</div><div><div class="how-label">Place &amp; split the bill</div><div class="how-sub">One order, individual payments, zero hassle</div></div></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- CART -->
<div class="cart-overlay" id="cartOverlay" onclick="toggleCart()"></div>
<div class="cart-drawer" id="cartDrawer">
  <div class="cart-head">
    <h3>Your Cart</h3>
    <button class="cart-close-btn" onclick="toggleCart()">✕</button>
  </div>
  <div class="cart-body" id="cartBody">
    <div class="cart-empty"><div class="cart-empty-icon">🛒</div><h4>Your cart is empty</h4><p>Browse the menu and add some delicious items!</p></div>
  </div>
  <div class="cart-foot" id="cartFoot" style="display:none;">
    <div class="cart-row"><span>Subtotal</span><span id="ctSub">₹ 0</span></div>
    <div class="cart-row"><span>Delivery fee</span><span>₹ 30</span></div>
    <div class="cart-row"><span>Taxes &amp; charges</span><span id="ctTax">₹ 0</span></div>
    <div class="cart-row total"><span>Total</span><span id="ctTotal">₹ 0</span></div>
    <div class="cart-savings">You're saving ₹25 on this order</div>
    <button class="btn-primary" onclick="placeOrder()">Place Order</button>
    <button class="btn-outline-teal" onclick="showSection('group');toggleCart()">Group Order &amp; Split</button>
  </div>
</div>

<!-- ORDER MODAL -->
<div class="modal-overlay" id="modalOrder">
  <div class="modal-box">
    <button class="modal-close" onclick="closeModal('modalOrder')">✕</button>
    <div class="modal-icon green">✅</div>
    <h3>Order Placed!</h3>
    <p>Your order <strong id="modalOID"></strong> has been placed successfully. Estimated delivery time is <strong>30 – 45 minutes</strong>.</p>
    <button class="btn-primary" onclick="closeModal('modalOrder');showSection('tracking');doTrack();">Track My Order</button>
  </div>
</div>

<!-- GROUP MODAL -->
<div class="modal-overlay" id="modalGroup">
  <div class="modal-box">
    <button class="modal-close" onclick="closeModal('modalGroup')">✕</button>
    <div class="modal-icon rose">👥</div>
    <h3>Group Order Confirmed!</h3>
    <p>All members have been notified. Each person's share has been calculated and payment requests sent. Your food is on its way!</p>
    <button class="btn-primary" onclick="closeModal('modalGroup')">Great, Thanks!</button>
  </div>
</div>

<div class="toast" id="toast"></div>

<script>
// ── STATE ──
let currentUser={name:'Foodie',email:''};
let cart=[];
let tasteProfile=null;
let quizStep=0;
let quizAnswers={};
let filteredItems=[];
let activeCategory='all';

// ── MENU DATA ──
const menuItems=[
  // PASTRIES
  {id:1,name:'Butter Croissant',cat:'pastries',price:85,veg:true,spice:0,tags:['sweet'],emoji:'🥐',bg:'#fef3e2',img:'https://cdn.pixabay.com/photo/2016/01/26/23/35/croissant-1163016_640.jpg',desc:'Golden, flaky French croissant made with premium European butter.'},
  {id:2,name:'Chocolate Muffin',cat:'pastries',price:70,veg:true,spice:0,tags:['sweet','comfort'],emoji:'🧁',bg:'#f3e5d0',img:'https://cdn.pixabay.com/photo/2017/01/11/11/33/cake-1971556_640.jpg',desc:'Rich double-chocolate muffin studded with dark chocolate chips.'},
  {id:3,name:'Cinnamon Roll',cat:'pastries',price:95,veg:true,spice:0,tags:['sweet'],emoji:'🌀',bg:'#fde8d0',img:'https://cdn.pixabay.com/photo/2014/11/05/15/57/pastry-518071_640.jpg',desc:'Soft, pillowy roll swirled with cinnamon sugar and vanilla glaze.',isNew:true},
  {id:4,name:'Blueberry Danish',cat:'pastries',price:110,veg:true,spice:0,tags:['sweet','healthy'],emoji:'🫐',bg:'#e8eaf6',img:'https://cdn.pixabay.com/photo/2015/09/18/16/59/muffin-946479_640.jpg',desc:'Layered pastry topped with fresh blueberry compote and cream cheese.'},
  {id:5,name:'Almond Croissant',cat:'pastries',price:120,veg:true,spice:0,tags:['sweet'],emoji:'🥐',bg:'#fff8e1',img:'https://cdn.pixabay.com/photo/2016/01/26/23/35/croissant-1163016_640.jpg',desc:'Classic croissant filled with house-made almond frangipane cream.'},
  // BEVERAGES
  {id:6,name:'Caramel Latte',cat:'beverages',price:150,veg:true,spice:0,tags:['sweet','comfort'],emoji:'☕',bg:'#efebe9',img:'https://cdn.pixabay.com/photo/2016/11/29/12/54/coffee-1869699_640.jpg',desc:'Double espresso with house caramel syrup and velvety steamed milk.'},
  {id:7,name:'Mango Lassi',cat:'beverages',price:120,veg:true,spice:0,tags:['sweet','healthy'],emoji:'🥭',bg:'#fff3e0',img:'https://cdn.pixabay.com/photo/2017/01/20/19/05/smoothie-1995056_640.jpg',desc:'Creamy yogurt blended with ripe Alphonso mangoes and cardamom.'},
  {id:8,name:'Masala Chai',cat:'beverages',price:60,veg:true,spice:2,tags:['spicy','comfort'],emoji:'🍵',bg:'#fce4ec',img:'https://cdn.pixabay.com/photo/2016/11/29/12/54/coffee-1869699_640.jpg',desc:'Aromatic spiced tea with ginger, cardamom and frothy whole milk.'},
  {id:9,name:'Cold Brew Coffee',cat:'beverages',price:180,veg:true,spice:0,tags:[],emoji:'🧋',bg:'#e8f5e9',img:'https://cdn.pixabay.com/photo/2016/11/29/12/54/coffee-1869699_640.jpg',desc:'12-hour cold-steeped single-origin arabica, served over ice.',isNew:true},
  {id:10,name:'Watermelon Cooler',cat:'beverages',price:90,veg:true,spice:0,tags:['healthy','sweet'],emoji:'🍉',bg:'#fce4ec',img:'https://cdn.pixabay.com/photo/2017/05/07/08/56/watermelon-2291908_640.jpg',desc:'Freshly pressed watermelon with mint leaves and a squeeze of lime.'},
  // MAINS
  {id:11,name:'Butter Chicken',cat:'mains',price:280,veg:false,spice:2,tags:['spicy','comfort'],emoji:'🍛',bg:'#fff3e0',img:'https://cdn.pixabay.com/photo/2019/11/04/22/14/curry-4602399_640.jpg',desc:'Tender chicken simmered in a rich, velvety tomato-butter masala.'},
  {id:12,name:'Pasta Arrabiata',cat:'mains',price:240,veg:true,spice:3,tags:['spicy'],emoji:'🍝',bg:'#fce4ec',img:'https://cdn.pixabay.com/photo/2018/07/18/19/12/pasta-3547078_640.jpg',desc:'Penne in bold spicy tomato sauce with roasted garlic and basil.'},
  {id:13,name:'Vegetable Biryani',cat:'mains',price:220,veg:true,spice:2,tags:['spicy','comfort'],emoji:'🍚',bg:'#fffde7',img:'https://cdn.pixabay.com/photo/2017/06/29/20/09/india-2456038_640.jpg',desc:'Fragrant basmati rice layered with seasonal vegetables and whole spices.'},
  {id:14,name:'Grilled Salmon',cat:'mains',price:380,veg:false,spice:1,tags:['healthy'],emoji:'🐟',bg:'#e0f2f1',img:'https://cdn.pixabay.com/photo/2016/03/05/19/02/salmon-1238248_640.jpg',desc:'Atlantic salmon fillet with lemon-herb butter and grilled asparagus.',isNew:true},
  {id:15,name:'Paneer Tikka Masala',cat:'mains',price:260,veg:true,spice:2,tags:['spicy','comfort'],emoji:'🧆',bg:'#fff8e1',img:'https://cdn.pixabay.com/photo/2019/11/04/22/14/curry-4602399_640.jpg',desc:'Smoky tandoor-roasted paneer in vibrant tikka masala gravy.'},
  // SNACKS
  {id:16,name:'Loaded Nachos',cat:'snacks',price:160,veg:true,spice:3,tags:['spicy','comfort'],emoji:'🌮',bg:'#fff9c4',img:'https://cdn.pixabay.com/photo/2016/11/23/18/27/nachos-1854255_640.jpg',desc:'Crispy tortilla chips with melted cheese, jalapeños and salsa.'},
  {id:17,name:'Crispy Chicken Wings',cat:'snacks',price:220,veg:false,spice:3,tags:['spicy','comfort'],emoji:'🍗',bg:'#fbe9e7',img:'https://cdn.pixabay.com/photo/2014/10/19/20/59/hamburger-494706_640.jpg',desc:'Double-fried wings tossed in smoky buffalo sauce with ranch dip.'},
  {id:18,name:'Vegetable Spring Rolls',cat:'snacks',price:130,veg:true,spice:1,tags:['comfort'],emoji:'🥢',bg:'#f1f8e9',img:'https://cdn.pixabay.com/photo/2015/12/09/17/11/vegetables-1085063_640.jpg',desc:'Crispy rolls stuffed with stir-fried vegetables and glass noodles.'},
  {id:19,name:'French Fries',cat:'snacks',price:100,veg:true,spice:0,tags:['comfort'],emoji:'🍟',bg:'#fffde7',img:'https://cdn.pixabay.com/photo/2016/11/20/10/17/fries-1842961_640.jpg',desc:'Hand-cut fries double-fried to perfection with seasoned salt.'},
  {id:20,name:'Bruschetta Platter',cat:'snacks',price:140,veg:true,spice:0,tags:['healthy'],emoji:'🍅',bg:'#fce4ec',img:'https://cdn.pixabay.com/photo/2017/09/16/19/21/salad-2756467_640.jpg',desc:'Toasted sourdough with vine tomatoes, basil and aged balsamic.'},
  // DESSERTS
  {id:21,name:'Belgian Waffle',cat:'desserts',price:170,veg:true,spice:0,tags:['sweet','comfort'],emoji:'🧇',bg:'#fff3e0',img:'https://cdn.pixabay.com/photo/2017/05/19/17/48/food-2326278_640.jpg',desc:'Light crispy waffle with Nutella, fresh strawberries and cream.'},
  {id:22,name:'Classic Tiramisu',cat:'desserts',price:200,veg:true,spice:0,tags:['sweet'],emoji:'🍮',bg:'#efebe9',img:'https://cdn.pixabay.com/photo/2017/03/10/08/03/tiramisu-2132129_640.jpg',desc:'Espresso-soaked ladyfingers layered with mascarpone and cocoa.'},
  {id:23,name:'Gulab Jamun',cat:'desserts',price:90,veg:true,spice:0,tags:['sweet','comfort'],emoji:'🟤',bg:'#fce4ec',img:'https://cdn.pixabay.com/photo/2016/03/26/13/09/dessert-1280459_640.jpg',desc:'Milk-solid dumplings in rose-saffron syrup, served warm.'},
  {id:24,name:'Mango Sorbet',cat:'desserts',price:120,veg:true,spice:0,tags:['sweet','healthy'],emoji:'🍧',bg:'#fff9c4',img:'https://cdn.pixabay.com/photo/2014/08/26/21/25/ice-cream-428092_640.jpg',desc:'Dairy-free Alphonso mango sorbet with fresh mint.',isNew:true},
  {id:25,name:'Chocolate Lava Cake',cat:'desserts',price:180,veg:true,spice:0,tags:['sweet','comfort'],emoji:'🎂',bg:'#efebe9',img:'https://cdn.pixabay.com/photo/2016/11/22/23/52/cake-1850011_640.jpg',desc:'Warm chocolate cake with a molten centre and vanilla ice cream.'},
  // HEALTHY
  {id:26,name:'Açaí Power Bowl',cat:'healthy',price:220,veg:true,spice:0,tags:['healthy','sweet'],emoji:'🍓',bg:'#fce4ec',img:'https://cdn.pixabay.com/photo/2017/05/11/19/44/fresh-fruits-2305192_640.jpg',desc:'Blended açaí with granola, fresh berries, banana and honey.'},
  {id:27,name:'Greek Salad',cat:'healthy',price:180,veg:true,spice:0,tags:['healthy'],emoji:'🥗',bg:'#e8f5e9',img:'https://cdn.pixabay.com/photo/2017/12/09/08/18/pizza-3007395_640.jpg',desc:'Cucumber, tomato, Kalamata olives, feta and cold-pressed olive oil.'},
  {id:28,name:'Quinoa Buddha Bowl',cat:'healthy',price:260,veg:true,spice:1,tags:['healthy'],emoji:'🥣',bg:'#f1f8e9',img:'https://cdn.pixabay.com/photo/2017/01/16/17/45/glass-1984412_640.jpg',desc:'Quinoa base with roasted vegetables, avocado and tahini dressing.',isNew:true},
  {id:29,name:'Oat & Banana Smoothie',cat:'healthy',price:130,veg:true,spice:0,tags:['healthy','sweet'],emoji:'🥤',bg:'#fff8e1',img:'https://cdn.pixabay.com/photo/2017/01/20/19/05/smoothie-1995056_640.jpg',desc:'Rolled oats, ripe banana, almond milk and chia seeds, blended smooth.'},
  {id:30,name:'Sprouts Chaat',cat:'healthy',price:100,veg:true,spice:2,tags:['healthy','spicy'],emoji:'🌱',bg:'#e8f5e9',img:'https://cdn.pixabay.com/photo/2015/12/09/17/11/vegetables-1085063_640.jpg',desc:'Mixed protein-rich sprouts with tamarind chutney and coriander.'},
];

// ── QUIZ ──
const quizQs=[
  {q:'How spicy do you like your food?',key:'spice',opts:[{icon:'🌿',label:'Mild',sub:'No heat at all'},{icon:'🌱',label:'Light',sub:'Subtle warmth'},{icon:'🌶️',label:'Medium',sub:'A pleasant kick'},{icon:'🔥',label:'Fiery',sub:'The hotter the better'}]},
  {q:'Which cuisine excites you most?',key:'cuisine',opts:[{icon:'🍛',label:'Indian',sub:'Curries, biryanis & more'},{icon:'🍝',label:'Italian',sub:'Pasta, pizza & risotto'},{icon:'🍔',label:'American',sub:'Burgers, wings & BBQ'},{icon:'🥢',label:'Asian',sub:'Sushi, ramen & stir-fry'}]},
  {q:'How strong is your sweet tooth?',key:'sweet',opts:[{icon:'🧂',label:'Not sweet',sub:'Savoury all the way'},{icon:'🫐',label:'A little',sub:'Only occasionally'},{icon:'🍮',label:'Moderate',sub:'A dessert after dinner'},{icon:'🍰',label:'Very sweet',sub:'Dessert is non-negotiable!'}]},
  {q:'What is your dietary preference?',key:'diet',opts:[{icon:'🥦',label:'Vegetarian',sub:'Plant-based ingredients'},{icon:'🍗',label:'Non-Vegetarian',sub:'Meat, fish & poultry'},{icon:'🌱',label:'Vegan',sub:'100% plant-based'},{icon:'🤷',label:'No restriction',sub:'I eat everything'}]},
  {q:'What best describes your food mood?',key:'mood',opts:[{icon:'🛋️',label:'Comfort food',sub:'Cosy, filling & familiar'},{icon:'💪',label:'Healthy & light',sub:'Nutritious and clean'},{icon:'🎭',label:'Adventurous',sub:'Unique and unexpected'},{icon:'⚡',label:'Quick & easy',sub:'Fast and satisfying'}]},
];

// ── RECIPE DB ──
const recipeDB={
  'mild-indian':[{n:'Creamy Butter Paneer',d:'Soft paneer in mild buttery tomato gravy. Ready in 30 min.',s:'Blend sautéed onion & tomato, add paneer + cream, simmer 15 min.',t:['Vegetarian','30 mins'],i:'https://images.unsplash.com/photo-1565557623262-b51c2513a641?w=400&h=240&fit=crop&q=75'},{n:'Coconut Dal Soup',d:'Soothing lentil soup with coconut milk, cumin and curry leaves.',s:'Cook masoor dal, add coconut milk, temper with mustard & curry leaves.',t:['Vegan','25 mins'],i:'https://images.unsplash.com/photo-1455619452474-d2be8b1e70cd?w=400&h=240&fit=crop&q=75'}],
  'medium-indian':[{n:'Chicken Tikka Masala',d:'Marinated chicken in smoky tikka masala — a restaurant classic.',s:'Marinate, grill, prepare masala base, combine & simmer 20 min.',t:['Non-Veg','45 mins'],i:'https://images.unsplash.com/photo-1603894584373-5ac82b2ae398?w=400&h=240&fit=crop&q=75'},{n:'Aloo Gobi Masala',d:'Spiced potato & cauliflower dry curry with garam masala.',s:'Sauté spices, add par-boiled veg, cook on low flame until dry.',t:['Vegetarian','35 mins'],i:'https://images.unsplash.com/photo-1585937421612-70a008356fbe?w=400&h=240&fit=crop&q=75'}],
  'hot-indian':[{n:'Fiery Chicken Vindaloo',d:'Goan-style super-spicy curry — bold, tangy and unforgettable.',s:'Marinate in vinegar-chili paste overnight, cook with tomatoes.',t:['Non-Veg','60 mins'],i:'https://images.unsplash.com/photo-1574653853027-5382a3d23a15?w=400&h=240&fit=crop&q=75'},{n:'Chettinad Pepper Curry',d:'South Indian bold curry with black pepper and aromatic whole spices.',s:'Grind fresh spices, sauté aromatics, slow-cook 40 minutes.',t:['Non-Veg','50 mins'],i:'https://images.unsplash.com/photo-1546833999-b9f581a1996d?w=400&h=240&fit=crop&q=75'}],
  'mild-italian':[{n:'Classic Pesto Pasta',d:'Fresh basil pesto tossed through al dente penne with parmesan.',s:'Blend basil + pine nuts + parmesan + olive oil, mix with pasta.',t:['Vegetarian','20 mins'],i:'https://images.unsplash.com/photo-1555949258-eb67b1ef0ceb?w=400&h=240&fit=crop&q=75'},{n:'Margherita Pizza',d:'Rustic pizza with tomato sauce, fresh mozzarella and basil.',s:'Spread sauce, top with cheese, bake 10 minutes at 220°C.',t:['Vegetarian','20 mins'],i:'https://images.unsplash.com/photo-1574071318508-1cdbab80d002?w=400&h=240&fit=crop&q=75'}],
  'medium-american':[{n:'Smoky BBQ Burger',d:'Juicy beef patty with smoky BBQ sauce, slaw and pickles.',s:'Season patty, grill 4 min each side, layer sauce + slaw.',t:['Non-Veg','25 mins'],i:'https://images.unsplash.com/photo-1568901346375-23c9450c58cd?w=400&h=240&fit=crop&q=75'},{n:'Loaded Mac & Cheese',d:'Extra-creamy baked mac with three cheeses and breadcrumb crust.',s:'Make roux, add three cheeses, mix pasta, bake 20 min at 190°C.',t:['Vegetarian','35 mins'],i:'https://images.unsplash.com/photo-1543339308-43e59d6b73a6?w=400&h=240&fit=crop&q=75'}],
  'mild-asian':[{n:'Pad Thai (Mild)',d:'Rice noodles with egg, tofu, peanuts and lime — not spicy.',s:'Soak noodles, stir-fry with egg + tofu, toss in pad thai sauce.',t:['Vegetarian','25 mins'],i:'https://images.unsplash.com/photo-1559314809-0d155014e29e?w=400&h=240&fit=crop&q=75'},{n:'Miso Soup & Onigiri',d:'Warming miso soup with silken tofu and triangle rice balls.',s:'Dissolve miso in dashi, add tofu + wakame; shape rice balls.',t:['Vegan','20 mins'],i:'https://images.unsplash.com/photo-1547592180-85f173990554?w=400&h=240&fit=crop&q=75'}],
  comfort:[{n:'Classic Khichdi',d:'Ultimate comfort — soft rice & lentils with ghee and cumin.',s:'Pressure cook rice + dal with turmeric, temper with ghee.',t:['Vegetarian','25 mins'],i:'https://images.unsplash.com/photo-1567337710282-00832b415979?w=400&h=240&fit=crop&q=75'}],
  healthy:[{n:'Rainbow Buddha Bowl',d:'Quinoa topped with 7 colourful veggies, avocado and tahini.',s:'Cook quinoa, roast veg at 200°C, arrange in bowl, drizzle tahini.',t:['Vegan','30 mins'],i:'https://images.unsplash.com/photo-1512621776951-a57141f2eefd?w=400&h=240&fit=crop&q=75'}],
  sweet:[{n:'Mango Shrikhand',d:'Silky hung curd with Alphonso mango, cardamom and saffron.',s:'Strain yogurt 6 hrs, fold in mango pulp, chill 2 hrs.',t:['Vegetarian','15 mins+chill'],i:'https://images.unsplash.com/photo-1590301157890-4810ed352733?w=400&h=240&fit=crop&q=75'}],
};

function getRecipes(p){
  const spMap={Fiery:'hot',Medium:'medium',Light:'mild',Mild:'mild'};
  const sp=spMap[p.spice]||'mild';
  const cu=(p.cuisine||'Indian').toLowerCase();
  let out=[];
  const key=sp+'-'+cu;
  if(recipeDB[key]) out.push(...recipeDB[key]);
  if(out.length<2&&recipeDB['mild-'+cu]) out.push(...recipeDB['mild-'+cu]);
  if((p.sweet==='Very sweet'||p.sweet==='Moderate')&&recipeDB.sweet) out.push(...recipeDB.sweet);
  if(p.mood==='Comfort food'&&recipeDB.comfort) out.push(...recipeDB.comfort);
  if(p.mood==='Healthy & light'&&recipeDB.healthy) out.push(...recipeDB.healthy);
  if(!out.length) out=recipeDB['mild-indian'];
  const seen=new Set(); return out.filter(r=>{if(seen.has(r.n))return false;seen.add(r.n);return true;}).slice(0,4);
}

// ── GROUP DATA ──
let groupMembers=[
  {name:'You',av:'👤',avc:'',items:['Butter Chicken','Mango Lassi'],total:430},
  {name:'Priya',av:'👩',avc:'plum',items:['Greek Salad','Cold Brew Coffee'],total:360},
  {name:'Rahul',av:'👨',avc:'sage',items:['Chicken Wings','French Fries','Caramel Latte'],total:470},
  {name:'Ananya',av:'👩🦰',avc:'peach',items:['Açaí Power Bowl','Blueberry Danish'],total:330},
];

// ── AUTH ──
function switchLoginTab(t){
  document.querySelectorAll('.ltab').forEach((b,i)=>b.classList.toggle('active',(i===0&&t==='login')||(i===1&&t==='signup')));
  document.getElementById('lsLogin').classList.toggle('active',t==='login');
  document.getElementById('lsSignup').classList.toggle('active',t==='signup');
}
function doLogin(){
  const email=document.getElementById('loginEmail').value.trim();
  const pass=document.getElementById('loginPassword').value;
  if(!email||!email.includes('@')){showToast('Enter a valid email address','error');return;}
  if(!pass||pass.length<6){showToast('Password must be at least 6 characters','error');return;}
  const name=email.split('@')[0].replace(/[^a-zA-Z]/g,' ').trim().replace(/\b\w/g,c=>c.toUpperCase());
  launchApp(name,email);
}
function doSignup(){
  const name=document.getElementById('signupName').value.trim();
  const email=document.getElementById('signupEmail').value.trim();
  const pass=document.getElementById('signupPassword').value;
  if(!name){showToast('Please enter your name','error');return;}
  if(!email||!email.includes('@')){showToast('Enter a valid email address','error');return;}
  if(!pass||pass.length<6){showToast('Password must be at least 6 characters','error');return;}
  launchApp(name,email);
}
function launchApp(name,email){
  currentUser={name,email};
  document.getElementById('loginPage').classList.remove('active');
  document.getElementById('mainApp').classList.add('active');
  document.getElementById('navUser').textContent=name;
  document.getElementById('navAv').textContent=name.charAt(0).toUpperCase();
  filteredItems=[...menuItems];
  renderMenu();
  renderGroupPanel();
  renderQuizQuestion();
  showToast('Welcome, '+name+'!','success');
}

// ── MENU ──
function renderMenu(items){
  const g=document.getElementById('menuGrid');
  const list=items!==undefined?items:filteredItems;
  if(!list.length){g.innerHTML='<div style="grid-column:1/-1;padding:48px;text-align:center;color:var(--ink-soft);">No items found. Try a different search.</div>';return;}
  g.innerHTML=list.map(menuCardHTML).join('');
}
function menuCardHTML(item){
  const inCart=cart.find(c=>c.id===item.id);
  const qty=inCart?inCart.qty:0;
  return `<div class="menu-card" id="mc-${item.id}">
    <div class="mc-img-wrap" style="background:${item.bg||'#fdf0f2'};">
      <div class="mc-emoji-bg" style="background:${item.bg||'#fdf0f2'};position:absolute;inset:0;display:flex;align-items:center;justify-content:center;font-size:5rem;z-index:0;">${item.emoji||'🍽️'}</div>
      <img class="mc-img" src="${item.img}" alt="${item.name}" loading="lazy" style="position:relative;z-index:1;" onerror="this.style.display='none'">
      <span class="mc-badge ${item.veg?'badge-veg':'badge-nonveg'}" style="z-index:2;position:absolute;">${item.veg?'● Veg':'● Non-Veg'}</span>
      ${item.isNew?'<span class="badge-new" style="z-index:2;position:absolute;">NEW</span>':''}
    </div>
    <div class="mc-body">
      <div class="mc-name">${item.name}</div>
      <div class="mc-desc">${item.desc}</div>
      <div class="mc-footer">
        <div class="mc-price"><sup>₹</sup>${item.price}</div>
        <div id="ma-${item.id}">${qty>0?`<div class="qty-ctrl"><button class="qty-btn" onclick="changeQty(${item.id},-1)">−</button><span class="qty-num">${qty}</span><button class="qty-btn" onclick="changeQty(${item.id},1)">+</button></div>`:`<button class="mc-add" onclick="addToCart(${item.id})">Add</button>`}</div>
      </div>
    </div>
  </div>`;
}
function filterByCategory(el,cat){document.querySelectorAll('.cat-pill').forEach(p=>p.classList.remove('active'));el.classList.add('active');activeCategory=cat;applyFilters();}
function filterMenu(){applyFilters();}
function applyFilters(){
  const q=(document.getElementById('searchInput')||{value:''}).value.toLowerCase();
  filteredItems=menuItems.filter(item=>(activeCategory==='all'||item.cat===activeCategory)&&(!q||item.name.toLowerCase().includes(q)||item.desc.toLowerCase().includes(q)));
  renderMenu();
}
function addToCart(id){const item=menuItems.find(m=>m.id===id);const ex=cart.find(c=>c.id===id);if(ex)ex.qty++;else cart.push({...item,qty:1});updateCart();refreshAction(id);showToast(item.name+' added to cart');}
function changeQty(id,delta){const i=cart.findIndex(c=>c.id===id);if(i===-1)return;cart[i].qty+=delta;if(cart[i].qty<=0)cart.splice(i,1);updateCart();refreshAction(id);}
function refreshAction(id){const el=document.getElementById('ma-'+id);if(!el)return;const inCart=cart.find(c=>c.id===id);const qty=inCart?inCart.qty:0;el.innerHTML=qty>0?`<div class="qty-ctrl"><button class="qty-btn" onclick="changeQty(${id},-1)">−</button><span class="qty-num">${qty}</span><button class="qty-btn" onclick="changeQty(${id},1)">+</button></div>`:`<button class="mc-add" onclick="addToCart(${id})">Add</button>`;}
function removeFromCart(id){const i=cart.findIndex(c=>c.id===id);if(i>-1)cart.splice(i,1);updateCart();refreshAction(id);}
function updateCart(){
  const totalQty=cart.reduce((s,c)=>s+c.qty,0);
  document.getElementById('cartBadge').textContent=totalQty;
  const sub=cart.reduce((s,c)=>s+c.price*c.qty,0);
  const tax=Math.round(sub*0.05);
  const total=sub+30+tax;
  document.getElementById('ctSub').textContent='₹ '+sub;
  document.getElementById('ctTax').textContent='₹ '+tax;
  document.getElementById('ctTotal').textContent='₹ '+total;
  const body=document.getElementById('cartBody');
  const foot=document.getElementById('cartFoot');
  if(!cart.length){body.innerHTML='<div class="cart-empty"><div class="cart-empty-icon">🛒</div><h4>Your cart is empty</h4><p>Browse the menu and add items.</p></div>';foot.style.display='none';return;}
  foot.style.display='block';
  body.innerHTML=cart.map(c=>`<div class="cart-item"><img class="ci-thumb" src="${c.img}" alt="${c.name}" loading="lazy" onerror="this.style.background='var(--rose-pale)'"><div class="ci-info"><div class="ci-name">${c.name}</div><div class="ci-price">₹${c.price} × ${c.qty} = ₹${c.price*c.qty}</div></div><div class="ci-qty"><button class="qty-btn" onclick="changeQty(${c.id},-1)">−</button><span class="qty-num">${c.qty}</span><button class="qty-btn" onclick="changeQty(${c.id},1)">+</button></div><button class="ci-del" onclick="removeFromCart(${c.id})">✕</button></div>`).join('');
}
function toggleCart(){document.getElementById('cartOverlay').classList.toggle('open');document.getElementById('cartDrawer').classList.toggle('open');}
function placeOrder(){
  if(!cart.length){showToast('Your cart is empty!','error');return;}
  const id='FT-2024-'+Math.floor(Math.random()*900+100);
  document.getElementById('modalOID').textContent='#'+id;
  document.getElementById('trackInput').value=id;
  cart=[];
  menuItems.forEach(m=>{const el=document.getElementById('ma-'+m.id);if(el)el.innerHTML=`<button class="mc-add" onclick="addToCart(${m.id})">Add</button>`;});
  updateCart();toggleCart();
  document.getElementById('modalOrder').classList.add('open');
}

// ── TRACKING ──
function doTrack(){
  const v=document.getElementById('trackInput').value.trim();
  if(!v){showToast('Please enter an order ID','error');return;}
  document.getElementById('trackResult').style.display='block';
  document.getElementById('riderInfo').style.display='block';
  document.getElementById('riderWait').style.display='none';
  document.getElementById('mapCard').style.display='block';
  showToast('Order found — tracking live status');
}

// ── QUIZ ──
function renderQuizQuestion(){
  document.getElementById('qFill').style.width=((quizStep+1)/quizQs.length*100)+'%';
  const q=quizQs[quizStep];
  document.getElementById('quizBody').style.display='block';
  document.getElementById('quizResult').style.display='none';
  document.getElementById('quizBody').innerHTML=`
    <div class="q-step-label">Question ${quizStep+1} of ${quizQs.length}</div>
    <div class="q-title">${q.q}</div>
    <div class="quiz-options">${q.opts.map(o=>`<button class="quiz-opt ${quizAnswers[q.key]===o.label?'selected':''}" onclick="selectOpt(this,'${q.key}','${o.label.replace(/'/g,"\\'")}')"><span class="qopt-icon">${o.icon}</span><div class="qopt-label">${o.label}</div><div class="qopt-sub">${o.sub}</div></button>`).join('')}</div>
    <div class="quiz-nav"><button class="btn-ghost" onclick="quizBack()" ${quizStep===0?'style="visibility:hidden;"':''}>← Back</button><button class="btn-rose" onclick="quizNext()">${quizStep===quizQs.length-1?'See My Results':'Next →'}</button></div>`;
}
function selectOpt(el,key,val){quizAnswers[key]=val;document.querySelectorAll('.quiz-opt').forEach(o=>o.classList.remove('selected'));el.classList.add('selected');}
function quizBack(){if(quizStep>0){quizStep--;renderQuizQuestion();}}
function quizNext(){
  const q=quizQs[quizStep];
  if(!quizAnswers[q.key]){showToast('Please select an option to continue','error');return;}
  if(quizStep<quizQs.length-1){quizStep++;renderQuizQuestion();}
  else showQuizResult();
}
function showQuizResult(){
  tasteProfile={...quizAnswers};
  document.getElementById('qFill').style.width='100%';
  document.getElementById('quizBody').style.display='none';
  const res=document.getElementById('quizResult');
  res.style.display='block';
  const recipes=getRecipes(tasteProfile);
  const badges=[{l:tasteProfile.spice,c:'rose'},{l:tasteProfile.cuisine,c:'plum'},{l:tasteProfile.sweet,c:'peach'},{l:tasteProfile.diet,c:'sage'},{l:tasteProfile.mood,c:'sky'}];
  res.innerHTML=`
    <div class="q-step-label">Your Results</div>
    <div class="q-title" style="font-size:1.35rem;">Your Taste Profile is Ready!</div>
    <p style="color:var(--ink-soft);font-size:0.88rem;margin-bottom:20px;">Based on your answers, here's your personalised taste profile — and recipes we think you'll love.</p>
    <div class="qr-strip">${badges.map(b=>`<span class="qr-badge ${b.c}">${b.l}</span>`).join('')}</div>
    <div style="font-weight:700;font-size:0.85rem;letter-spacing:0.04em;color:var(--ink-mid);margin-bottom:14px;text-transform:uppercase;">Suggested Recipes For You</div>
    <div class="recipe-grid">${recipes.map(r=>`<div class="recipe-card"><img class="recipe-card-img" src="${r.i}" alt="${r.n}" loading="lazy" onerror="this.style.background='var(--rose-pale)'"><div class="recipe-card-body"><div class="rc-title">${r.n}</div><div class="rc-desc">${r.d}</div><div class="rc-step">How to make: ${r.s}</div>${r.t.map((t,i)=>`<span class="recipe-tag${i===1?' green':''}">${t}</span>`).join('')}</div></div>`).join('')}</div>
    <div class="quiz-result-actions"><button class="btn-rose" onclick="applyProfileToMenu()">View Personalised Menu</button><button class="btn-ghost" onclick="quizStep=0;quizAnswers={};renderQuizQuestion()">Retake Quiz</button></div>`;
  updateProfileBar();
}
function applyProfileToMenu(){
  showSection('menu');updateProfileBar();
  const sug=menuItems.filter(item=>{
    if((tasteProfile.diet==='Vegetarian'||tasteProfile.diet==='Vegan')&&!item.veg)return false;
    const sp=tasteProfile.spice;
    const spiceMatch=(sp==='Fiery'&&item.spice>=2)||(sp==='Medium'&&item.spice>=1&&item.spice<=3)||(sp==='Mild'&&item.spice===0)||(sp==='Light'&&item.spice<=1);
    const moodMatch=(tasteProfile.mood==='Healthy & light'&&item.tags.includes('healthy'))||(tasteProfile.mood==='Comfort food'&&item.tags.includes('comfort'))||((tasteProfile.sweet==='Very sweet'||tasteProfile.sweet==='Moderate')&&item.tags.includes('sweet'));
    return spiceMatch||moodMatch;
  }).slice(0,4);
  document.getElementById('sugGrid').innerHTML=sug.map(menuCardHTML).join('');
  document.getElementById('sugSection').style.display='block';
  showToast('Personalised suggestions loaded!','success');
}
function updateProfileBar(){
  if(!tasteProfile)return;
  document.getElementById('profileBar').style.display='flex';
  document.getElementById('pbAv').textContent=currentUser.name.charAt(0).toUpperCase();
  document.getElementById('pbName').textContent=currentUser.name+"'s Profile";
  document.getElementById('pbTags').innerHTML=Object.values(tasteProfile).map(v=>`<span class="pb-tag">${v}</span>`).join('');
}

// ── GROUP ──
function renderGroupPanel(){
  const ml=document.getElementById('membersList');
  ml.innerHTML=groupMembers.map(m=>`<div class="member-row"><div class="member-av ${m.avc}">${m.av}</div><div><div class="member-name">${m.name}</div><div class="member-items">${m.items.join(' • ')}</div></div><div class="member-amt">₹ ${m.total}</div></div>`).join('');
  const total=groupMembers.reduce((s,m)=>s+m.total,0);
  const per=Math.ceil(total/groupMembers.length);
  document.getElementById('splitTable').innerHTML=groupMembers.map(m=>`<tr><td>${m.av} ${m.name}</td><td>₹ ${m.total}</td></tr>`).join('')+`<tr class="tr-total"><td>Per person (equal split)</td><td>₹ ${per}</td></tr>`;
}
function addGroupMember(){
  const pool=[['Karan','👨💼','plum'],['Sneha','👩🎤','sage'],['Dev','🧑💻','peach'],['Riya','👩🎨','']];
  const d=pool[groupMembers.length%pool.length];
  groupMembers.push({name:d[0],av:d[1],avc:d[2],items:['Browsing menu…'],total:0});
  renderGroupPanel();showToast(d[0]+' joined the group!','success');
}
function copyInvite(){showToast('Invite link copied to clipboard!','success');}
function confirmGroupOrder(){document.getElementById('modalGroup').classList.add('open');}

// ── SECTIONS ──
function showSection(sec){
  const map={menu:'secMenu',tracking:'secTracking',quiz:'secQuiz',group:'secGroup'};
  Object.keys(map).forEach(k=>document.getElementById(map[k]).style.display=k===sec?'block':'none');
  document.querySelectorAll('.nav-link').forEach((el,i)=>el.classList.toggle('active',['menu','tracking','quiz','group'][i]===sec));
  if(sec==='quiz'){quizStep=0;quizAnswers={};renderQuizQuestion();}
  if(sec==='group')renderGroupPanel();
}

// ── MODALS & TOAST ──
function closeModal(id){document.getElementById(id).classList.remove('open');}
function showToast(msg,type){
  const t=document.getElementById('toast');t.textContent=msg;t.className='toast'+(type?' '+type:'');
  t.classList.add('show');clearTimeout(t._t);t._t=setTimeout(()=>t.classList.remove('show'),2800);
}

// ── KEYBOARD ──
document.addEventListener('keydown',function(e){
  if(e.key==='Enter'){
    if(document.activeElement.id==='loginPassword')doLogin();
    if(document.activeElement.id==='signupPassword')doSignup();
    if(document.activeElement.id==='trackInput')doTrack();
  }
});
</script>
</body>
</html>
