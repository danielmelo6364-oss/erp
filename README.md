<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Géor — Sistema de Gestão</title>
<style>
*{box-sizing:border-box;margin:0;padding:0;}
:root{
  --rose:#c9748a;--rose-light:#f7e8ec;--rose-dark:#9e4f63;
  --gold:#b8860b;--dark:#1a1a2e;--brown:#4a3728;
  --text:#2d2d2d;--muted:#9e8575;--bg:#fdf5f7;
  --green:#28a745;--blue:#007bff;--orange:#fd7e14;--red:#dc3545;
}
body{font-family:'Segoe UI',sans-serif;background:var(--bg);color:var(--text);min-height:100vh;}

/* ── LOGIN ── */
.login-screen{min-height:100vh;display:flex;align-items:center;justify-content:center;
  background:linear-gradient(135deg,#1a1a2e 0%,#9e4f63 60%,#c9748a 100%);}
.login-box{background:#fff;border-radius:24px;padding:44px 38px;width:100%;max-width:390px;
  box-shadow:0 24px 64px rgba(0,0,0,.25);text-align:center;}
.geor-logo{font-size:38px;font-weight:900;letter-spacing:4px;
  background:linear-gradient(135deg,var(--rose-dark),var(--gold));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;margin-bottom:4px;}
.login-box .sub{font-size:12px;color:var(--muted);margin-bottom:28px;letter-spacing:1px;}
.lf{margin-bottom:16px;text-align:left;}
.lf label{display:block;font-size:11px;font-weight:700;color:var(--rose-dark);
  margin-bottom:5px;text-transform:uppercase;letter-spacing:.5px;}
.lf input{width:100%;padding:11px 14px;border:1.5px solid #e0d0d5;border-radius:10px;
  font-size:14px;transition:border-color .2s;background:#fdf5f7;}
.lf input:focus{outline:none;border-color:var(--rose);}
.btn-login{width:100%;padding:13px;border:none;border-radius:10px;
  background:linear-gradient(135deg,var(--rose),var(--rose-dark));
  color:#fff;font-size:15px;font-weight:700;cursor:pointer;margin-top:8px;
  box-shadow:0 6px 20px rgba(201,116,138,.4);transition:transform .1s;}
.btn-login:hover{transform:translateY(-1px);}
.login-error{color:#dc3545;font-size:12px;margin-top:10px;display:none;}

/* ── CLUBE PÚBLICO ── */
.clube-screen{min-height:100vh;display:none;align-items:center;justify-content:center;
  background:linear-gradient(135deg,#1a1a2e 0%,#9e4f63 60%,#c9748a 100%);padding:20px;}
.clube-box{background:#fff;border-radius:24px;padding:36px 30px;width:100%;max-width:440px;
  box-shadow:0 24px 64px rgba(0,0,0,.3);}
.clube-header{text-align:center;margin-bottom:24px;}
.clube-logo{font-size:32px;font-weight:900;letter-spacing:4px;
  background:linear-gradient(135deg,var(--rose-dark),var(--gold));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;}
.clube-sub{font-size:12px;color:var(--muted);margin-top:4px;letter-spacing:1px;}
.clube-badge{background:linear-gradient(135deg,var(--rose),var(--rose-dark));
  color:#fff;border-radius:12px;padding:8px 18px;font-size:13px;font-weight:700;
  display:inline-block;margin:12px 0;}
.clube-beneficios{background:var(--rose-light);border-radius:12px;padding:14px;
  margin-bottom:20px;font-size:12px;color:var(--rose-dark);}
.clube-beneficios p{margin-bottom:4px;}
.btn-clube{width:100%;padding:13px;border:none;border-radius:10px;
  background:linear-gradient(135deg,var(--rose),var(--rose-dark));
  color:#fff;font-size:15px;font-weight:700;cursor:pointer;
  box-shadow:0 6px 20px rgba(201,116,138,.4);}
.clube-success{display:none;text-align:center;padding:20px;}
.clube-success .icon{font-size:48px;margin-bottom:12px;}
.clube-success h3{color:var(--rose-dark);font-size:18px;margin-bottom:8px;}
.clube-success p{font-size:13px;color:var(--muted);}

/* ── SISTEMA ── */
.sistema{display:none;}
header{background:linear-gradient(135deg,var(--dark),var(--rose-dark));color:#fff;
  padding:14px 28px;display:flex;align-items:center;justify-content:space-between;
  box-shadow:0 3px 16px rgba(0,0,0,.25);flex-wrap:wrap;gap:10px;}
.h-left{display:flex;align-items:center;gap:14px;}
.h-logo{font-size:22px;font-weight:900;letter-spacing:3px;
  background:linear-gradient(135deg,#f7e8ec,#f0c8d4);
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;}
.h-title{font-size:13px;opacity:.8;margin-top:1px;}
.h-right{display:flex;align-items:center;gap:10px;flex-wrap:wrap;}
.user-badge{background:rgba(255,255,255,.15);border-radius:20px;padding:5px 14px;
  font-size:12px;font-weight:600;}
.admin-tag{background:var(--gold);border-radius:12px;padding:2px 8px;
  font-size:10px;font-weight:700;margin-left:5px;}
.btn-logout{background:rgba(255,255,255,.1);border:1px solid rgba(255,255,255,.3);
  color:#fff;padding:5px 12px;border-radius:8px;font-size:12px;cursor:pointer;}
.sync-status{display:flex;align-items:center;gap:6px;font-size:11px;padding:4px 10px;
  border-radius:12px;font-weight:600;}
.sync-ok{background:rgba(40,167,69,.2);color:#90ee90;}
.sync-off{background:rgba(255,255,255,.1);color:rgba(255,255,255,.5);}
.sync-sending{background:rgba(184,134,11,.2);color:#ffd700;}

/* ── TABS ── */
.tabs{display:flex;background:#fff;border-bottom:2px solid var(--rose-light);
  padding:0 16px;box-shadow:0 2px 8px rgba(0,0,0,.05);flex-wrap:wrap;overflow-x:auto;}
.tab{padding:12px 16px;font-size:12px;font-weight:600;cursor:pointer;
  color:var(--muted);border-bottom:3px solid transparent;margin-bottom:-2px;
  transition:all .2s;white-space:nowrap;}
.tab.active{color:var(--rose-dark);border-bottom-color:var(--rose);}
.tab:hover{color:var(--rose);}

/* ── PAINÉIS ── */
.painel{display:none;padding:20px 24px;max-width:1280px;margin:0 auto;}
.painel.active{display:block;}
.card{background:#fff;border-radius:16px;padding:22px;box-shadow:0 4px 20px rgba(0,0,0,.07);margin-bottom:16px;}
.card h2{font-size:14px;font-weight:700;color:var(--brown);margin-bottom:18px;
  padding-bottom:10px;border-bottom:2px solid var(--rose-light);}

/* ── GRID ── */
.grid-form{display:grid;grid-template-columns:380px 1fr;gap:20px;align-items:start;}
@media(max-width:820px){.grid-form{grid-template-columns:1fr;}}
.row2{display:grid;grid-template-columns:1fr 1fr;gap:10px;}
.row3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;}
.row4{display:grid;grid-template-columns:1fr 1fr 1fr 1fr;gap:10px;}

/* ── FIELDS ── */
.field{margin-bottom:12px;}
.field label{display:block;font-size:11px;font-weight:700;color:var(--rose-dark);
  margin-bottom:4px;text-transform:uppercase;letter-spacing:.4px;}
input[type=text],input[type=number],input[type=date],input[type=email],
input[type=tel],input[type=url],select,textarea{
  width:100%;padding:9px 13px;border:1.5px solid #e0d0d5;border-radius:8px;
  font-size:13px;color:var(--text);background:#fdf5f7;transition:border-color .2s;
  font-family:inherit;}
input:focus,select:focus,textarea:focus{outline:none;border-color:var(--rose);background:#fff;}
textarea{resize:vertical;min-height:60px;}

/* ── BOTÕES ── */
.btn{padding:10px 18px;border:none;border-radius:8px;font-size:13px;font-weight:700;
  cursor:pointer;transition:transform .1s,box-shadow .2s;}
.btn-primary{background:linear-gradient(135deg,var(--rose),var(--rose-dark));color:#fff;
  box-shadow:0 4px 14px rgba(201,116,138,.35);width:100%;padding:12px;}
.btn-primary:hover{transform:translateY(-1px);}
.btn-sm{padding:4px 10px;font-size:11px;border-radius:6px;border:none;cursor:pointer;font-weight:600;}
.btn-danger{background:#dc3545;color:#fff;}
.btn-warning{background:#fd7e14;color:#fff;}
.btn-success{background:#28a745;color:#fff;}
.btn-info{background:#007bff;color:#fff;}
.btn-dark{background:var(--dark);color:#f7e8ec;font-size:12px;padding:7px 14px;
  border:none;border-radius:8px;cursor:pointer;}
.btn-nuvem{background:linear-gradient(135deg,#00b1e1,#0090b8);color:#fff;}

/* ── STATS ── */
.stats-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(110px,1fr));
  gap:10px;margin-bottom:16px;}
.stat-box{background:#fff;border-radius:12px;padding:14px 16px;text-align:center;
  box-shadow:0 2px 10px rgba(0,0,0,.06);border-top:3px solid var(--rose);}
.stat-box .num{font-size:22px;font-weight:800;color:var(--rose-dark);}
.stat-box .lbl{font-size:10px;color:var(--muted);margin-top:2px;text-transform:uppercase;letter-spacing:.4px;}
.stat-box.warn{border-top-color:#fd7e14;}.stat-box.warn .num{color:#fd7e14;}
.stat-box.ok{border-top-color:#28a745;}.stat-box.ok .num{color:#28a745;}
.stat-box.blue{border-top-color:#007bff;}.stat-box.blue .num{color:#007bff;}
.stat-box.gold{border-top-color:var(--gold);}.stat-box.gold .num{color:var(--gold);}

/* ── CARDS DE LISTA ── */
.hist-wrap{max-height:60vh;overflow-y:auto;padding-right:4px;}
.hist-wrap::-webkit-scrollbar{width:4px;}
.hist-wrap::-webkit-scrollbar-thumb{background:var(--rose-light);border-radius:10px;}
.entry{background:#fff;border-radius:12px;padding:14px;margin-bottom:10px;
  box-shadow:0 2px 8px rgba(0,0,0,.06);display:grid;
  grid-template-columns:68px 1fr auto;gap:12px;align-items:start;
  border-left:4px solid var(--rose-light);transition:box-shadow .2s;}
.entry:hover{box-shadow:0 4px 16px rgba(0,0,0,.1);border-left-color:var(--rose);}
.entry.low{border-left-color:#fd7e14;}
.entry.synced{border-left-color:#28a745;}
.entry img{width:68px;height:68px;object-fit:cover;border-radius:8px;}
.entry .no-img{width:68px;height:68px;border-radius:8px;background:var(--rose-light);
  display:flex;align-items:center;justify-content:center;font-size:22px;}
.entry-info h3{font-size:13px;font-weight:700;margin-bottom:3px;}
.entry-info .ref{font-size:10px;color:var(--muted);font-family:monospace;margin-bottom:3px;}
.entry-info .meta{font-size:11px;color:var(--muted);}
.entry-actions{display:flex;flex-direction:column;align-items:flex-end;gap:5px;}
.entry-date{font-size:10px;color:#bbb;text-align:right;margin-bottom:4px;}
.pills{display:flex;gap:5px;flex-wrap:wrap;margin-top:4px;}
.pill{border-radius:6px;padding:2px 8px;font-size:10px;font-weight:600;}
.pill-rose{background:var(--rose-light);color:var(--rose-dark);}
.pill-green{background:#e8f5e9;color:#2e7d32;}
.pill-blue{background:#e3f2fd;color:#1565c0;}
.pill-gold{background:#fff8e1;color:#856404;}
.pill-orange{background:#fff3e0;color:#e65100;}
.pill-red{background:#ffebee;color:#c62828;}
.tipo-badge{display:inline-block;padding:1px 8px;border-radius:12px;font-size:10px;font-weight:700;}
.tipo-Joia{background:#fff3cd;color:#856404;}
.tipo-Bijuteria{background:#d1ecf1;color:#0c5460;}
.tipo-Semijoia{background:#f8d7da;color:#721c24;}
.tipo-Acessório{background:#d4edda;color:#155724;}
.tipo-Outro{background:#e2e3e5;color:#383d41;}

/* ── FILTROS ── */
.filtros{display:flex;gap:8px;flex-wrap:wrap;margin-bottom:12px;align-items:center;}
.filtros select,.filtros input{padding:7px 12px;border:1.5px solid #e0d0d5;
  border-radius:8px;font-size:12px;background:#fff;font-family:inherit;}

/* ── FRENTE DE CAIXA ── */
.caixa-layout{display:grid;grid-template-columns:1fr 340px;gap:20px;}
@media(max-width:900px){.caixa-layout{grid-template-columns:1fr;}}
.produto-search{position:relative;}
.search-results{position:absolute;top:100%;left:0;right:0;background:#fff;
  border:1.5px solid var(--rose);border-radius:0 0 10px 10px;z-index:50;
  max-height:200px;overflow-y:auto;display:none;}
.search-item{padding:10px 14px;cursor:pointer;font-size:13px;border-bottom:1px solid #f0e0e5;}
.search-item:hover{background:var(--rose-light);}
.search-item .si-ref{font-size:10px;color:var(--muted);}
.carrinho{background:#fff;border-radius:12px;box-shadow:0 4px 20px rgba(0,0,0,.1);}
.carrinho-header{background:linear-gradient(135deg,var(--rose-dark),var(--dark));
  color:#fff;padding:14px 16px;border-radius:12px 12px 0 0;font-weight:700;font-size:14px;}
.carrinho-items{min-height:200px;max-height:340px;overflow-y:auto;padding:12px;}
.cart-item{display:flex;justify-content:space-between;align-items:center;
  padding:8px 0;border-bottom:1px solid #f0e0e5;font-size:13px;}
.cart-item .ci-nome{flex:1;font-weight:600;}
.cart-item .ci-qty{display:flex;align-items:center;gap:6px;margin:0 10px;}
.cart-item .ci-qty button{width:22px;height:22px;border:1px solid #ddd;border-radius:4px;
  background:#f5f5f5;cursor:pointer;font-size:14px;display:flex;align-items:center;justify-content:center;}
.cart-item .ci-preco{color:var(--rose-dark);font-weight:700;min-width:70px;text-align:right;}
.cart-item .ci-del{color:#dc3545;cursor:pointer;margin-left:8px;font-size:16px;}
.carrinho-footer{padding:14px 16px;border-top:2px solid var(--rose-light);}
.total-line{display:flex;justify-content:space-between;font-size:13px;margin-bottom:6px;color:var(--muted);}
.total-line.destaque{font-size:16px;font-weight:800;color:var(--rose-dark);}
.pgto-btns{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin:12px 0;}
.pgto-btn{padding:10px;border:2px solid #e0d0d5;border-radius:8px;background:#fff;
  cursor:pointer;font-size:12px;font-weight:600;color:var(--muted);text-align:center;
  transition:all .2s;}
.pgto-btn.active{border-color:var(--rose);background:var(--rose-light);color:var(--rose-dark);}
.desconto-field{display:flex;gap:8px;align-items:center;margin-bottom:10px;}
.desconto-field input{width:80px;padding:7px;border:1.5px solid #e0d0d5;
  border-radius:8px;font-size:13px;background:#fdf5f7;text-align:center;}
.desconto-field label{font-size:12px;color:var(--muted);}

/* ── DRE ── */
.dre-periodo{display:flex;gap:10px;align-items:flex-end;flex-wrap:wrap;
  background:#fff;border-radius:12px;padding:16px;box-shadow:0 2px 8px rgba(0,0,0,.06);
  margin-bottom:20px;}
.dre-periodo .pf{display:flex;flex-direction:column;gap:4px;}
.dre-periodo label{font-size:11px;font-weight:700;color:var(--rose-dark);text-transform:uppercase;}
.dre-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(200px,1fr));gap:14px;margin-bottom:20px;}
.dre-card{background:#fff;border-radius:12px;padding:18px;
  box-shadow:0 2px 10px rgba(0,0,0,.06);}
.dre-card .dc-label{font-size:11px;font-weight:700;color:var(--muted);
  text-transform:uppercase;letter-spacing:.4px;margin-bottom:6px;}
.dre-card .dc-valor{font-size:26px;font-weight:800;}
.dre-card .dc-desc{font-size:11px;color:var(--muted);margin-top:4px;}
.dre-card.receita{border-top:3px solid #28a745;}.dre-card.receita .dc-valor{color:#28a745;}
.dre-card.custo{border-top:3px solid #fd7e14;}.dre-card.custo .dc-valor{color:#fd7e14;}
.dre-card.despesa{border-top:3px solid #dc3545;}.dre-card.despesa .dc-valor{color:#dc3545;}
.dre-card.lucro{border-top:3px solid var(--rose);}.dre-card.lucro .dc-valor{color:var(--rose-dark);}
.dre-card.margem{border-top:3px solid var(--gold);}.dre-card.margem .dc-valor{color:var(--gold);}
.dre-table{width:100%;border-collapse:collapse;font-size:13px;}
.dre-table th{background:var(--rose-light);color:var(--rose-dark);padding:10px 12px;
  text-align:left;font-size:11px;text-transform:uppercase;letter-spacing:.4px;}
.dre-table td{padding:10px 12px;border-bottom:1px solid #f5eef0;}
.dre-table tr:hover td{background:#fdf5f7;}
.dre-table .total-row td{font-weight:800;background:var(--rose-light);color:var(--rose-dark);}
.despesa-form{display:grid;grid-template-columns:2fr 1fr 1fr auto;gap:10px;
  align-items:end;margin-bottom:16px;}
@media(max-width:700px){.despesa-form{grid-template-columns:1fr 1fr;}}

/* ── SUGESTÕES ── */
.sug-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:16px;}
.sug-card{background:#fff;border-radius:14px;padding:18px;
  box-shadow:0 4px 16px rgba(0,0,0,.08);border-top:4px solid var(--rose);}
.sug-card.urgente{border-top-color:#dc3545;}
.sug-card.atencao{border-top-color:#fd7e14;}
.sug-card.positivo{border-top-color:#28a745;}
.sug-card.info{border-top-color:#007bff;}
.sug-card .sug-icon{font-size:28px;margin-bottom:8px;}
.sug-card .sug-titulo{font-size:14px;font-weight:700;color:var(--brown);margin-bottom:4px;}
.sug-card .sug-desc{font-size:12px;color:var(--muted);line-height:1.6;margin-bottom:10px;}
.sug-card .sug-acao{background:var(--rose-light);color:var(--rose-dark);
  border:none;padding:7px 14px;border-radius:8px;font-size:12px;font-weight:700;cursor:pointer;}
.sug-card.urgente .sug-acao{background:#ffebee;color:#c62828;}
.sug-card.atencao .sug-acao{background:#fff3e0;color:#e65100;}
.sug-card.positivo .sug-acao{background:#e8f5e9;color:#2e7d32;}
.sug-prioridade{display:inline-block;border-radius:8px;padding:2px 10px;
  font-size:10px;font-weight:800;margin-bottom:8px;text-transform:uppercase;}
.prior-alta{background:#ffebee;color:#c62828;}
.prior-media{background:#fff3e0;color:#e65100;}
.prior-baixa{background:#e8f5e9;color:#2e7d32;}
.prior-info{background:#e3f2fd;color:#1565c0;}

/* ── CLIENTE CARD ── */
.cliente-card{background:#fff;border-radius:12px;padding:14px;margin-bottom:10px;
  box-shadow:0 2px 8px rgba(0,0,0,.06);border-left:4px solid var(--rose-light);
  display:grid;grid-template-columns:48px 1fr auto;gap:12px;align-items:start;}
.cliente-card:hover{box-shadow:0 4px 16px rgba(0,0,0,.1);border-left-color:var(--rose);}
.avatar{width:48px;height:48px;border-radius:50%;background:linear-gradient(135deg,var(--rose),var(--rose-dark));
  display:flex;align-items:center;justify-content:center;color:#fff;font-size:18px;font-weight:700;}
.cliente-info h3{font-size:13px;font-weight:700;margin-bottom:2px;}
.cliente-info .ci-meta{font-size:11px;color:var(--muted);}
.clube-tag{display:inline-block;background:linear-gradient(135deg,var(--rose),var(--gold));
  color:#fff;border-radius:8px;padding:2px 8px;font-size:10px;font-weight:700;margin-top:3px;}

/* ── FORNECEDOR CARD ── */
.forn-card{background:#fff;border-radius:12px;padding:14px;margin-bottom:10px;
  box-shadow:0 2px 8px rgba(0,0,0,.06);border-left:4px solid #e3f2fd;}
.forn-card:hover{box-shadow:0 4px 16px rgba(0,0,0,.1);border-left-color:#007bff;}

/* ── VENDA CARD ── */
.venda-card{background:#fff;border-radius:12px;padding:14px;margin-bottom:10px;
  box-shadow:0 2px 8px rgba(0,0,0,.06);border-left:4px solid #e8f5e9;}
.venda-card:hover{box-shadow:0 4px 16px rgba(0,0,0,.1);border-left-color:#28a745;}

/* ── INTEGRAÇÃO ── */
.integ-card{background:linear-gradient(135deg,#e3f2fd,#f0f8ff);
  border:1.5px solid #b3d9f7;border-radius:12px;padding:16px;margin-bottom:16px;}
.integ-card h3{font-size:13px;font-weight:700;color:#0277bd;margin-bottom:8px;}
.dot{width:8px;height:8px;border-radius:50%;}
.dot.on{background:#28a745;box-shadow:0 0 6px #28a74580;}
.dot.off{background:#ccc;}
.integ-status{display:flex;align-items:center;gap:8px;font-size:12px;margin-top:8px;}
.log-box{background:#1a1a2e;border-radius:10px;padding:14px;font-family:monospace;
  font-size:11px;color:#90ee90;max-height:160px;overflow-y:auto;margin-top:10px;}
.log-item{padding:2px 0;border-bottom:1px solid rgba(255,255,255,.05);}
.log-item.err{color:#ff6b6b;}.log-item.ok{color:#90ee90;}.log-item.info{color:#87ceeb;}

/* ── MODAL ── */
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,.55);
  display:none;align-items:center;justify-content:center;z-index:200;padding:16px;}
.modal-overlay.open{display:flex;}
.modal-box{background:#fff;border-radius:16px;padding:28px;width:100%;max-width:480px;
  box-shadow:0 16px 48px rgba(0,0,0,.25);max-height:90vh;overflow-y:auto;}
.modal-box h3{font-size:16px;font-weight:700;color:var(--brown);margin-bottom:18px;}
.modal-btns{display:flex;gap:10px;margin-top:14px;}
.modal-btns button{flex:1;padding:11px;border:none;border-radius:8px;
  font-size:13px;font-weight:700;cursor:pointer;}
.mb-ok{background:linear-gradient(135deg,var(--rose),var(--rose-dark));color:#fff;}
.mb-cancel{background:#f0f0f0;color:#666;}

/* ── ALERTA ── */
.alerta-box{background:#fff3cd;border:1px solid #ffc107;border-radius:10px;
  padding:12px 16px;margin-bottom:14px;font-size:12px;color:#856404;}
.alerta-box strong{display:block;margin-bottom:4px;}

/* ── CLUBE LINK ── */
.clube-link-box{background:linear-gradient(135deg,var(--rose-light),#fff);
  border:1.5px solid var(--rose);border-radius:12px;padding:16px;margin-bottom:16px;}
.clube-link-box p{font-size:12px;color:var(--muted);margin-bottom:8px;}
.link-display{display:flex;gap:8px;align-items:center;}
.link-display input{flex:1;background:#fff;font-size:12px;color:var(--rose-dark);
  font-weight:600;border:1.5px solid var(--rose-light);border-radius:8px;padding:8px 12px;}

/* ── TOAST ── */
#toast{position:fixed;bottom:24px;right:24px;background:var(--dark);color:#f7e8ec;
  padding:11px 18px;border-radius:10px;font-size:13px;font-weight:600;
  opacity:0;transform:translateY(8px);transition:all .3s;z-index:999;pointer-events:none;}
#toast.show{opacity:1;transform:translateY(0);}
.empty{text-align:center;color:#d4a0b0;font-size:13px;padding:36px 20px;}
.periodo-form{display:flex;gap:10px;align-items:flex-end;flex-wrap:wrap;
  background:#fff;border-radius:12px;padding:16px;
  box-shadow:0 2px 8px rgba(0,0,0,.06);margin-bottom:16px;}
.periodo-form .pf{display:flex;flex-direction:column;gap:4px;}
.periodo-form label{font-size:11px;font-weight:700;color:var(--rose-dark);text-transform:uppercase;}
.rel-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:12px;margin-bottom:16px;}
.rel-card{background:#fff;border-radius:12px;padding:14px;box-shadow:0 2px 10px rgba(0,0,0,.06);border-top:3px solid var(--rose);}
.rel-card h4{font-size:11px;font-weight:700;color:var(--muted);text-transform:uppercase;letter-spacing:.4px;margin-bottom:6px;}
.rel-card .big{font-size:26px;font-weight:800;color:var(--rose-dark);}
.rel-table{width:100%;border-collapse:collapse;font-size:12px;}
.rel-table th{background:var(--rose-light);color:var(--rose-dark);padding:8px 10px;
  text-align:left;font-size:11px;text-transform:uppercase;letter-spacing:.4px;}
.rel-table td{padding:8px 10px;border-bottom:1px solid #f5eef0;}
.rel-table tr:hover td{background:#fdf5f7;}
</style>
</head>
<body>

<!-- ══ TELA DE LOGIN ══ -->
<div class="login-screen" id="login-screen">
  <div class="login-box">
    <div class="geor-logo">GÉOR</div>
    <div class="sub">SEMIJOIAS & ACESSÓRIOS</div>
    <div class="lf"><label>Usuário</label>
      <input type="text" id="l-user" placeholder="Digite seu usuário"/></div>
    <div class="lf"><label>Senha</label>
      <input type="password" id="l-pass" placeholder="Digite sua senha"
        onkeydown="if(event.key==='Enter')login()"/></div>
    <button class="btn-login" onclick="login()">🔐 Entrar</button>
    <div class="login-error" id="login-error">Usuário ou senha incorretos.</div>
  </div>
</div>

<!-- ══ CLUBE DE VANTAGENS (PÚBLICO) ══ -->
<div class="clube-screen" id="clube-screen">
  <div class="clube-box">
    <div class="clube-header">
      <div class="clube-logo">GÉOR</div>
      <div class="clube-sub">SEMIJOIAS & ACESSÓRIOS</div>
      <div class="clube-badge">💎 Clube de Vantagens</div>
      <div class="clube-beneficios">
        <p>✨ Acesso antecipado a novas coleções</p>
        <p>🎁 Desconto exclusivo na primeira compra</p>
        <p>📱 Ofertas especiais via WhatsApp</p>
        <p>🎂 Presente surpresa no seu aniversário</p>
      </div>
    </div>
    <div id="clube-form-area">
      <div class="field"><label>Nome Completo *</label>
        <input type="text" id="cb-nome" placeholder="Seu nome completo"/></div>
      <div class="field"><label>WhatsApp *</label>
        <input type="tel" id="cb-tel" placeholder="(00) 00000-0000"/></div>
      <div class="field"><label>E-mail</label>
        <input type="email" id="cb-email" placeholder="seu@email.com"/></div>
      <div class="field"><label>Data de Aniversário</label>
        <input type="date" id="cb-aniv"/></div>
      <div class="field"><label>Cidade</label>
        <input type="text" id="cb-cidade" placeholder="Sua cidade"/></div>
      <div class="field"><label>Como nos conheceu?</label>
        <select id="cb-origem">
          <option value="">Selecione...</option>
          <option>Instagram</option>
          <option>Indicação de amiga</option>
          <option>Passou na loja</option>
          <option>WhatsApp</option>
          <option>Outro</option>
        </select>
      </div>
      <button class="btn-clube" onclick="cadastrarClube()">💎 Quero Fazer Parte!</button>
    </div>
    <div class="clube-success" id="clube-success">
      <div class="icon">🎉</div>
      <h3>Bem-vinda ao Clube Géor!</h3>
      <p>Seu cadastro foi realizado com sucesso.<br>
         Em breve você receberá nossas novidades e vantagens exclusivas pelo WhatsApp!</p>
    </div>
  </div>
</div>

<!-- ══ SISTEMA ══ -->
<div class="sistema" id="sistema">
  <header>
    <div class="h-left">
      <div class="h-logo">GÉOR</div>
      <div class="h-title">Sistema de Gestão</div>
    </div>
    <div class="h-right">
      <div class="sync-status sync-off" id="sync-indicator">⚡ Make: Desconectado</div>
      <div class="user-badge" id="user-badge">👤 —</div>
      <button class="btn-logout" onclick="logout()">Sair</button>
    </div>
  </header>

  <div class="tabs">
    <div class="tab active" onclick="aba('checkin')">📦 Check-in</div>
    <div class="tab" onclick="aba('estoque')">🗄️ Estoque</div>
    <div class="tab" onclick="aba('caixa')">🛒 Caixa</div>
    <div class="tab" onclick="aba('clientes')">👥 Clientes</div>
    <div class="tab" onclick="aba('fornecedores')">🏭 Fornecedores</div>
    <div class="tab" onclick="aba('dre')">📊 DRE</div>
    <div class="tab" onclick="aba('sugestoes')">💡 Sugestões</div>
    <div class="tab" onclick="aba('relatorio')">📋 Relatório</div>
    <div class="tab admin-tab" style="display:none" onclick="aba('admin')">⚙️ Admin</div>
  </div>

  <!-- ══ ABA CHECK-IN ══ -->
  <div class="painel active" id="tab-checkin">
    <div class="grid-form">
      <div class="card">
        <h2>📦 Novo Registro de Produto</h2>
        <div class="field"><label>Foto do Produto</label>
          <div style="border:2px dashed #e0c0cc;border-radius:10px;padding:16px;
            text-align:center;cursor:pointer;position:relative;background:#fdf5f7;">
            <input type="file" accept="image/*" id="foto-input"
              style="position:absolute;inset:0;opacity:0;cursor:pointer;width:100%;height:100%;"/>
            <div style="font-size:26px;margin-bottom:4px;">📷</div>
            <p style="font-size:11px;color:var(--muted);">Clique para adicionar foto</p>
          </div>
          <img id="preview-img" alt="" style="width:100%;max-height:140px;object-fit:cover;
            border-radius:8px;margin-top:8px;display:none;"/>
        </div>
        <div class="field"><label>Nome / Descrição *</label>
          <input type="text" id="f-nome" placeholder="Ex: Anel Solitário Banhado a Ouro"/></div>
        <div class="row2">
          <div class="field"><label>Código / Referência *</label>
            <input type="text" id="f-ref" placeholder="Ex: GR-001"/></div>
          <div class="field"><label>Tipo *</label>
            <select id="f-tipo">
              <option value="">Selecione...</option>
              <option>Joia</option><option>Bijuteria</option>
              <option>Semijoia</option><option>Acessório</option><option>Outro</option>
            </select>
          </div>
        </div>
        <div class="field"><label>Fornecedor</label>
          <input type="text" id="f-forn" placeholder="Nome do fornecedor"/></div>
        <div class="row2">
          <div class="field"><label>Preço de Custo (R$)</label>
            <input type="number" id="f-custo" min="0" step="0.01" placeholder="0,00"/></div>
          <div class="field"><label>Preço de Venda (R$)</label>
            <input type="number" id="f-preco" min="0" step="0.01" placeholder="0,00"/></div>
        </div>
        <div class="row3">
          <div class="field"><label>Qtd. Gôndola</label>
            <input type="number" id="f-gondola" min="0" placeholder="0"/></div>
          <div class="field"><label>Qtd. Estoque</label>
            <input type="number" id="f-estoque" min="0" placeholder="0"/></div>
          <div class="field"><label>Alertar abaixo de</label>
            <input type="number" id="f-alerta" min="0" placeholder="5"/></div>
        </div>
        <div class="field"><label>Observações</label>
          <textarea id="f-obs" placeholder="Cor, tamanho, coleção..."></textarea></div>
        <button class="btn btn-primary" onclick="registrar()">✅ Registrar Check-in</button>
      </div>
      <div>
        <div class="stats-grid" id="stats-checkin"></div>
        <div id="alertas-top"></div>
        <div class="card" style="padding:18px;">
          <div style="display:flex;justify-content:space-between;align-items:center;
            margin-bottom:12px;flex-wrap:wrap;gap:8px;">
            <h2 style="margin:0;padding:0;border:none;font-size:14px;">📋 Histórico de Entradas</h2>
            <button class="btn-dark" onclick="exportarCSV()">⬇️ CSV</button>
          </div>
          <div class="filtros">
            <select id="ft-tipo" onchange="renderCheckin()">
              <option value="">Todos os tipos</option>
              <option>Joia</option><option>Bijuteria</option>
              <option>Semijoia</option><option>Acessório</option><option>Outro</option>
            </select>
            <input type="text" id="ft-busca" placeholder="🔍 Nome ou código..."
              oninput="renderCheckin()" style="flex:1;min-width:120px;"/>
          </div>
          <div class="hist-wrap" id="hist-checkin"></div>
        </div>
      </div>
    </div>
  </div>

  <!-- ══ ABA ESTOQUE ══ -->
  <div class="painel" id="tab-estoque">
    <div class="stats-grid" id="stats-estoque"></div>
    <div id="alertas-estoque"></div>
    <div class="card">
      <div style="display:flex;justify-content:space-between;align-items:center;
        margin-bottom:14px;flex-wrap:wrap;gap:8px;">
        <h2 style="margin:0;padding:0;border:none;font-size:14px;">🗄️ Posição de Estoque</h2>
        <button class="btn-dark" onclick="exportarCSV()">⬇️ CSV</button>
      </div>
      <div class="filtros">
        <select id="fe-tipo" onchange="renderEstoque()">
          <option value="">Todos os tipos</option>
          <option>Joia</option><option>Bijuteria</option>
          <option>Semijoia</option><option>Acessório</option><option>Outro</option>
        </select>
        <select id="fe-alerta" onchange="renderEstoque()">
          <option value="">Todos</option>
          <option value="low">⚠️ Estoque baixo</option>
          <option value="ok">✅ Estoque ok</option>
        </select>
        <input type="text" id="fe-busca" placeholder="🔍 Nome ou código..."
          oninput="renderEstoque()" style="flex:1;min-width:120px;"/>
      </div>
      <div class="hist-wrap" id="hist-estoque"></div>
    </div>
  </div>

  <!-- ══ ABA CAIXA ══ -->
  <div class="painel" id="tab-caixa">
    <div class="caixa-layout">
      <div>
        <div class="card">
          <h2>🛒 Nova Venda</h2>
          <div class="row2" style="margin-bottom:12px;">
            <div class="field"><label>Cliente</label>
              <select id="cx-cliente">
                <option value="">Consumidor final</option>
              </select>
            </div>
            <div class="field"><label>Vendedor</label>
              <select id="cx-vendedor">
                <option>Administrador</option>
                <option>Hellen</option>
              </select>
            </div>
          </div>
          <div class="field"><label>Buscar Produto</label>
            <div class="produto-search">
              <input type="text" id="cx-busca-prod" placeholder="🔍 Digite o nome ou código..."
                oninput="buscarProdutoCaixa()" autocomplete="off"/>
              <div class="search-results" id="cx-search-results"></div>
            </div>
          </div>
        </div>
        <div class="card" style="padding:18px;">
          <h2>📊 Últimas Vendas</h2>
          <div class="filtros">
            <input type="date" id="cv-data" onchange="renderVendas()"
              style="font-size:12px;padding:7px 10px;"/>
            <input type="text" id="cv-busca" placeholder="🔍 Buscar..."
              oninput="renderVendas()" style="flex:1;"/>
          </div>
          <div class="hist-wrap" id="hist-vendas"></div>
        </div>
      </div>
      <!-- CARRINHO -->
      <div class="carrinho">
        <div class="carrinho-header">🛒 Carrinho</div>
        <div class="carrinho-items" id="carrinho-items">
          <div class="empty" style="padding:24px;">
            <div style="font-size:30px;margin-bottom:8px;">🛍️</div>
            <p>Nenhum item adicionado</p>
          </div>
        </div>
        <div class="carrinho-footer">
          <div class="total-line"><span>Subtotal</span><span id="cx-subtotal">R$ 0,00</span></div>
          <div class="desconto-field">
            <label>Desconto R$</label>
            <input type="number" id="cx-desconto" min="0" step="0.01" value="0"
              oninput="calcTotal()"/>
          </div>
          <div class="total-line destaque">
            <span>Total</span><span id="cx-total">R$ 0,00</span>
          </div>
          <div class="pgto-btns">
            <button class="pgto-btn active" onclick="setPgto(this,'Dinheiro')">💵 Dinheiro</button>
            <button class="pgto-btn" onclick="setPgto(this,'Cartão Débito')">💳 Débito</button>
            <button class="pgto-btn" onclick="setPgto(this,'Cartão Crédito')">💳 Crédito</button>
            <button class="pgto-btn" onclick="setPgto(this,'Pix')">📱 Pix</button>
          </div>
          <input type="hidden" id="cx-pgto" value="Dinheiro"/>
          <div class="field"><label>Observação</label>
            <input type="text" id="cx-obs-venda" placeholder="Opcional..."/></div>
          <button class="btn btn-primary" onclick="finalizarVenda()"
            style="margin-top:8px;">✅ Finalizar Venda</button>
          <button class="btn-sm btn-danger" onclick="limparCarrinho()"
            style="width:100%;margin-top:6px;padding:6px;">🗑️ Limpar Carrinho</button>
        </div>
      </div>
    </div>
  </div>

  <!-- ══ ABA CLIENTES ══ -->
  <div class="painel" id="tab-clientes">
    <div class="grid-form">
      <div class="card">
        <h2>👥 Cadastrar Cliente</h2>
        <div class="field"><label>Nome Completo *</label>
          <input type="text" id="cl-nome" placeholder="Nome do cliente"/></div>
        <div class="row2">
          <div class="field"><label>WhatsApp *</label>
            <input type="tel" id="cl-tel" placeholder="(00) 00000-0000"/></div>
          <div class="field"><label>E-mail</label>
            <input type="email" id="cl-email" placeholder="email@email.com"/></div>
        </div>
        <div class="row2">
          <div class="field"><label>Data de Nascimento</label>
            <input type="date" id="cl-aniv"/></div>
          <div class="field"><label>CPF</label>
            <input type="text" id="cl-cpf" placeholder="000.000.000-00"/></div>
        </div>
        <div class="field"><label>Endereço</label>
          <input type="text" id="cl-end" placeholder="Rua, número, bairro"/></div>
        <div class="row2">
          <div class="field"><label>Cidade</label>
            <input type="text" id="cl-cidade" placeholder="Cidade"/></div>
          <div class="field"><label>Como nos conheceu?</label>
            <select id="cl-origem">
              <option value="">Selecione...</option>
              <option>Instagram</option><option>Indicação</option>
              <option>Passou na loja</option><option>WhatsApp</option><option>Outro</option>
            </select>
          </div>
        </div>
        <div class="field"><label>Observações</label>
          <textarea id="cl-obs" placeholder="Preferências, tamanhos, etc..."></textarea></div>
        <div style="display:flex;align-items:center;gap:10px;margin-bottom:14px;">
          <input type="checkbox" id="cl-clube" style="width:auto;"/>
          <label for="cl-clube" style="font-size:13px;font-weight:600;color:var(--rose-dark);
            text-transform:none;letter-spacing:0;">💎 Membro do Clube de Vantagens</label>
        </div>
        <button class="btn btn-primary" onclick="cadastrarCliente()">✅ Cadastrar Cliente</button>

        <!-- LINK CLUBE -->
        <div class="clube-link-box" style="margin-top:18px;">
          <p>🔗 Compartilhe este link para que clientes se cadastrem no Clube:</p>
          <div class="link-display">
            <input type="text" id="clube-link-url" readonly/>
            <button class="btn-dark" onclick="copiarLink()">📋 Copiar</button>
          </div>
        </div>
      </div>
      <div>
        <div class="stats-grid" id="stats-clientes"></div>
        <div class="card" style="padding:18px;">
          <h2>📋 Lista de Clientes</h2>
          <div class="filtros">
            <select id="fcl-clube" onchange="renderClientes()">
              <option value="">Todos</option>
              <option value="sim">💎 Clube</option>
              <option value="nao">Sem clube</option>
            </select>
            <input type="text" id="fcl-busca" placeholder="🔍 Nome ou WhatsApp..."
              oninput="renderClientes()" style="flex:1;"/>
          </div>
          <div class="hist-wrap" id="hist-clientes"></div>
        </div>
      </div>
    </div>
  </div>

  <!-- ══ ABA FORNECEDORES ══ -->
  <div class="painel" id="tab-fornecedores">
    <div class="grid-form">
      <div class="card">
        <h2>🏭 Cadastrar Fornecedor</h2>
        <div class="field"><label>Nome / Razão Social *</label>
          <input type="text" id="fn-nome" placeholder="Nome do fornecedor"/></div>
        <div class="row2">
          <div class="field"><label>Contato / WhatsApp</label>
            <input type="tel" id="fn-tel" placeholder="(00) 00000-0000"/></div>
          <div class="field"><label>E-mail</label>
            <input type="email" id="fn-email" placeholder="contato@fornecedor.com"/></div>
        </div>
        <div class="row2">
          <div class="field"><label>CNPJ / CPF</label>
            <input type="text" id="fn-cnpj" placeholder="00.000.000/0001-00"/></div>
          <div class="field"><label>Cidade / Estado</label>
            <input type="text" id="fn-cidade" placeholder="São Paulo / SP"/></div>
        </div>
        <div class="field"><label>Categorias que fornece</label>
          <input type="text" id="fn-cats" placeholder="Ex: Semijoias, Anéis, Colares"/></div>
        <div class="row2">
          <div class="field"><label>Prazo médio de entrega</label>
            <input type="text" id="fn-prazo" placeholder="Ex: 7 dias úteis"/></div>
          <div class="field"><label>Pedido mínimo (R$)</label>
            <input type="number" id="fn-minimo" min="0" step="0.01" placeholder="0,00"/></div>
        </div>
        <div class="field"><label>Condições de pagamento</label>
          <input type="text" id="fn-pgto" placeholder="Ex: Boleto 30 dias, Pix à vista"/></div>
        <div class="field"><label>Observações</label>
          <textarea id="fn-obs" placeholder="Qualidade dos produtos, histórico..."></textarea></div>
        <button class="btn btn-primary" onclick="cadastrarFornecedor()">✅ Cadastrar Fornecedor</button>
      </div>
      <div>
        <div class="stats-grid" id="stats-fornecedores"></div>
        <div class="card" style="padding:18px;">
          <h2>📋 Lista de Fornecedores</h2>
          <div class="filtros">
            <input type="text" id="ffn-busca" placeholder="🔍 Nome ou cidade..."
              oninput="renderFornecedores()" style="flex:1;"/>
          </div>
          <div class="hist-wrap" id="hist-fornecedores"></div>
        </div>
      </div>
    </div>
  </div>

  <!-- ══ ABA DRE ══ -->
  <div class="painel" id="tab-dre">
    <div class="dre-periodo">
      <div class="pf"><label>Mês/Ano</label>
        <input type="month" id="dre-mes" style="padding:8px 12px;border:1.5px solid #e0d0d5;
          border-radius:8px;font-size:13px;background:#fdf5f7;"/></div>
      <button class="btn btn-primary" style="width:auto;padding:9px 20px;"
        onclick="gerarDRE()">📊 Gerar DRE</button>
    </div>

    <div class="dre-grid" id="dre-cards"></div>

    <!-- LANÇAR DESPESAS -->
    <div class="card">
      <h2>💸 Lançar Despesas</h2>
      <div class="despesa-form">
        <div class="field" style="margin:0;">
          <label>Descrição</label>
          <input type="text" id="dp-desc" placeholder="Ex: Aluguel, Embalagens..."/></div>
        <div class="field" style="margin:0;">
          <label>Categoria</label>
          <select id="dp-cat">
            <option>Fixo</option><option>Variável</option>
            <option>CMV</option><option>Marketing</option><option>Outro</option>
          </select>
        </div>
        <div class="field" style="margin:0;">
          <label>Valor (R$)</label>
          <input type="number" id="dp-valor" min="0" step="0.01" placeholder="0,00"/></div>
        <div class="field" style="margin:0;">
          <label>Data</label>
          <input type="date" id="dp-data"/></div>
        <button class="btn btn-primary" style="width:auto;padding:9px 16px;align-self:end;"
          onclick="lancarDespesa()">+ Lançar</button>
      </div>
      <div class="hist-wrap" id="hist-despesas"></div>
    </div>

    <!-- DEMONSTRATIVO -->
    <div class="card">
      <h2>📄 Demonstrativo de Resultado</h2>
      <div style="overflow-x:auto;">
        <table class="dre-table" id="dre-table">
          <thead>
            <tr><th>Descrição</th><th>Valor</th><th>%</th></tr>
          </thead>
          <tbody id="dre-tbody"></tbody>
        </table>
      </div>
    </div>
  </div>

  <!-- ══ ABA SUGESTÕES ══ -->
  <div class="painel" id="tab-sugestoes">
    <div style="display:flex;justify-content:space-between;align-items:center;
      margin-bottom:18px;flex-wrap:wrap;gap:10px;">
      <div>
        <h2 style="font-size:18px;font-weight:800;color:var(--brown);">💡 Painel de Sugestões</h2>
        <p style="font-size:12px;color:var(--muted);margin-top:2px;">
          Ações recomendadas com base nos dados da sua loja</p>
      </div>
      <button class="btn-dark" onclick="gerarSugestoes()">🔄 Atualizar</button>
    </div>

    <div class="sug-grid" id="sug-grid">
      <div class="empty"><div class="icon">💡</div><p>Clique em "Atualizar" para gerar sugestões</p></div>
    </div>
  </div>

  <!-- ══ ABA RELATÓRIO ══ -->
  <div class="painel" id="tab-relatorio">
    <div class="periodo-form">
      <div class="pf"><label>Data Início</label><input type="date" id="r-inicio"/></div>
      <div class="pf"><label>Data Fim</label><input type="date" id="r-fim"/></div>
      <div class="pf"><label>Tipo</label>
        <select id="r-tipo">
          <option value="">Todos</option><option>Joia</option><option>Bijuteria</option>
          <option>Semijoia</option><option>Acessório</option><option>Outro</option>
        </select>
      </div>
      <button class="btn btn-primary" style="width:auto;padding:9px 20px;" onclick="gerarRelatorio()">🔍 Gerar</button>
      <button class="btn-dark" onclick="exportarRelCSV()">⬇️ CSV</button>
    </div>
    <div class="rel-grid" id="rel-cards"></div>
    <div class="card" style="padding:18px;">
      <h2>Detalhamento do Período</h2>
      <div style="overflow-x:auto;">
        <table class="rel-table">
          <thead><tr>
            <th>Data</th><th>Código</th><th>Produto</th><th>Tipo</th>
            <th>Gôndola</th><th>Estoque</th><th>Total</th><th>Por</th>
          </tr></thead>
          <tbody id="rel-tbody"></tbody>
        </table>
      </div>
    </div>
  </div>

  <!-- ══ ABA ADMIN ══ -->
  <div class="painel" id="tab-admin">
    <div class="card" style="margin-bottom:16px;">
      <h2>☁️ Integração Nuvemshop via Make</h2>
      <div class="integ-card">
        <h3>🔗 Webhook Make</h3>
        <p style="font-size:12px;color:#555;margin-bottom:10px;">
          Cole a URL do webhook gerada no Make. A cada check-in ou atualização de estoque,
          os dados serão enviados automaticamente para a Nuvemshop.
        </p>
        <div class="field" style="margin-bottom:10px;">
          <label>URL do Webhook</label>
          <input type="url" id="cfg-webhook" placeholder="https://hook.eu1.make.com/xxxxxxxxx"/>
        </div>
        <div style="display:flex;gap:10px;flex-wrap:wrap;">
          <button class="btn btn-primary" style="width:auto;padding:9px 18px;" onclick="salvarWebhook()">💾 Salvar</button>
          <button class="btn-dark" onclick="testarWebhook()">🧪 Testar Conexão</button>
        </div>
        <div class="integ-status" id="integ-status">
          <div class="dot off" id="status-dot"></div>
          <span id="status-txt">Webhook não configurado</span>
        </div>
      </div>
      <p style="font-size:12px;font-weight:700;color:var(--brown);margin-bottom:6px;">📋 Log de Sincronizações</p>
      <div class="log-box" id="log-box">
        <div class="log-item info">— Aguardando sincronizações...</div>
      </div>
      <div style="display:flex;justify-content:flex-end;margin-top:8px;">
        <button class="btn-dark" onclick="limparLogs()">🗑️ Limpar Logs</button>
      </div>
    </div>

    <div class="card">
      <h2>⚙️ Edição de Registros</h2>
      <div class="filtros">
        <input type="text" id="fa-busca" placeholder="🔍 Buscar produto..."
          oninput="renderAdmin()" style="flex:1;"/>
      </div>
      <div class="hist-wrap" id="hist-admin"></div>
    </div>
  </div>
</div>

<!-- ══ MODAL REPOR ══ -->
<div class="modal-overlay" id="repor-modal">
  <div class="modal-box" style="max-width:360px;text-align:center;">
    <h3>🔄 Repor Gôndola</h3>
    <p style="font-size:12px;color:var(--muted);margin-bottom:14px;">Mover unidades do estoque para a gôndola</p>
    <div style="background:var(--rose-light);border-radius:8px;padding:10px;font-size:13px;
      margin-bottom:14px;color:var(--rose-dark);line-height:1.6;" id="repor-info">—</div>
    <input type="number" id="repor-qtd" min="1" placeholder="Quantidade"
      style="width:100%;padding:10px;border:1.5px solid #e0d0d5;border-radius:8px;
      font-size:18px;text-align:center;margin-bottom:14px;background:#fdf5f7;"/>
    <div class="modal-btns">
      <button class="mb-cancel" onclick="fecharModal('repor-modal')">Cancelar</button>
      <button class="mb-ok" onclick="confirmarRepor()">✅ Confirmar</button>
    </div>
  </div>
</div>

<!-- ══ MODAL EDITAR PRODUTO ══ -->
<div class="modal-overlay" id="edit-modal">
  <div class="modal-box">
    <h3>✏️ Editar Produto</h3>
    <input type="hidden" id="edit-id"/>
    <div class="field"><label>Nome</label><input type="text" id="edit-nome"/></div>
    <div class="row2">
      <div class="field"><label>Código</label><input type="text" id="edit-ref"/></div>
      <div class="field"><label>Tipo</label>
        <select id="edit-tipo">
          <option>Joia</option><option>Bijuteria</option>
          <option>Semijoia</option><option>Acessório</option><option>Outro</option>
        </select>
      </div>
    </div>
    <div class="field"><label>Fornecedor</label><input type="text" id="edit-forn"/></div>
    <div class="row2">
      <div class="field"><label>Preço Custo</label><input type="number" id="edit-custo" min="0" step="0.01"/></div>
      <div class="field"><label>Preço Venda</label><input type="number" id="edit-preco" min="0" step="0.01"/></div>
    </div>
    <div class="row3">
      <div class="field"><label>Gôndola</label><input type="number" id="edit-gondola" min="0"/></div>
      <div class="field"><label>Estoque</label><input type="number" id="edit-estoque" min="0"/></div>
      <div class="field"><label>Alertar abaixo de</label><input type="number" id="edit-alerta" min="0"/></div>
    </div>
    <div class="field"><label>Observações</label><textarea id="edit-obs"></textarea></div>
    <div class="modal-btns">
      <button class="mb-cancel" onclick="fecharModal('edit-modal')">Cancelar</button>
      <button class="mb-ok" onclick="salvarEdit()">💾 Salvar</button>
    </div>
  </div>
</div>

<!-- ══ MODAL EDITAR CLIENTE ══ -->
<div class="modal-overlay" id="edit-cliente-modal">
  <div class="modal-box">
    <h3>✏️ Editar Cliente</h3>
    <input type="hidden" id="ecl-id"/>
    <div class="field"><label>Nome</label><input type="text" id="ecl-nome"/></div>
    <div class="row2">
      <div class="field"><label>WhatsApp</label><input type="tel" id="ecl-tel"/></div>
      <div class="field"><label>E-mail</label><input type="email" id="ecl-email"/></div>
    </div>
    <div class="row2">
      <div class="field"><label>Nascimento</label><input type="date" id="ecl-aniv"/></div>
      <div class="field"><label>CPF</label><input type="text" id="ecl-cpf"/></div>
    </div>
    <div class="field"><label>Endereço</label><input type="text" id="ecl-end"/></div>
    <div class="row2">
      <div class="field"><label>Cidade</label><input type="text" id="ecl-cidade"/></div>
      <div class="field"><label>Como nos conheceu?</label>
        <select id="ecl-origem">
          <option value="">Selecione...</option>
          <option>Instagram</option><option>Indicação</option>
          <option>Passou na loja</option><option>WhatsApp</option><option>Outro</option>
        </select>
      </div>
    </div>
    <div class="field"><label>Observações</label><textarea id="ecl-obs"></textarea></div>
    <div style="display:flex;align-items:center;gap:10px;margin-bottom:12px;">
      <input type="checkbox" id="ecl-clube" style="width:auto;"/>
      <label for="ecl-clube" style="font-size:13px;font-weight:600;color:var(--rose-dark);
        text-transform:none;letter-spacing:0;">💎 Membro do Clube de Vantagens</label>
    </div>
    <div class="modal-btns">
      <button class="mb-cancel" onclick="fecharModal('edit-cliente-modal')">Cancelar</button>
      <button class="mb-ok" onclick="salvarEditCliente()">💾 Salvar</button>
    </div>
  </div>
</div>

<!-- ══ MODAL DETALHES VENDA ══ -->
<div class="modal-overlay" id="venda-modal">
  <div class="modal-box">
    <h3>🧾 Detalhes da Venda</h3>
    <div id="venda-detalhe-content"></div>
    <div class="modal-btns">
      <button class="mb-cancel" onclick="fecharModal('venda-modal')">Fechar</button>
    </div>
  </div>
</div>

<div id="toast"></div>

<script>
// ══════════ DADOS & UTILS ══════════
const USERS={admin:{senha:'geor2024',nome:'Administrador',isAdmin:true},
             hellen:{senha:'hellen123',nome:'Hellen',isAdmin:false}};
let USER=null, reporId=null, carrinho=[], pgtoAtual='Dinheiro', relFiltrado=[];

const getData   = ()=>JSON.parse(localStorage.getItem('geor_v3')||'[]');
const setData   = d=>localStorage.setItem('geor_v3',JSON.stringify(d));
const getClientes= ()=>JSON.parse(localStorage.getItem('geor_clientes')||'[]');
const setClientes= d=>localStorage.setItem('geor_clientes',JSON.stringify(d));
const getForn   = ()=>JSON.parse(localStorage.getItem('geor_fornecedores')||'[]');
const setForn   = d=>localStorage.setItem('geor_fornecedores',JSON.stringify(d));
const getVendas = ()=>JSON.parse(localStorage.getItem('geor_vendas')||'[]');
const setVendas = d=>localStorage.setItem('geor_vendas',JSON.stringify(d));
const getDespesas=()=>JSON.parse(localStorage.getItem('geor_despesas')||'[]');
const setDespesas=d=>localStorage.setItem('geor_despesas',JSON.stringify(d));
const moeda = v=>'R$ '+parseFloat(v||0).toFixed(2).replace('.',',');
const fmtData= s=>new Date(s).toLocaleDateString('pt-BR');
const fmtHora= s=>new Date(s).toLocaleString('pt-BR');

function toast(msg,dur=3000){
  const t=document.getElementById('toast');
  t.textContent=msg; t.classList.add('show');
  setTimeout(()=>t.classList.remove('show'),dur);
}
function fecharModal(id){document.getElementById(id).classList.remove('open');}
function abrirModal(id){document.getElementById(id).classList.add('open');}

// ══════════ LOGIN / LOGOUT ══════════
function login(){
  const u=document.getElementById('l-user').value.trim().toLowerCase();
  const s=document.getElementById('l-pass').value;
  const err=document.getElementById('login-error');
  if(USERS[u]&&USERS[u].senha===s){
    USER={login:u,...USERS[u]};
    err.style.display='none';
    document.getElementById('login-screen').style.display='none';
    document.getElementById('sistema').style.display='block';
    document.getElementById('user-badge').innerHTML=
      `👤 ${USER.nome}${USER.isAdmin?'<span class="admin-tag">ADMIN</span>':''}`;
    if(USER.isAdmin) document.querySelectorAll('.admin-tab').forEach(el=>el.style.display='');
    const hoje=new Date(), ini=new Date(hoje.getFullYear(),hoje.getMonth(),1);
    document.getElementById('r-inicio').value=ini.toISOString().slice(0,10);
    document.getElementById('r-fim').value=hoje.toISOString().slice(0,10);
    document.getElementById('dre-mes').value=hoje.toISOString().slice(0,7);
    document.getElementById('dp-data').value=hoje.toISOString().slice(0,10);
    document.getElementById('cv-data').value=hoje.toISOString().slice(0,10);
    const clubeUrl=window.location.href.split('?')[0]+'?clube=1';
    document.getElementById('clube-link-url').value=clubeUrl;
    atualizarStatusWebhook();
    carregarClientesCaixa();
    atualizar();
  } else { err.style.display='block'; }
}
function logout(){
  USER=null;
  document.getElementById('login-screen').style.display='flex';
  document.getElementById('sistema').style.display='none';
  document.getElementById('l-user').value='';
  document.getElementById('l-pass').value='';
}

// ══════════ CLUBE PÚBLICO ══════════
function verificarClube(){
  const params=new URLSearchParams(window.location.search);
  if(params.get('clube')==='1'){
    document.getElementById('login-screen').style.display='none';
    document.getElementById('clube-screen').style.display='flex';
  }
}
function cadastrarClube(){
  const nome=document.getElementById('cb-nome').value.trim();
  const tel=document.getElementById('cb-tel').value.trim();
  if(!nome||!tel) return toast('⚠️ Nome e WhatsApp são obrigatórios.');
  const novo={id:Date.now(),nome,tel,email:document.getElementById('cb-email').value.trim(),
    aniversario:document.getElementById('cb-aniv').value,
    cidade:document.getElementById('cb-cidade').value.trim(),
    origem:document.getElementById('cb-origem').value,
    clube:true,obs:'Cadastro via link do Clube de Vantagens',
    data:new Date().toISOString(),por:'Auto-cadastro'};
  const lista=getClientes(); lista.unshift(novo); setClientes(lista);
  document.getElementById('clube-form-area').style.display='none';
  document.getElementById('clube-success').style.display='block';
}
function copiarLink(){
  const input=document.getElementById('clube-link-url');
  input.select(); document.execCommand('copy');
  toast('📋 Link copiado!');
}

// ══════════ ABAS ══════════
function aba(id){
  const ids=['checkin','estoque','caixa','clientes','fornecedores','dre','sugestoes','relatorio','admin'];
  document.querySelectorAll('.tab').forEach((t,i)=>t.classList.toggle('active',ids[i]===id));
  document.querySelectorAll('.painel').forEach(p=>p.classList.remove('active'));
  document.getElementById('tab-'+id).classList.add('active');
  if(id==='estoque')      renderEstoque();
  if(id==='caixa')        {carregarClientesCaixa();renderVendas();}
  if(id==='clientes')     renderClientes();
  if(id==='fornecedores') renderFornecedores();
  if(id==='dre')          {gerarDRE();renderDespesas();}
  if(id==='sugestoes')    gerarSugestoes();
  if(id==='relatorio')    gerarRelatorio();
  if(id==='admin')        {renderAdmin();carregarCfgWebhook();}
}

// ══════════ FOTO ══════════
let fotoB64=null;
document.getElementById('foto-input').addEventListener('change',function(e){
  const f=e.target.files[0]; if(!f) return;
  const r=new FileReader();
  r.onload=ev=>{fotoB64=ev.target.result;
    const img=document.getElementById('preview-img');
    img.src=fotoB64; img.style.display='block';};
  r.readAsDataURL(f);
});

// ══════════ WEBHOOK ══════════
const getWebhookUrl=()=>localStorage.getItem('geor_webhook')||'';
function salvarWebhook(){
  const url=document.getElementById('cfg-webhook').value.trim();
  localStorage.setItem('geor_webhook',url);
  atualizarStatusWebhook();
  toast(url?'✅ Webhook salvo!':'🗑️ Webhook removido.');
}
function carregarCfgWebhook(){
  document.getElementById('cfg-webhook').value=getWebhookUrl();
  atualizarStatusWebhook();
}
function atualizarStatusWebhook(){
  const url=getWebhookUrl();
  const dot=document.getElementById('status-dot');
  const txt=document.getElementById('status-txt');
  const ind=document.getElementById('sync-indicator');
  if(url){dot.className='dot on';txt.textContent='Webhook ativo';
    ind.className='sync-status sync-ok';ind.textContent='⚡ Make: Conectado';}
  else{dot.className='dot off';txt.textContent='Webhook não configurado';
    ind.className='sync-status sync-off';ind.textContent='⚡ Make: Desconectado';}
}
async function testarWebhook(){
  const url=getWebhookUrl();
  if(!url) return toast('⚠️ Configure a URL do webhook primeiro.');
  adicionarLog('info','🧪 Enviando teste...');
  const ok=await enviarWebhook({evento:'teste',loja:'Géor Semijoias',timestamp:new Date().toISOString()});
  if(ok){adicionarLog('ok','✅ Teste enviado! Verifique o Make.');toast('✅ Teste enviado ao Make!');}
  else{adicionarLog('err','❌ Falha. Verifique a URL.');toast('❌ Falha na conexão.');}
}
async function enviarWebhook(payload){
  const url=getWebhookUrl(); if(!url) return false;
  const ind=document.getElementById('sync-indicator');
  ind.className='sync-status sync-sending'; ind.textContent='⚡ Make: Sincronizando...';
  try{
    await fetch(url,{method:'POST',headers:{'Content-Type':'application/json'},
      mode:'no-cors',body:JSON.stringify(payload)});
    atualizarStatusWebhook(); return true;
  }catch(e){atualizarStatusWebhook(); return false;}
}
function adicionarLog(tipo,msg){
  const box=document.getElementById('log-box'); if(!box) return;
  const hora=new Date().toLocaleTimeString('pt-BR');
  const item=document.createElement('div');
  item.className=`log-item ${tipo}`;
  item.textContent=`[${hora}] ${msg}`;
  if(box.firstChild&&box.firstChild.textContent.includes('Aguardando')) box.innerHTML='';
  box.insertBefore(item,box.firstChild);
  while(box.children.length>50) box.removeChild(box.lastChild);
}
function limparLogs(){
  const box=document.getElementById('log-box');
  if(box) box.innerHTML='<div class="log-item info">— Logs limpos.</div>';
}

// ══════════ CHECK-IN ══════════
async function registrar(){
  const nome=document.getElementById('f-nome').value.trim();
  const ref=document.getElementById('f-ref').value.trim();
  const tipo=document.getElementById('f-tipo').value;
  const forn=document.getElementById('f-forn').value.trim();
  const custo=parseFloat(document.getElementById('f-custo').value)||0;
  const preco=parseFloat(document.getElementById('f-preco').value)||0;
  const gondola=parseInt(document.getElementById('f-gondola').value)||0;
  const estoque=parseInt(document.getElementById('f-estoque').value)||0;
  const alerta=parseInt(document.getElementById('f-alerta').value)||5;
  const obs=document.getElementById('f-obs').value.trim();
  if(!nome) return toast('⚠️ Informe o nome do produto.');
  if(!tipo) return toast('⚠️ Selecione o tipo.');
  if(!ref)  return toast('⚠️ Informe o código/referência.');
  if(gondola===0&&estoque===0) return toast('⚠️ Informe ao menos uma quantidade.');
  const reg={id:Date.now(),data:new Date().toISOString(),nome,ref,tipo,forn,
    custo,preco,gondola,estoque,alerta,obs,foto:fotoB64||null,
    por:USER.nome,sincronizado:false,ultimaSync:null,
    movimentacoes:[{data:new Date().toISOString(),acao:'Check-in inicial',
      gondola,estoque,por:USER.nome}]};
  const lista=getData(); lista.unshift(reg); setData(lista);
  const payload={evento:'novo_produto',sku:ref,nome,tipo,fornecedor:forn,
    preco_custo:custo,preco_venda:preco,
    estoque_gondola:gondola,estoque_deposito:estoque,
    estoque_total:gondola+estoque,observacoes:obs,
    registrado_por:USER.nome,data:new Date().toISOString()};
  const ok=await enviarWebhook(payload);
  if(ok){
    const l2=getData(); const idx=l2.findIndex(x=>x.id===reg.id);
    if(idx>=0){l2[idx].sincronizado=true;l2[idx].ultimaSync=new Date().toISOString();setData(l2);}
    adicionarLog('ok',`✅ [${ref}] ${nome} → Nuvemshop`);
    toast('✅ Produto registrado e sincronizado!');
  } else { toast('✅ Produto registrado!'); }
  limparFormCheckin(); atualizar();
}
function limparFormCheckin(){
  ['f-nome','f-ref','f-forn','f-custo','f-preco','f-gondola','f-estoque','f-obs']
    .forEach(id=>document.getElementById(id).value='');
  document.getElementById('f-tipo').value='';
  document.getElementById('f-alerta').value='';
  document.getElementById('preview-img').style.display='none';
  document.getElementById('foto-input').value=''; fotoB64=null;
}

// ══════════ REPOR GÔNDOLA ══════════
function abrirRepor(id){
  const r=getData().find(x=>x.id===id); if(!r) return;
  reporId=id;
  document.getElementById('repor-info').innerHTML=
    `<strong>${r.nome}</strong><br>🛒 Gôndola: <b>${r.gondola}</b> &nbsp; 📦 Estoque: <b>${r.estoque}</b>`;
  document.getElementById('repor-qtd').value='';
  abrirModal('repor-modal');
}
async function confirmarRepor(){
  const qtd=parseInt(document.getElementById('repor-qtd').value)||0;
  if(qtd<=0) return toast('⚠️ Quantidade inválida.');
  const lista=getData(); const idx=lista.findIndex(x=>x.id===reporId); if(idx<0) return;
  const r=lista[idx];
  if(qtd>r.estoque) return toast(`⚠️ Estoque insuficiente! Disponível: ${r.estoque}`);
  r.gondola+=qtd; r.estoque-=qtd;
  r.movimentacoes=r.movimentacoes||[];
  r.movimentacoes.unshift({data:new Date().toISOString(),
    acao:`Reposição: ${qtd} un. → Gôndola`,gondola:r.gondola,estoque:r.estoque,por:USER.nome});
  lista[idx]=r; setData(lista); fecharModal('repor-modal');
  const payload={evento:'atualizacao_estoque',sku:r.ref,nome:r.nome,tipo:r.tipo,
    estoque_gondola:r.gondola,estoque_deposito:r.estoque,
    estoque_total:r.gondola+r.estoque,
    movimentacao:`${qtd} un. → gôndola`,atualizado_por:USER.nome,data:new Date().toISOString()};
  const ok=await enviarWebhook(payload);
  if(ok){
    const l2=getData(); const idx2=l2.findIndex(x=>x.id===r.id);
    if(idx2>=0){l2[idx2].sincronizado=true;l2[idx2].ultimaSync=new Date().toISOString();setData(l2);}
    adicionarLog('ok',`✅ [${r.ref}] Reposição ${qtd} un. sincronizada`);
    toast(`✅ ${qtd} un. movidas e sincronizadas!`);
  } else { toast(`✅ ${qtd} un. movidas para a gôndola!`); }
  atualizar();
}

// ══════════ EDITAR PRODUTO ══════════
function abrirEdit(id){
  const r=getData().find(x=>x.id===id); if(!r) return;
  document.getElementById('edit-id').value=id;
  document.getElementById('edit-nome').value=r.nome||'';
  document.getElementById('edit-ref').value=r.ref||'';
  document.getElementById('edit-tipo').value=r.tipo||'Outro';
  document.getElementById('edit-forn').value=r.forn||'';
  document.getElementById('edit-custo').value=r.custo||0;
  document.getElementById('edit-preco').value=r.preco||0;
  document.getElementById('edit-gondola').value=r.gondola||0;
  document.getElementById('edit-estoque').value=r.estoque||0;
  document.getElementById('edit-alerta').value=r.alerta||5;
  document.getElementById('edit-obs').value=r.obs||'';
  abrirModal('edit-modal');
}
function salvarEdit(){
  const id=parseInt(document.getElementById('edit-id').value);
  const lista=getData(); const idx=lista.findIndex(x=>x.id===id); if(idx<0) return;
  lista[idx]={...lista[idx],
    nome:document.getElementById('edit-nome').value.trim(),
    ref:document.getElementById('edit-ref').value.trim(),
    tipo:document.getElementById('edit-tipo').value,
    forn:document.getElementById('edit-forn').value.trim(),
    custo:parseFloat(document.getElementById('edit-custo').value)||0,
    preco:parseFloat(document.getElementById('edit-preco').value)||0,
    gondola:parseInt(document.getElementById('edit-gondola').value)||0,
    estoque:parseInt(document.getElementById('edit-estoque').value)||0,
    alerta:parseInt(document.getElementById('edit-alerta').value)||5,
    obs:document.getElementById('edit-obs').value.trim(),
    sincronizado:false};
  setData(lista); fecharModal('edit-modal'); atualizar(); toast('✅ Produto atualizado!');
}
function excluirProduto(id){
  if(!confirm('Excluir este produto?')) return;
  setData(getData().filter(x=>x.id!==id)); atualizar(); toast('🗑️ Produto excluído.');
}

// ══════════ RENDER CHECK-IN ══════════
function renderCheckin(){
  const tipo=document.getElementById('ft-tipo').value;
  const busca=document.getElementById('ft-busca').value.toLowerCase();
  let lista=getData();
  if(tipo) lista=lista.filter(x=>x.tipo===tipo);
  if(busca) lista=lista.filter(x=>x.nome.toLowerCase().includes(busca)||x.ref.toLowerCase().includes(busca));
  const el=document.getElementById('hist-checkin');
  if(!lista.length){el.innerHTML='<div class="empty"><div class="icon">📦</div><p>Nenhum registro encontrado.</p></div>';return;}
  el.innerHTML=lista.map(r=>`
    <div class="entry ${(r.gondola+r.estoque)<r.alerta?'low':''} ${r.sincronizado?'synced':''}">
      ${r.foto?`<img src="${r.foto}" alt=""/>`:`<div class="no-img">💍</div>`}
      <div class="entry-info">
        <h3>${r.nome}</h3>
        <div class="ref">${r.ref}</div>
        <div class="meta">${r.forn?'🏭 '+r.forn+' &nbsp;':''}<span class="tipo-badge tipo-${r.tipo}">${r.tipo}</span></div>
        <div class="pills">
          <span class="pill pill-rose">🛒 Gôndola: ${r.gondola}</span>
          <span class="pill pill-blue">📦 Estoque: ${r.estoque}</span>
          <span class="pill pill-gold">💰 ${moeda(r.preco)}</span>
          ${r.sincronizado?'<span class="pill pill-green">☁️ Sync</span>':''}
        </div>
        ${r.obs?`<div class="obs">📝 ${r.obs}</div>`:''}
        <div class="reg-por">👤 ${r.por} · ${fmtData(r.data)}</div>
      </div>
      <div class="entry-actions">
        <div class="entry-date">${fmtData(r.data)}</div>
        <button class="btn-sm btn-warning" onclick="abrirRepor(${r.id})">🔄 Repor</button>
        ${USER&&USER.isAdmin?`<button class="btn-sm btn-info" onclick="abrirEdit(${r.id})">✏️</button>
        <button class="btn-sm btn-danger" onclick="excluirProduto(${r.id})">🗑️</button>`:''}
      </div>
    </div>`).join('');
}

// ══════════ RENDER ESTOQUE ══════════
function renderEstoque(){
  const tipo=document.getElementById('fe-tipo').value;
  const alertaF=document.getElementById('fe-alerta').value;
  const busca=document.getElementById('fe-busca').value.toLowerCase();
  let lista=getData();
  if(tipo) lista=lista.filter(x=>x.tipo===tipo);
  if(alertaF==='low') lista=lista.filter(x=>(x.gondola+x.estoque)<x.alerta);
  if(alertaF==='ok')  lista=lista.filter(x=>(x.gondola+x.estoque)>=x.alerta);
  if(busca) lista=lista.filter(x=>x.nome.toLowerCase().includes(busca)||x.ref.toLowerCase().includes(busca));
  const el=document.getElementById('hist-estoque');
  if(!lista.length){el.innerHTML='<div class="empty"><div class="icon">🗄️</div><p>Nenhum produto encontrado.</p></div>';return;}
  el.innerHTML=lista.map(r=>{
    const total=r.gondola+r.estoque, low=total<r.alerta;
    return `<div class="entry ${low?'low':''} ${r.sincronizado?'synced':''}">
      ${r.foto?`<img src="${r.foto}" alt=""/>`:`<div class="no-img">💍</div>`}
      <div class="entry-info">
        <h3>${r.nome} <span class="tipo-badge tipo-${r.tipo}">${r.tipo}</span></h3>
        <div class="ref">${r.ref}</div>
        <div class="pills">
          <span class="pill pill-rose">🛒 ${r.gondola}</span>
          <span class="pill pill-blue">📦 ${r.estoque}</span>
          <span class="pill pill-gold">∑ ${total}</span>
          ${low?'<span class="pill pill-orange">⚠️ Baixo</span>':''}
          ${r.sincronizado?'<span class="pill pill-green">☁️ Sync</span>':''}
        </div>
        <div class="meta">Custo: ${moeda(r.custo)} | Venda: ${moeda(r.preco)}</div>
      </div>
      <div class="entry-actions">
        <button class="btn-sm btn-warning" onclick="abrirRepor(${r.id})">🔄 Repor</button>
        ${USER&&USER.isAdmin?`<button class="btn-sm btn-info" onclick="abrirEdit(${r.id})">✏️</button>`:''}
      </div>
    </div>`;
  }).join('');
}

// ══════════ STATS ══════════
function renderStats(){
  const lista=getData();
  const total=lista.length;
  const totalItens=lista.reduce((a,r)=>a+r.gondola+r.estoque,0);
  const baixo=lista.filter(r=>(r.gondola+r.estoque)<r.alerta).length;
  const synced=lista.filter(r=>r.sincronizado).length;
  const clientes=getClientes().length;
  const clube=getClientes().filter(c=>c.clube).length;
  const vendas=getVendas();
  const totalVendas=vendas.reduce((a,v)=>a+v.total,0);
  const s1=document.getElementById('stats-checkin');
  const s2=document.getElementById('stats-estoque');
  const sc=document.getElementById('stats-clientes');
  const sf=document.getElementById('stats-fornecedores');
  const html=`
    <div class="stat-box"><div class="num">${total}</div><div class="lbl">Produtos</div></div>
    <div class="stat-box blue"><div class="num">${totalItens}</div><div class="lbl">Itens</div></div>
    <div class="stat-box warn"><div class="num">${baixo}</div><div class="lbl">Baixo Estoque</div></div>
    <div class="stat-box ok"><div class="num">${synced}</div><div class="lbl">Sincronizados</div></div>`;
  if(s1) s1.innerHTML=html;
  if(s2) s2.innerHTML=html;
  if(sc) sc.innerHTML=`
    <div class="stat-box"><div class="num">${clientes}</div><div class="lbl">Clientes</div></div>
    <div class="stat-box gold"><div class="num">${clube}</div><div class="lbl">Clube</div></div>
    <div class="stat-box ok"><div class="num">${moeda(totalVendas)}</div><div class="lbl">Total Vendas</div></div>`;
  if(sf) sf.innerHTML=`
    <div class="stat-box blue"><div class="num">${getForn().length}</div><div class="lbl">Fornecedores</div></div>`;
}

function renderAlertas(){
  const lista=getData();
  const baixo=lista.filter(r=>(r.gondola+r.estoque)<r.alerta);
  const html=baixo.length?`<div class="alerta-box">
    <strong>⚠️ ${baixo.length} produto(s) com estoque baixo:</strong>
    ${baixo.map(r=>`<div class="alerta-item">• ${r.nome} (${r.ref}) — Total: ${r.gondola+r.estoque} / Alerta: ${r.alerta}</div>`).join('')}
  </div>`:'';
  const a1=document.getElementById('alertas-top');
  const a2=document.getElementById('alertas-estoque');
  if(a1) a1.innerHTML=html;
  if(a2) a2.innerHTML=html;
}

// ══════════ CLIENTES ══════════
function cadastrarCliente(){
  const nome=document.getElementById('cl-nome').value.trim();
  const tel=document.getElementById('cl-tel').value.trim();
  if(!nome||!tel) return toast('⚠️ Nome e WhatsApp são obrigatórios.');
  const novo={id:Date.now(),nome,tel,
    email:document.getElementById('cl-email').value.trim(),
    aniversario:document.getElementById('cl-aniv').value,
    cpf:document.getElementById('cl-cpf').value.trim(),
    endereco:document.getElementById('cl-end').value.trim(),
    cidade:document.getElementById('cl-cidade').value.trim(),
    origem:document.getElementById('cl-origem').value,
    obs:document.getElementById('cl-obs').value.trim(),
    clube:document.getElementById('cl-clube').checked,
    data:new Date().toISOString(),por:USER.nome,totalGasto:0,qtdCompras:0};
  const lista=getClientes(); lista.unshift(novo); setClientes(lista);
  ['cl-nome','cl-tel','cl-email','cl-cpf','cl-end','cl-cidade','cl-obs']
    .forEach(id=>document.getElementById(id).value='');
  document.getElementById('cl-origem').value='';
  document.getElementById('cl-clube').checked=false;
  toast('✅ Cliente cadastrado!'); renderClientes(); renderStats();
}
function renderClientes(){
  const clube=document.getElementById('fcl-clube').value;
  const busca=document.getElementById('fcl-busca').value.toLowerCase();
  let lista=getClientes();
  if(clube==='sim') lista=lista.filter(c=>c.clube);
  if(clube==='nao') lista=lista.filter(c=>!c.clube);
  if(busca) lista=lista.filter(c=>c.nome.toLowerCase().includes(busca)||c.tel.includes(busca));
  const el=document.getElementById('hist-clientes');
  if(!lista.length){el.innerHTML='<div class="empty"><div class="icon">👥</div><p>Nenhum cliente encontrado.</p></div>';return;}
  el.innerHTML=lista.map(c=>`
    <div class="cliente-card">
      <div class="avatar">${c.nome.charAt(0).toUpperCase()}</div>
      <div class="cliente-info">
        <h3>${c.nome} ${c.clube?'<span class="clube-tag">💎 Clube</span>':''}</h3>
        <div class="ci-meta">📱 ${c.tel} ${c.email?'· 📧 '+c.email:''}</div>
        <div class="ci-meta">${c.cidade?'📍 '+c.cidade:''} ${c.origem?'· '+c.origem:''}</div>
        <div class="ci-meta">🛒 ${c.qtdCompras||0} compras · ${moeda(c.totalGasto||0)}</div>
        ${c.aniversario?`<div class="ci-meta">🎂 ${fmtData(c.aniversario)}</div>`:''}
      </div>
      <div class="entry-actions">
        <div class="entry-date">${fmtData(c.data)}</div>
        <a href="https://wa.me/55${c.tel.replace(/\D/g,'')}" target="_blank"
          class="btn-sm btn-success">💬 WhatsApp</a>
        ${USER&&USER.isAdmin?`<button class="btn-sm btn-info" onclick="abrirEditCliente(${c.id})">✏️</button>
        <button class="btn-sm btn-danger" onclick="excluirCliente(${c.id})">🗑️</button>`:''}
      </div>
    </div>`).join('');
}
function abrirEditCliente(id){
  const c=getClientes().find(x=>x.id===id); if(!c) return;
  document.getElementById('ecl-id').value=id;
  document.getElementById('ecl-nome').value=c.nome||'';
  document.getElementById('ecl-tel').value=c.tel||'';
  document.getElementById('ecl-email').value=c.email||'';
  document.getElementById('ecl-aniv').value=c.aniversario||'';
  document.getElementById('ecl-cpf').value=c.cpf||'';
  document.getElementById('ecl-end').value=c.endereco||'';
  document.getElementById('ecl-cidade').value=c.cidade||'';
  document.getElementById('ecl-origem').value=c.origem||'';
  document.getElementById('ecl-obs').value=c.obs||'';
  document.getElementById('ecl-clube').checked=c.clube||false;
  abrirModal('edit-cliente-modal');
}
function salvarEditCliente(){
  const id=parseInt(document.getElementById('ecl-id').value);
  const lista=getClientes(); const idx=lista.findIndex(x=>x.id===id); if(idx<0) return;
  lista[idx]={...lista[idx],
    nome:document.getElementById('ecl-nome').value.trim(),
    tel:document.getElementById('ecl-tel').value.trim(),
    email:document.getElementById('ecl-email').value.trim(),
    aniversario:document.getElementById('ecl-aniv').value,
    cpf:document.getElementById('ecl-cpf').value.trim(),
    endereco:document.getElementById('ecl-end').value.trim(),
    cidade:document.getElementById('ecl-cidade').value.trim(),
    origem:document.getElementById('ecl-origem').value,
    obs:document.getElementById('ecl-obs').value.trim(),
    clube:document.getElementById('ecl-clube').checked};
  setClientes(lista); fecharModal('edit-cliente-modal'); renderClientes(); toast('✅ Cliente atualizado!');
}
function excluirCliente(id){
  if(!confirm('Excluir este cliente?')) return;
  setClientes(getClientes().filter(x=>x.id!==id)); renderClientes(); renderStats(); toast('🗑️ Cliente excluído.');
}

// ══════════ FORNECEDORES ══════════
function cadastrarFornecedor(){
  const nome=document.getElementById('fn-nome').value.trim();
  if(!nome) return toast('⚠️ Informe o nome do fornecedor.');
  const novo={id:Date.now(),nome,
    tel:document.getElementById('fn-tel').value.trim(),
    email:document.getElementById('fn-email').value.trim(),
    cnpj:document.getElementById('fn-cnpj').value.trim(),
    cidade:document.getElementById('fn-cidade').value.trim(),
    categorias:document.getElementById('fn-cats').value.trim(),
    prazo:document.getElementById('fn-prazo').value.trim(),
    minimo:parseFloat(document.getElementById('fn-minimo').value)||0,
    pgto:document.getElementById('fn-pgto').value.trim(),
    obs:document.getElementById('fn-obs').value.trim(),
    data:new Date().toISOString(),por:USER.nome};
  const lista=getForn(); lista.unshift(novo); setForn(lista);
  ['fn-nome','fn-tel','fn-email','fn-cnpj','fn-cidade','fn-cats','fn-prazo','fn-minimo','fn-pgto','fn-obs']
    .forEach(id=>document.getElementById(id).value='');
  toast('✅ Fornecedor cadastrado!'); renderFornecedores(); renderStats();
}
function renderFornecedores(){
  const busca=document.getElementById('ffn-busca').value.toLowerCase();
  let lista=getForn();
  if(busca) lista=lista.filter(f=>f.nome.toLowerCase().includes(busca)||f.cidade.toLowerCase().includes(busca));
  const el=document.getElementById('hist-fornecedores');
  if(!lista.length){el.innerHTML='<div class="empty"><div class="icon">🏭</div><p>Nenhum fornecedor cadastrado.</p></div>';return;}
  el.innerHTML=lista.map(f=>`
    <div class="forn-card">
      <div style="display:flex;justify-content:space-between;align-items:start;flex-wrap:wrap;gap:8px;">
        <div>
          <h3 style="font-size:13px;font-weight:700;margin-bottom:3px;">🏭 ${f.nome}</h3>
          <div style="font-size:11px;color:var(--muted);">
            ${f.tel?'📱 '+f.tel+' &nbsp;':''}${f.email?'📧 '+f.email:''}
          </div>
          <div style="font-size:11px;color:var(--muted);">
            ${f.cidade?'📍 '+f.cidade+' &nbsp;':''}${f.cnpj?'CNPJ: '+f.cnpj:''}
          </div>
          <div class="pills" style="margin-top:5px;">
            ${f.categorias?`<span class="pill pill-blue">${f.categorias}</span>`:''}
            ${f.prazo?`<span class="pill pill-rose">⏱️ ${f.prazo}</span>`:''}
            ${f.minimo?`<span class="pill pill-gold">Mín: ${moeda(f.minimo)}</span>`:''}
            ${f.pgto?`<span class="pill pill-green">${f.pgto}</span>`:''}
          </div>
          ${f.obs?`<div style="font-size:11px;color:var(--brown);margin-top:4px;font-style:italic;">📝 ${f.obs}</div>`:''}
        </div>
        <div style="display:flex;flex-direction:column;gap:5px;align-items:flex-end;">
          <div style="font-size:10px;color:#bbb;">${fmtData(f.data)}</div>
          ${f.tel?`<a href="https://wa.me/55${f.tel.replace(/\D/g,'')}" target="_blank"
            class="btn-sm btn-success">💬 WhatsApp</a>`:''}
          ${USER&&USER.isAdmin?`<button class="btn-sm btn-danger" onclick="excluirFornecedor(${f.id})">🗑️</button>`:''}
        </div>
      </div>
    </div>`).join('');
}
function excluirFornecedor(id){
  if(!confirm('Excluir este fornecedor?')) return;
  setForn(getForn().filter(x=>x.id!==id)); renderFornecedores(); renderStats(); toast('🗑️ Fornecedor excluído.');
}

// ══════════ FRENTE DE CAIXA ══════════
function carregarClientesCaixa(){
  const sel=document.getElementById('cx-cliente');
  if(!sel) return;
  const atual=sel.value;
  sel.innerHTML='<option value="">Consumidor final</option>';
  getClientes().forEach(c=>{
    const opt=document.createElement('option');
    opt.value=c.id; opt.textContent=c.nome+(c.clube?' 💎':'');
    if(c.id==atual) opt.selected=true;
    sel.appendChild(opt);
  });
}
function buscarProdutoCaixa(){
  const busca=document.getElementById('cx-busca-prod').value.toLowerCase();
  const res=document.getElementById('cx-search-results');
  if(busca.length<2){res.style.display='none';return;}
  const lista=getData().filter(p=>(p.gondola+p.estoque)>0&&
    (p.nome.toLowerCase().includes(busca)||p.ref.toLowerCase().includes(busca)));
  if(!lista.length){res.style.display='none';return;}
  res.style.display='block';
  res.innerHTML=lista.slice(0,8).map(p=>`
    <div class="search-item" onclick="adicionarCarrinho(${p.id})">
      <div>${p.nome} <span class="tipo-badge tipo-${p.tipo}">${p.tipo}</span></div>
      <div class="si-ref">${p.ref} · ${moeda(p.preco)} · Estoque: ${p.gondola+p.estoque}</div>
    </div>`).join('');
}
function adicionarCarrinho(id){
  const p=getData().find(x=>x.id===id); if(!p) return;
  document.getElementById('cx-busca-prod').value='';
  document.getElementById('cx-search-results').style.display='none';
  const idx=carrinho.findIndex(x=>x.id===id);
  if(idx>=0){
    const max=p.gondola+p.estoque;
    if(carrinho[idx].qty>=max) return toast('⚠️ Estoque insuficiente!');
    carrinho[idx].qty++;
  } else {
    carrinho.push({id:p.id,nome:p.nome,ref:p.ref,preco:p.preco,qty:1,custo:p.custo||0});
  }
  renderCarrinho();
}
function renderCarrinho(){
  const el=document.getElementById('carrinho-items');
  if(!carrinho.length){
    el.innerHTML='<div class="empty" style="padding:24px;"><div style="font-size:30px;">🛍️</div><p>Nenhum item</p></div>';
    calcTotal(); return;
  }
  el.innerHTML=carrinho.map((item,i)=>`
    <div class="cart-item">
      <div class="ci-nome">${item.nome}<br><span style="font-size:10px;color:var(--muted);">${item.ref}</span></div>
      <div class="ci-qty">
        <button onclick="alterarQty(${i},-1)">−</button>
        <span>${item.qty}</span>
        <button onclick="alterarQty(${i},1)">+</button>
      </div>
      <div class="ci-preco">${moeda(item.preco*item.qty)}</div>
      <div class="ci-del" onclick="removerCarrinho(${i})">✕</div>
    </div>`).join('');
  calcTotal();
}
function alterarQty(i,delta){
  carrinho[i].qty+=delta;
  if(carrinho[i].qty<=0) carrinho.splice(i,1);
  renderCarrinho();
}
function removerCarrinho(i){carrinho.splice(i,1);renderCarrinho();}
function limparCarrinho(){carrinho=[];renderCarrinho();}
function calcTotal(){
  const sub=carrinho.reduce((a,x)=>a+x.preco*x.qty,0);
  const desc=parseFloat(document.getElementById('cx-desconto').value)||0;
  const total=Math.max(0,sub-desc);
  document.getElementById('cx-subtotal').textContent=moeda(sub);
  document.getElementById('cx-total').textContent=moeda(total);
}
function setPgto(btn,forma){
  document.querySelectorAll('.pgto-btn').forEach(b=>b.classList.remove('active'));
  btn.classList.add('active');
  pgtoAtual=forma;
}
async function finalizarVenda(){
  if(!carrinho.length) return toast('⚠️ Carrinho vazio!');
  const sub=carrinho.reduce((a,x)=>a+x.preco*x.qty,0);
  const desc=parseFloat(document.getElementById('cx-desconto').value)||0;
  const total=Math.max(0,sub-desc);
  const clienteId=document.getElementById('cx-cliente').value;
  const clienteNome=clienteId?
    (getClientes().find(c=>c.id==clienteId)||{nome:'Consumidor final'}).nome:
    'Consumidor final';
  const venda={id:Date.now(),data:new Date().toISOString(),
    itens:[...carrinho],subtotal:sub,desconto:desc,total,
    pagamento:pgtoAtual,clienteId,clienteNome,
    vendedor:document.getElementById('cx-vendedor').value,
    obs:document.getElementById('cx-obs-venda').value.trim()};
  // Baixar estoque
  const lista=getData();
  carrinho.forEach(item=>{
    const idx=lista.findIndex(x=>x.id===item.id); if(idx<0) return;
    const r=lista[idx];
    let q=item.qty;
    if(r.gondola>=q){r.gondola-=q;}
    else{q-=r.gondola;r.gondola=0;r.estoque=Math.max(0,r.estoque-q);}
    r.movimentacoes=r.movimentacoes||[];
    r.movimentacoes.unshift({data:new Date().toISOString(),
      acao:`Venda: ${item.qty} un.`,gondola:r.gondola,estoque:r.estoque,por:USER.nome});
    lista[idx]=r;
  });
  setData(lista);
  // Atualizar cliente
  if(clienteId){
    const cls=getClientes();
    const ci=cls.findIndex(c=>c.id==clienteId);
    if(ci>=0){cls[ci].totalGasto=(cls[ci].totalGasto||0)+total;
      cls[ci].qtdCompras=(cls[ci].qtdCompras||0)+1;setClientes(cls);}
  }
  const vendas=getVendas(); vendas.unshift(venda); setVendas(vendas);
  // Enviar para Make
  await enviarWebhook({evento:'venda',venda_id:venda.id,cliente:clienteNome,
    itens:carrinho.map(x=>({sku:x.ref,nome:x.nome,qty:x.qty,preco:x.preco})),
    total,pagamento:pgtoAtual,vendedor:venda.vendedor,data:venda.data});
  adicionarLog('ok',`✅ Venda #${venda.id} — ${clienteNome} — ${moeda(total)}`);
  limparCarrinho();
  document.getElementById('cx-desconto').value=0;
  document.getElementById('cx-obs-venda').value='';
  toast(`✅ Venda finalizada! Total: ${moeda(total)}`);
  renderVendas(); atualizar();
}
function renderVendas(){
  const data=document.getElementById('cv-data').value;
  const busca=document.getElementById('cv-busca').value.toLowerCase();
  let lista=getVendas();
  if(data) lista=lista.filter(v=>v.data.startsWith(data));
  if(busca) lista=lista.filter(v=>v.clienteNome.toLowerCase().includes(busca)||
    v.itens.some(i=>i.nome.toLowerCase().includes(busca)));
  const el=document.getElementById('hist-vendas');
  if(!lista.length){el.innerHTML='<div class="empty"><div class="icon">🛒</div><p>Nenhuma venda encontrada.</p></div>';return;}
  el.innerHTML=lista.map(v=>`
    <div class="venda-card" onclick="verVenda(${v.id})" style="cursor:pointer;">
      <div style="display:flex;justify-content:space-between;align-items:start;flex-wrap:wrap;gap:6px;">
        <div>
          <div style="font-size:13px;font-weight:700;">👤 ${v.clienteNome}</div>
          <div style="font-size:11px;color:var(--muted);">
            ${v.itens.length} item(s) · ${v.pagamento} · ${v.vendedor}
          </div>
          <div class="pills" style="margin-top:4px;">
            ${v.desconto>0?`<span class="pill pill-orange">Desc: ${moeda(v.desconto)}</span>`:''}
            <span class="pill pill-green">💰 ${moeda(v.total)}</span>
          </div>
        </div>
        <div style="font-size:10px;color:#bbb;">${fmtHora(v.data)}</div>
      </div>
    </div>`).join('');
}
function verVenda(id){
  const v=getVendas().find(x=>x.id===id); if(!v) return;
  document.getElementById('venda-detalhe-content').innerHTML=`
    <div style="font-size:13px;margin-bottom:10px;">
      <strong>Cliente:</strong> ${v.clienteNome}<br>
      <strong>Vendedor:</strong> ${v.vendedor}<br>
      <strong>Pagamento:</strong> ${v.pagamento}<br>
      <strong>Data:</strong> ${fmtHora(v.data)}
    </div>
    <table class="rel-table" style="margin-bottom:12px;">
      <thead><tr><th>Produto</th><th>Qtd</th><th>Unit</th><th>Total</th></tr></thead>
      <tbody>${v.itens.map(i=>`<tr><td>${i.nome}<br><span style="font-size:10px;color:var(--muted);">${i.ref}</span></td>
        <td>${i.qty}</td><td>${moeda(i.preco)}</td><td>${moeda(i.preco*i.qty)}</td></tr>`).join('')}</tbody>
    </table>
    <div style="text-align:right;font-size:13px;">
      Subtotal: ${moeda(v.subtotal)}<br>
      ${v.desconto>0?`Desconto: -${moeda(v.desconto)}<br>`:''}
      <strong>Total: ${moeda(v.total)}</strong>
    </div>
    ${v.obs?`<div style="margin-top:8px;font-size:12

        font-size:12px;color:var(--brown);font-style:italic;">📝 ${v.obs}</div>`:''}`;
  abrirModal('venda-modal');
}

// ══════════ DRE ══════════
function gerarDRE(){
  const mes=document.getElementById('dre-mes').value;
  if(!mes) return;
  const [ano,m]=mes.split('-');
  const inicio=new Date(ano,m-1,1);
  const fim=new Date(ano,m,0,23,59,59);
  const vendas=getVendas().filter(v=>{const d=new Date(v.data);return d>=inicio&&d<=fim;});
  const despesas=getDespesas().filter(d=>{const dt=new Date(d.data);return dt>=inicio&&dt<=fim;});
  const receita=vendas.reduce((a,v)=>a+v.total,0);
  const cmv=vendas.reduce((a,v)=>a+v.itens.reduce((b,i)=>b+(i.custo||0)*i.qty,0),0);
  const despFixas=despesas.filter(d=>d.categoria==='Fixo').reduce((a,d)=>a+d.valor,0);
  const despVar=despesas.filter(d=>d.categoria==='Variável').reduce((a,d)=>a+d.valor,0);
  const marketing=despesas.filter(d=>d.categoria==='Marketing').reduce((a,d)=>a+d.valor,0);
  const outras=despesas.filter(d=>!['Fixo','Variável','Marketing','CMV'].includes(d.categoria)).reduce((a,d)=>a+d.valor,0);
  const totalDesp=despFixas+despVar+marketing+outras;
  const lucroBruto=receita-cmv;
  const lucroLiquido=lucroBruto-totalDesp;
  const margem=receita>0?((lucroLiquido/receita)*100):0;
  const cards=document.getElementById('dre-cards');
  cards.innerHTML=`
    <div class="dre-card receita">
      <div class="dc-label">💰 Receita Bruta</div>
      <div class="dc-valor">${moeda(receita)}</div>
      <div class="dc-desc">${vendas.length} vendas no período</div>
    </div>
    <div class="dre-card custo">
      <div class="dc-label">📦 CMV</div>
      <div class="dc-valor">${moeda(cmv)}</div>
      <div class="dc-desc">Custo das mercadorias vendidas</div>
    </div>
    <div class="dre-card receita" style="border-top-color:#20c997;">
      <div class="dc-label">📈 Lucro Bruto</div>
      <div class="dc-valor" style="color:#20c997;">${moeda(lucroBruto)}</div>
      <div class="dc-desc">Receita − CMV</div>
    </div>
    <div class="dre-card despesa">
      <div class="dc-label">💸 Despesas Totais</div>
      <div class="dc-valor">${moeda(totalDesp)}</div>
      <div class="dc-desc">Fixas + Variáveis + Marketing</div>
    </div>
    <div class="dre-card lucro">
      <div class="dc-label">🏆 Lucro Líquido</div>
      <div class="dc-valor" style="color:${lucroLiquido>=0?'var(--rose-dark)':'#dc3545'};">
        ${moeda(lucroLiquido)}</div>
      <div class="dc-desc">${lucroLiquido>=0?'Resultado positivo ✅':'Resultado negativo ⚠️'}</div>
    </div>
    <div class="dre-card margem">
      <div class="dc-label">📊 Margem Líquida</div>
      <div class="dc-valor">${margem.toFixed(1)}%</div>
      <div class="dc-desc">Sobre a receita bruta</div>
    </div>`;
  const tbody=document.getElementById('dre-tbody');
  const linha=(desc,val,cls='',bold=false)=>`
    <tr class="${cls}">
      <td style="${bold?'font-weight:700;':''}">${desc}</td>
      <td style="${bold?'font-weight:700;':''}${val<0?'color:#dc3545;':val>0?'color:#28a745;':''}">${moeda(val)}</td>
      <td>${receita>0?((val/receita)*100).toFixed(1)+'%':'—'}</td>
    </tr>`;
  tbody.innerHTML=
    linha('(+) Receita Bruta',receita,'',true)+
    linha('(−) Custo das Mercadorias (CMV)',-cmv)+
    linha('(=) Lucro Bruto',lucroBruto,'total-row',true)+
    linha('(−) Despesas Fixas',-despFixas)+
    linha('(−) Despesas Variáveis',-despVar)+
    linha('(−) Marketing',-marketing)+
    linha('(−) Outras Despesas',-outras)+
    linha('(=) Lucro Líquido',lucroLiquido,'total-row',true);
}

function lancarDespesa(){
  const desc=document.getElementById('dp-desc').value.trim();
  const valor=parseFloat(document.getElementById('dp-valor').value)||0;
  const data=document.getElementById('dp-data').value;
  if(!desc) return toast('⚠️ Informe a descrição.');
  if(!valor) return toast('⚠️ Informe o valor.');
  if(!data)  return toast('⚠️ Informe a data.');
  const nova={id:Date.now(),desc,
    categoria:document.getElementById('dp-cat').value,
    valor,data,por:USER.nome,criado:new Date().toISOString()};
  const lista=getDespesas(); lista.unshift(nova); setDespesas(lista);
  document.getElementById('dp-desc').value='';
  document.getElementById('dp-valor').value='';
  toast('✅ Despesa lançada!'); renderDespesas(); gerarDRE();
}

function renderDespesas(){
  const lista=getDespesas().slice(0,30);
  const el=document.getElementById('hist-despesas');
  if(!lista.length){el.innerHTML='<div class="empty"><p>Nenhuma despesa lançada.</p></div>';return;}
  el.innerHTML=lista.map(d=>`
    <div style="display:flex;justify-content:space-between;align-items:center;
      padding:8px 0;border-bottom:1px solid #f5eef0;font-size:12px;">
      <div>
        <span style="font-weight:600;">${d.desc}</span>
        <span class="pill pill-rose" style="margin-left:6px;">${d.categoria}</span>
        <span style="color:var(--muted);margin-left:6px;">· ${fmtData(d.data)}</span>
      </div>
      <div style="display:flex;align-items:center;gap:8px;">
        <span style="font-weight:700;color:#dc3545;">${moeda(d.valor)}</span>
        ${USER&&USER.isAdmin?`<button class="btn-sm btn-danger" 
          onclick="excluirDespesa(${d.id})">🗑️</button>`:''}
      </div>
    </div>`).join('');
}

function excluirDespesa(id){
  if(!confirm('Excluir esta despesa?')) return;
  setDespesas(getDespesas().filter(x=>x.id!==id));
  renderDespesas(); gerarDRE(); toast('🗑️ Despesa excluída.');
}

// ══════════ SUGESTÕES ══════════
function gerarSugestoes(){
  const produtos=getData();
  const clientes=getClientes();
  const vendas=getVendas();
  const sugestoes=[];
  const hoje=new Date();

  // Estoque baixo
  const baixo=produtos.filter(p=>(p.gondola+p.estoque)<p.alerta);
  if(baixo.length>0){
    sugestoes.push({tipo:'urgente',prioridade:'Alta',icone:'⚠️',
      titulo:`${baixo.length} produto(s) com estoque crítico`,
      desc:`${baixo.map(p=>p.nome).slice(0,3).join(', ')}${baixo.length>3?' e outros...':''} estão abaixo do nível de alerta.`,
      acao:'Ver Estoque',onclick:"aba('estoque')"});
  }

  // Produtos sem preço de venda
  const semPreco=produtos.filter(p=>!p.preco||p.preco===0);
  if(semPreco.length>0){
    sugestoes.push({tipo:'atencao',prioridade:'Média',icone:'💰',
      titulo:`${semPreco.length} produto(s) sem preço de venda`,
      desc:'Produtos sem preço cadastrado não aparecem corretamente no caixa e nas vendas.',
      acao:'Ir para Estoque',onclick:"aba('estoque')"});
  }

  // Clientes sem compra recente
  const trintaDias=new Date(hoje); trintaDias.setDate(trintaDias.getDate()-30);
  const inativos=clientes.filter(c=>{
    if(!c.qtdCompras||c.qtdCompras===0) return false;
    const ultimaV=vendas.filter(v=>v.clienteId==c.id).sort((a,b)=>new Date(b.data)-new Date(a.data))[0];
    return ultimaV&&new Date(ultimaV.data)<trintaDias;
  });
  if(inativos.length>0){
    sugestoes.push({tipo:'atencao',prioridade:'Média',icone:'👥',
      titulo:`${inativos.length} cliente(s) sem compra há +30 dias`,
      desc:`${inativos.slice(0,2).map(c=>c.nome).join(', ')} podem precisar de um contato via WhatsApp.`,
      acao:'Ver Clientes',onclick:"aba('clientes')"});
  }

  // Aniversariantes do mês
  const mesAtual=hoje.getMonth()+1;
  const aniversariantes=clientes.filter(c=>{
    if(!c.aniversario) return false;
    const m=parseInt(c.aniversario.split('-')[1]);
    return m===mesAtual;
  });
  if(aniversariantes.length>0){
    sugestoes.push({tipo:'positivo',prioridade:'Info',icone:'🎂',
      titulo:`${aniversariantes.length} aniversariante(s) este mês!`,
      desc:`${aniversariantes.map(c=>c.nome).slice(0,3).join(', ')}. Que tal enviar uma mensagem especial?`,
      acao:'Ver Clientes',onclick:"aba('clientes')"});
  }

  // Produtos não sincronizados
  const naoSync=produtos.filter(p=>!p.sincronizado);
  if(naoSync.length>0&&localStorage.getItem('geor_webhook')){
    sugestoes.push({tipo:'info',prioridade:'Info',icone:'☁️',
      titulo:`${naoSync.length} produto(s) não sincronizados`,
      desc:'Estes produtos ainda não foram enviados para a Nuvemshop via Make.',
      acao:'Ir para Admin',onclick:"aba('admin')"});
  }

  // Clube de vantagens vazio
  const clube=clientes.filter(c=>c.clube);
  if(clientes.length>5&&clube.length===0){
    sugestoes.push({tipo:'info',prioridade:'Baixa',icone:'💎',
      titulo:'Nenhum cliente no Clube de Vantagens',
      desc:'Compartilhe o link do clube com suas clientes e aumente o engajamento.',
      acao:'Ver Clientes',onclick:"aba('clientes')"});
  }

  // Sem fornecedores
  if(getForn().length===0){
    sugestoes.push({tipo:'info',prioridade:'Baixa',icone:'🏭',
      titulo:'Nenhum fornecedor cadastrado',
      desc:'Cadastre seus fornecedores para facilitar o controle de compras e reposição.',
      acao:'Ir para Fornecedores',onclick:"aba('fornecedores')"});
  }

  // Sem vendas hoje
  const vendasHoje=vendas.filter(v=>v.data.startsWith(hoje.toISOString().slice(0,10)));
  if(vendasHoje.length===0&&produtos.length>0){
    sugestoes.push({tipo:'info',prioridade:'Info',icone:'🛒',
      titulo:'Nenhuma venda registrada hoje',
      desc:'Lembre-se de registrar todas as vendas no caixa para manter o DRE atualizado.',
      acao:'Abrir Caixa',onclick:"aba('caixa')"});
  }

  // Positivo: meta atingida
  const totalMes=vendas.filter(v=>v.data.slice(0,7)===hoje.toISOString().slice(0,7))
    .reduce((a,v)=>a+v.total,0);
  if(totalMes>1000){
    sugestoes.push({tipo:'positivo',prioridade:'Info',icone:'🏆',
      titulo:`${moeda(totalMes)} vendidos este mês!`,
      desc:'Ótimo desempenho! Continue acompanhando o DRE para garantir a lucratividade.',
      acao:'Ver DRE',onclick:"aba('dre')"});
  }

  const el=document.getElementById('sug-grid');
  if(!sugestoes.length){
    el.innerHTML=`<div class="empty">
      <div class="icon">✅</div>
      <p>Tudo em ordem! Nenhuma ação pendente no momento.</p>
    </div>`;
    return;
  }
  el.innerHTML=sugestoes.map(s=>`
    <div class="sug-card ${s.tipo}">
      <div class="sug-icon">${s.icone}</div>
      <div class="sug-prioridade prior-${s.prioridade==='Alta'?'alta':s.prioridade==='Média'?'media':s.prioridade==='Baixa'?'baixa':'info'}">
        ${s.prioridade}
      </div>
      <div class="sug-titulo">${s.titulo}</div>
      <div class="sug-desc">${s.desc}</div>
      <button class="sug-acao" onclick="${s.onclick}">${s.acao} →</button>
    </div>`).join('');
}

// ══════════ RELATÓRIO ══════════
function gerarRelatorio(){
  const ini=new Date(document.getElementById('r-inicio').value+'T00:00:00');
  const fim=new Date(document.getElementById('r-fim').value+'T23:59:59');
  const tipo=document.getElementById('r-tipo').value;
  let lista=getData().filter(r=>{
    const d=new Date(r.data);
    return d>=ini&&d<=fim&&(!tipo||r.tipo===tipo);
  });
  relFiltrado=lista;
  const total=lista.length;
  const totalItens=lista.reduce((a,r)=>a+r.gondola+r.estoque,0);
  const totalValor=lista.reduce((a,r)=>a+(r.preco||0)*(r.gondola+r.estoque),0);
  const tipoMaisFreq=lista.length?
    Object.entries(lista.reduce((a,r)=>{a[r.tipo]=(a[r.tipo]||0)+1;return a},{}))
      .sort((a,b)=>b[1]-a[1])[0][0]:'—';
  document.getElementById('rel-cards').innerHTML=`
    <div class="rel-card"><h4>Registros</h4><div class="big">${total}</div></div>
    <div class="rel-card"><h4>Itens em Estoque</h4><div class="big">${totalItens}</div></div>
    <div class="rel-card"><h4>Valor em Estoque</h4><div class="big" style="font-size:18px;">${moeda(totalValor)}</div></div>
    <div class="rel-card"><h4>Tipo mais registrado</h4><div class="big" style="font-size:18px;">${tipoMaisFreq}</div></div>`;
  document.getElementById('rel-tbody').innerHTML=lista.length?
    lista.map(r=>`<tr>
      <td>${fmtData(r.data)}</td>
      <td><code>${r.ref}</code></td>
      <td>${r.nome}</td>
      <td><span class="tipo-badge tipo-${r.tipo}">${r.tipo}</span></td>
      <td>${r.gondola}</td>
      <td>${r.estoque}</td>
      <td><strong>${r.gondola+r.estoque}</strong></td>
      <td>${r.por}</td>
    </tr>`).join(''):
    '<tr><td colspan="8" style="text-align:center;color:#ccc;">Nenhum registro no período</td></tr>';
}

// ══════════ ADMIN ══════════
function renderAdmin(){
  const busca=document.getElementById('fa-busca').value.toLowerCase();
  let lista=getData();
  if(busca) lista=lista.filter(r=>r.nome.toLowerCase().includes(busca)||r.ref.toLowerCase().includes(busca));
  const el=document.getElementById('hist-admin');
  if(!lista.length){el.innerHTML='<div class="empty"><p>Nenhum produto encontrado.</p></div>';return;}
  el.innerHTML=lista.map(r=>`
    <div class="entry">
      ${r.foto?`<img src="${r.foto}" alt=""/>`:`<div class="no-img">💍</div>`}
      <div class="entry-info">
        <h3>${r.nome} <span class="tipo-badge tipo-${r.tipo}">${r.tipo}</span></h3>
        <div class="ref">${r.ref}</div>
        <div class="pills">
          <span class="pill pill-rose">🛒 ${r.gondola}</span>
          <span class="pill pill-blue">📦 ${r.estoque}</span>
          <span class="pill pill-gold">💰 ${moeda(r.preco)}</span>
          ${r.sincronizado?'<span class="pill pill-green">☁️ Sync</span>':'<span class="pill pill-orange">⚠️ Não sync</span>'}
        </div>
      </div>
      <div class="entry-actions">
        <div class="entry-date">${fmtData(r.data)}</div>
        <button class="btn-sm btn-info" onclick="abrirEdit(${r.id})">✏️ Editar</button>
        <button class="btn-sm btn-danger" onclick="excluirProduto(${r.id})">🗑️ Excluir</button>
      </div>
    </div>`).join('');
}

// ══════════ EXPORTAR CSV ══════════
function exportarCSV(){
  const lista=getData();
  const header='Data,Código,Nome,Tipo,Fornecedor,Custo,Preço,Gôndola,Estoque,Total,Alerta,Por';
  const rows=lista.map(r=>[
    fmtData(r.data),r.ref,r.nome,r.tipo,r.forn||'',
    r.custo||0,r.preco||0,r.gondola,r.estoque,
    r.gondola+r.estoque,r.alerta,r.por
  ].join(','));
  download('geor_estoque.csv',[header,...rows].join('\n'));
}
function exportarRelCSV(){
  if(!relFiltrado.length) return toast('⚠️ Gere o relatório primeiro.');
  const header='Data,Código,Nome,Tipo,Gôndola,Estoque,Total,Por';
  const rows=relFiltrado.map(r=>[
    fmtData(r.data),r.ref,r.nome,r.tipo,r.gondola,r.estoque,r.gondola+r.estoque,r.por
  ].join(','));
  download('geor_relatorio.csv',[header,...rows].join('\n'));
}
function download(nome,conteudo){
  const a=document.createElement('a');
  a.href='data:text/csv;charset=utf-8,\uFEFF'+encodeURIComponent(conteudo);
  a.download=nome; a.click();
}

// ══════════ ATUALIZAR GERAL ══════════
function atualizar(){
  renderStats();
  renderAlertas();
  renderCheckin();
}

// ══════════ INIT ══════════
window.addEventListener('click',e=>{
  if(!e.target.closest('.produto-search'))
    document.getElementById('cx-search-results').style.display='none';
});
verificarClube();
</script>
</body>
</html>
