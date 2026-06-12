<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1,maximum-scale=1,user-scalable=no,viewport-fit=cover">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="SAO2">
<title>スマスロ SAO2 設定判別</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{height:100%;overscroll-behavior:none}
body{background:#070a12;color:#e0e0e0;font-family:-apple-system,BlinkMacSystemFont,'Hiragino Kaku Gothic ProN',sans-serif;font-size:14px;-webkit-font-smoothing:antialiased}
button{touch-action:manipulation;font-family:inherit;cursor:pointer;border:none;outline:none}
input[type=number]::-webkit-inner-spin-button,input[type=number]::-webkit-outer-spin-button{-webkit-appearance:none}
input[type=number]{-moz-appearance:textfield}

#W{max-width:520px;margin:0 auto;display:flex;flex-direction:column;height:100vh;height:100dvh;padding-top:env(safe-area-inset-top,0px)}

/* Header - SAO=ブルー/シアン系のSF基調 */
#hdr{background:rgba(10,14,24,.92);backdrop-filter:blur(20px);-webkit-backdrop-filter:blur(20px);padding:12px 14px 8px;border-bottom:1px solid rgba(56,189,248,.2);flex-shrink:0}
.hr{display:flex;align-items:center;justify-content:space-between}
.ht{font-size:16px;font-weight:900;background:linear-gradient(135deg,#38BDF8,#818CF8);-webkit-background-clip:text;-webkit-text-fill-color:transparent;letter-spacing:.5px}
.hs{font-size:10px;color:rgba(255,255,255,.35);margin-top:2px}
.hb{padding:5px 12px;border-radius:8px;font-size:11px;font-weight:700;background:rgba(255,100,100,.08);border:1px solid rgba(255,100,100,.2);color:#ff8a80;backdrop-filter:blur(10px)}
.hb.p{background:rgba(255,50,50,.15);border-color:rgba(255,50,50,.4);color:#ff5252}
.cfm{margin-top:6px;padding:5px 10px;border-radius:8px;font-size:11px;font-weight:700;backdrop-filter:blur(10px)}

/* Quick stats */
.qs{display:flex;gap:5px;flex-wrap:wrap;padding:6px 14px;background:rgba(10,12,20,.95);border-bottom:1px solid rgba(255,255,255,.04);font-size:10px;flex-shrink:0}
.qc{background:rgba(255,255,255,.04);border-radius:8px;padding:4px 8px;border:1px solid rgba(255,255,255,.06)}
.ql{color:rgba(255,255,255,.3);margin-right:3px}.qv{color:#7dd3fc;font-weight:600}.qe{font-weight:700}
.qc.hl{background:rgba(129,140,248,.1);border-color:rgba(129,140,248,.3)}

/* Bottom tabs */
#tabs{display:flex;background:rgba(10,12,20,.95);backdrop-filter:blur(20px);-webkit-backdrop-filter:blur(20px);border-top:1px solid rgba(255,255,255,.06);flex-shrink:0;padding-bottom:env(safe-area-inset-bottom)}
.tb{flex:1;padding:8px 0 6px;text-align:center;font-size:8.5px;font-weight:600;color:rgba(255,255,255,.3);transition:color .15s}
.tb.a{color:#38BDF8}
.tb-ic{font-size:18px;display:block;margin-bottom:2px}

/* Scroll area */
#ct{flex:1;overflow-y:auto;-webkit-overflow-scrolling:touch;background:#070a12}

/* === Record tab === */
.inp{padding:12px 14px}
.ig{display:flex;gap:8px;margin-bottom:10px;align-items:center;flex-wrap:wrap}
.ig label{font-size:11px;color:rgba(255,255,255,.4);white-space:nowrap;font-weight:600}
.ig input{width:78px;height:36px;background:rgba(255,255,255,.05);border:1px solid rgba(255,255,255,.1);border-radius:10px;color:#a5d6a7;font-size:15px;font-weight:700;text-align:center;outline:none;font-family:monospace;transition:border-color .15s}
.ig input:focus{border-color:rgba(125,211,252,.5);background:rgba(255,255,255,.08)}
.tot{font-size:10px;color:rgba(255,255,255,.25)}

/* Event grid */
.eg{display:grid;grid-template-columns:repeat(4,1fr);gap:5px;margin-bottom:10px}
.eb{padding:10px 2px;border-radius:10px;font-size:11px;font-weight:700;text-align:center;line-height:1.2;transition:all .1s;border:1px solid transparent}
.eb:active{transform:scale(.95)}
.eb.s{border-color:#38BDF8;box-shadow:0 0 12px rgba(56,189,248,.25)}
.e-cz{background:rgba(56,189,248,.12);color:#38BDF8;border-color:rgba(56,189,248,.15)}
.e-kakcz{background:rgba(234,128,252,.14);color:#ea80fc;border-color:rgba(234,128,252,.2)}
.e-at{background:rgba(129,199,132,.12);color:#81c784;border-color:rgba(129,199,132,.15)}
.e-upat{background:rgba(255,179,0,.14);color:#FFB300;border-color:rgba(255,179,0,.2)}
.e-kouya{background:rgba(255,138,101,.12);color:#ff8a65;border-color:rgba(255,138,101,.15)}
.e-bnend{background:rgba(255,255,255,.04);color:rgba(255,255,255,.5);border-color:rgba(255,255,255,.06)}
.e-other{background:rgba(255,255,255,.03);color:rgba(255,255,255,.4);border-color:rgba(255,255,255,.05)}

/* Detail inputs */
.dt{margin-bottom:8px}
.dt-t{font-size:10px;color:rgba(255,255,255,.35);margin-bottom:4px;font-weight:600}
.dt-r{display:flex;gap:4px;flex-wrap:wrap}
.dt-b{padding:6px 10px;border-radius:8px;font-size:11px;font-weight:700;background:rgba(255,255,255,.04);border:1px solid rgba(255,255,255,.08);color:rgba(255,255,255,.5);transition:all .1s}
.dt-b.s{border-color:rgba(56,189,248,.5);color:#38BDF8;background:rgba(56,189,248,.08)}
.dt-b:active{transform:scale(.96)}
.dt-f{width:100%;height:32px;background:rgba(255,255,255,.04);border:1px solid rgba(255,255,255,.08);border-radius:8px;color:#ccc;font-size:12px;padding:0 10px;outline:none;font-family:inherit;transition:border-color .15s}
.dt-f:focus{border-color:rgba(125,211,252,.4)}

.yr-wrap{margin:8px 0;padding:8px 10px;border-radius:10px;background:rgba(255,179,0,.06);border:1px solid rgba(255,179,0,.15)}
.yr-row{display:flex;align-items:center;gap:8px}
.yr-label{font-size:11px;color:#FFB300;font-weight:700;flex:1}
.yr-hint{font-size:9px;color:rgba(255,255,255,.3);margin-top:3px;line-height:1.5}
.yr-tog{width:44px;height:24px;border-radius:12px;background:rgba(255,255,255,.1);border:1px solid rgba(255,255,255,.15);position:relative;transition:all .15s;flex-shrink:0}
.yr-tog.on{background:rgba(255,179,0,.3);border-color:#FFB300}
.yr-knob{width:18px;height:18px;border-radius:9px;background:#888;position:absolute;top:2px;left:2px;transition:all .15s}
.yr-tog.on .yr-knob{left:22px;background:#FFB300}

.ab{width:100%;padding:14px;border-radius:12px;font-size:14px;font-weight:900;color:#fff;margin-top:6px;transition:all .1s}
.ab.ok{background:linear-gradient(135deg,#0284c7,#0369a1);box-shadow:0 4px 16px rgba(2,132,199,.3)}
.ab.no{background:rgba(255,255,255,.03);color:rgba(255,255,255,.2)}
.ab:active{transform:scale(.98)}
.rec-t{font-size:10px;color:rgba(255,255,255,.25);padding:8px 14px 4px;font-weight:600}

/* === Timeline table === */
.tbl{width:100%;border-collapse:collapse;font-size:11px}
.tbl th{background:rgba(56,189,248,.08);color:rgba(56,189,248,.8);padding:6px 8px;font-weight:700;text-align:center;position:sticky;top:0;z-index:2;backdrop-filter:blur(10px);border-bottom:1px solid rgba(56,189,248,.1)}
.tbl td{padding:7px 8px;border-bottom:1px solid rgba(255,255,255,.03);vertical-align:top}
.tbl .gm{text-align:center;font-family:monospace;font-weight:700;color:rgba(255,255,255,.45);white-space:nowrap}
.tbl .ev{text-align:center;font-weight:700}
.tbl .nt{color:rgba(255,255,255,.35);font-size:10px}
.tbl .del-c{text-align:center;width:28px}
.td-d{width:22px;height:22px;border-radius:6px;background:rgba(255,100,100,.06);border:1px solid rgba(255,100,100,.15);color:#ff8a80;font-size:11px;display:flex;align-items:center;justify-content:center}
.c-cz{color:#38BDF8}.c-kakcz{color:#ea80fc}.c-at{color:#81c784}.c-upat{color:#FFB300}
.c-kouya{color:#ff8a65}.c-bnend{color:rgba(255,255,255,.4)}.c-other{color:rgba(255,255,255,.4)}
.tl-mt{text-align:center;color:rgba(255,255,255,.15);padding:30px;font-size:13px}

/* === Counter tab === */
.cnt{padding:8px 14px}
.cs{margin-bottom:10px;border-radius:12px;border:1px solid rgba(255,255,255,.06);background:rgba(255,255,255,.02);overflow:hidden}
.cs-h{padding:10px 12px;background:rgba(255,255,255,.03);display:flex;align-items:center;justify-content:space-between;cursor:pointer;user-select:none}
.cs-h .t{font-size:13px;font-weight:700;color:rgba(56,189,248,.85)}
.cs-h .ar{font-size:10px;color:rgba(255,255,255,.2);transition:transform .15s}
.cs-b{padding:6px 10px 10px}
.ci{padding:6px 2px;border-bottom:1px solid rgba(255,255,255,.03);display:flex;align-items:center;justify-content:space-between;gap:6px}
.ci-l{flex:1;min-width:0}.ci-n{font-size:12px;font-weight:600;color:rgba(255,255,255,.7)}
.ci-h{font-size:9px;color:#FFB300;background:rgba(255,179,0,.1);border-radius:4px;padding:1px 6px;display:inline-block;margin-top:2px;font-weight:700}
.ci-s{font-size:9px;color:rgba(255,255,255,.25);margin-top:1px}
.cw{display:flex;align-items:center;gap:4px}
.cm,.cp2{width:34px;height:34px;border-radius:8px;font-size:17px;font-weight:700;display:flex;align-items:center;justify-content:center;transition:transform .08s}
.cm{background:rgba(255,100,100,.08);border:1px solid rgba(255,100,100,.15);color:#ff8a80}
.cp2{background:rgba(100,255,100,.06);border:1px solid rgba(100,255,100,.12);color:#a5d6a7}
.cm:active,.cp2:active{transform:scale(.88)}
.vl{min-width:36px;height:34px;border-radius:8px;background:rgba(255,255,255,.04);border:1px solid rgba(255,255,255,.06);display:flex;align-items:center;justify-content:center;font-size:15px;font-weight:700;color:#e0f0fa;font-family:monospace;padding:0 4px}

.cc{margin-top:6px;padding:8px 10px;border-radius:10px;background:rgba(255,255,255,.02);border:1px solid rgba(255,255,255,.05);font-size:11px}
.cc-t{color:rgba(56,189,248,.8);font-weight:700;margin-bottom:3px;font-size:12px}
.cc-l{color:#7dd3fc;margin-top:2px}.cc-hl{color:#38BDF8;font-weight:700}
.cc-sub{color:rgba(255,255,255,.25);margin-top:2px;font-size:10px}

/* === レア役別CZ：状態タブUI ===== */
.pt-wrap{margin-bottom:10px;border-radius:12px;border:1px solid rgba(255,255,255,.06);background:rgba(255,255,255,.02);overflow:hidden}
.pt-header{padding:10px 12px;background:rgba(255,255,255,.03);display:flex;align-items:center;justify-content:space-between;cursor:pointer;user-select:none}
.pt-header .t{font-size:13px;font-weight:700;color:rgba(56,189,248,.85)}
.pt-header .ar{font-size:10px;color:rgba(255,255,255,.2)}
.pt-tabs{display:flex;gap:0;background:rgba(0,0,0,.3);border-bottom:1px solid rgba(255,255,255,.04)}
.pt-tab{flex:1;padding:9px 4px;text-align:center;font-size:12px;font-weight:700;color:rgba(255,255,255,.3);border-bottom:2px solid transparent;transition:all .15s}
.pt-tab.active{border-bottom-color:var(--tab-color,#38BDF8);color:var(--tab-color,#38BDF8)}
.pt-tab:active{opacity:.7}
.pt-body{padding:8px 12px 12px}

/* kakucz hero panel */
.haji-hero{margin-bottom:10px;border-radius:14px;overflow:hidden;border:1px solid rgba(234,128,252,.25);background:linear-gradient(135deg,rgba(234,128,252,.08),rgba(80,40,120,.04))}
.haji-hh{padding:10px 12px;display:flex;align-items:center;justify-content:space-between;cursor:pointer;user-select:none}
.haji-hh .t{font-size:13px;font-weight:800;color:#ea80fc}
.haji-hh .ar{font-size:10px;color:rgba(255,255,255,.2)}
.haji-body{padding:4px 12px 12px}
.haji-big{text-align:center;padding:10px 0 6px}
.haji-rate{font-size:30px;font-weight:900;font-family:monospace;line-height:1}
.haji-lab{font-size:10px;color:rgba(255,255,255,.4);margin-top:2px}
.haji-est{display:inline-block;margin-top:6px;padding:3px 12px;border-radius:8px;font-size:13px;font-weight:800}
.haji-cnt-row{display:flex;gap:8px;margin-top:8px}
.haji-cbox{flex:1;text-align:center;padding:8px 4px;border-radius:10px;background:rgba(255,255,255,.03);border:1px solid rgba(255,255,255,.06)}
.haji-cbox .n{font-size:9px;color:rgba(255,255,255,.4);font-weight:600}
.haji-cbox .v{font-size:22px;font-weight:800;font-family:monospace;color:#fff;margin-top:2px}
.haji-cnt-ctl{display:flex;align-items:center;justify-content:center;gap:6px;margin-top:6px}
.sbar{display:flex;align-items:center;gap:6px;margin-top:5px;font-size:10px}
.sbar-l{width:30px;font-weight:800;text-align:right}
.sbar-track{flex:1;height:14px;border-radius:7px;background:rgba(255,255,255,.04);overflow:hidden;position:relative}
.sbar-fill{height:100%;border-radius:7px;transition:width .3s}
.sbar-v{width:42px;font-family:monospace;font-weight:700;color:rgba(255,255,255,.55)}
.sbar.cur .sbar-l,.sbar.cur .sbar-v{color:#fff}
.sbar.cur .sbar-track{outline:1px solid rgba(255,255,255,.3)}

/* === info / guide tab === */
.info{padding:10px 14px 24px}
.isec{margin-bottom:12px;border-radius:12px;border:1px solid rgba(255,255,255,.06);background:rgba(255,255,255,.02);overflow:hidden}
.isec-h{padding:10px 12px;background:rgba(255,255,255,.03);display:flex;align-items:center;justify-content:space-between;cursor:pointer;user-select:none}
.isec-h .t{font-size:13px;font-weight:700;color:rgba(56,189,248,.85)}
.isec-h .ar{font-size:10px;color:rgba(255,255,255,.2)}
.isec-b{padding:8px 12px 12px}
.itbl{width:100%;border-collapse:collapse;font-size:11px;margin-top:4px}
.itbl th{background:rgba(56,189,248,.06);color:rgba(56,189,248,.7);padding:5px 6px;font-weight:700;text-align:left}
.itbl td{padding:5px 6px;border-top:1px solid rgba(255,255,255,.04);vertical-align:top;color:rgba(255,255,255,.6)}
.itbl td.v{text-align:right;white-space:nowrap;font-family:monospace;color:#7dd3fc;font-weight:700}
.ibadge{display:inline-block;font-size:10px;font-weight:800;padding:1px 7px;border-radius:5px;color:#070a12}
.inote{font-size:10px;color:rgba(255,255,255,.3);margin-top:6px;line-height:1.5}
.idot{display:inline-block;width:9px;height:9px;border-radius:50%;margin-right:4px;vertical-align:middle}
.cyc3{margin-top:6px;border-radius:10px;overflow:hidden;border:1px solid rgba(56,189,248,.12)}
.cyc3 table{width:100%;border-collapse:collapse;font-size:11px}
.cyc3 th{background:rgba(56,189,248,.1);color:rgba(56,189,248,.85);padding:5px 4px;font-weight:700}
.cyc3 td{padding:5px 4px;text-align:center;border-top:1px solid rgba(255,255,255,.04);font-family:monospace;font-weight:700}
.cyc3 tr.cur{background:rgba(56,189,248,.08)}

/* === Export tab === */
.exp{padding:14px}
.exp-h{font-size:12px;color:rgba(56,189,248,.7);font-weight:700;margin-bottom:6px}
.exp-ta{width:100%;min-height:300px;background:rgba(255,255,255,.03);border:1px solid rgba(255,255,255,.06);border-radius:12px;padding:12px;color:#b0d8d8;font-size:11px;font-family:monospace;white-space:pre-wrap;resize:none;outline:none;-webkit-user-select:all;user-select:all}
</style>
</head>
<body>
<div id="W"><div id="hdr"></div><div class="qs" id="qs"></div><div id="ct"></div><div id="tabs"></div></div>
<script>
/* ========================================================================
   スマスロ ソードアート・オンラインⅡ（SAO2）設定判別＆総合ツール
   パオン・ディーピー/大都技研・2026年6月8日導入

   ◆ 設計方針（ヨルムンガンドツールの構成を踏襲） ◆
   ・各要素を並べて表示。機械的な総合点は出さない。
   ・最大の設定差は「強チャンス目→確定CZ(THE END)当選率」（設1=0.4%→設6=5.1%）。
     ただし試行回数が非常に少ない（強チャンス目自体が約1/1057）ため、
     実用上のメイン軸は CZ確率・AT初当り・強チェリーCZ当選率・スイカSC当選率。
   ・CZ確率は通常時CZのみを母数に。確定CZ(THE END帯)は別カウント。
   ・各レア役のCZ/SC当選率を状態(通常/高確)タブで分けて記録。

   ◆ 解析データ（2026年・ちょんぼりすた/なな徹/p-world 3ソース照合済み） ◆
   CZ確率:  1=1/238.4 2=1/232.3 3=1/232.7 4=1/218.9 5=1/225.2 6=1/191.7
   AT確率:  1=1/386.2 2=1/364.3 3=1/368.1 4=1/326.8 5=1/340.6 6=1/269.6
   出玉率:  1=97.6% 2=98.8% 3=100.2% 4=105.3% 5=110.4% 6=114.9%
   ======================================================================== */

var SK="sao2_1";
var SC={1:"#78909C",2:"#42A5F5",3:"#66BB6A",4:"#FFA726",5:"#EF5350",6:"#AB47BC"};

/* 設定別 参考値 (1/x) */
var REF={
cz:{1:238.4,2:232.3,3:232.7,4:218.9,5:225.2,6:191.7},      /* CZ出現率 */
at:{1:386.2,2:364.3,3:368.1,4:326.8,5:340.6,6:269.6},      /* AT初当り */
kouya:{1:128.0,2:110.0,3:96.0,4:85.0,5:75.0,6:64.0}        /* CZ失敗時 曠野の決闘(推定補間/両端は判明値) */
};
/* 強チャンス目→確定CZ(THE END)当選率(%) — 最大の設定差 */
var KAKCZ={1:0.4,2:0.8,3:0.8,4:1.6,5:2.3,6:5.1};
/* CZ失敗時アイテム獲得率(%) */
var ITEM={1:20.3,2:21.1,3:21.9,4:22.7,5:25.0,6:30.1};
/* 通常中スイカ→シューティングチャージ当選率(%) */
var SUIKA_SC={1:40.2,2:44.5,3:41.0,4:48.4,5:42.2,6:55.1};
/* 出玉率(参考) */
var KAPPA={1:97.6,2:98.8,3:100.2,4:105.3,5:110.4,6:114.9};

/* 強チェリーCZ当選率(%) 状態別 */
var CHERRY_CZ={
normal:{1:20.0,2:21.0,3:20.0,4:25.0,5:20.0,6:33.0},
high:  {1:50.0,2:51.0,3:52.0,4:55.0,5:58.0,6:60.0}
};

/* イベント定義 */
var EVS=[
{id:"cz",l:"CZ(スコードロン)",c:"c-cz",cat:"cz"},
{id:"kakcz",l:"確定CZ(THE END)",c:"c-kakcz",cat:"cz"},
{id:"at",l:"AT初当り",c:"c-at",cat:"at"},
{id:"upat",l:"上位AT(フルダイブ)",c:"c-upat",cat:"upat"},
{id:"kouya",l:"曠野の決闘",c:"c-kouya",cat:"ep"},
{id:"bnend",l:"AT/上位AT終了",c:"c-bnend",cat:"bnend"},
{id:"other",l:"その他",c:"c-other",cat:"other"}
];
var EVBTNS=[
{id:"cz",l:"CZ",c:"e-cz"},
{id:"kakcz",l:"確定CZ",c:"e-kakcz"},
{id:"at",l:"AT初当り",c:"e-at"},
{id:"upat",l:"上位AT",c:"e-upat"},
{id:"kouya",l:"曠野の決闘",c:"e-kouya"},
{id:"bnend",l:"AT/上位終了",c:"e-bnend"},
{id:"other",l:"その他",c:"e-other"}
];

/* CZ突入契機（kakuteiは別イベントなのでここでは通常時の契機のみ） */
var CZ_KIND=[
{id:"gsuu",l:"液晶G数",denom:true},
{id:"bullet",l:"バレットCT",denom:true},
{id:"cherry",l:"強チェリー",denom:true},
{id:"other",l:"その他/不明",denom:true}
];
var CZ_RES=[{id:"s",l:"勝利"},{id:"f",l:"敗北"}];
/* CZ敗北時のアイテム獲得（高設定ほど獲得しやすい→設定差カウント用） */
var CZ_ITEM=[{id:"none",l:"獲得なし"},{id:"got",l:"アイテム獲得"}];
/* AT/上位AT終了画面 */
var END_SCR=[{id:"def",l:"通常/不明"},{id:"s5",l:"画面⑥(設5期待)"},{id:"other",l:"その他示唆"}];

/* レア役別CZ/SC当選率：状態タブ */
var RARE_ITEMS={
normal:[
{role:"cherry",nm:"強チェリー→CZ",ref:CHERRY_CZ.normal,c4:false,kind:"cz"},
{role:"suika",nm:"スイカ→シューティングチャージ",ref:SUIKA_SC,c4:false,kind:"sc"}
],
high:[
{role:"cherry",nm:"強チェリー→CZ",ref:CHERRY_CZ.high,c4:false,kind:"cz"}
]};
var RARE_KEYS=["cherryN_t","cherryN_w","suikaN_t","suikaN_w","cherryH_t","cherryH_w"];

/* カウンター（自力カウント系・入力頻度順） */
var CNTS=[
{id:"end",t:"🏁 AT/上位AT終了画面",items:[
{k:"endS5",l:"画面⑥",h:"設5期待",s:"設5が設6より出やすい",dot:"#EF5350"},
{k:"endOther",l:"その他の示唆あり画面",s:"内容調査中（記録のみ）",dot:"#90A4AE"}]},
{id:"trophy",t:"🏆 コパンダトロフィー（終了画面）",items:[
{k:"tCu",l:"銅",h:"設2↑",s:"設定2以上濃厚",dot:"#CD7F32"},
{k:"tSi",l:"銀",h:"設3↑",s:"設定3以上濃厚",dot:"#C0C0C0"},
{k:"tGo",l:"金",h:"設4↑",s:"設定4以上濃厚",dot:"#FFD700"},
{k:"tIna",l:"イナズマ",h:"設5↑",s:"設定5以上濃厚",dot:"#FF6347"},
{k:"tNiji",l:"虹",h:"設6",s:"設定6濃厚",dot:"#DA70D6"}]},
{id:"voice",t:"🔊 CZ/AT終了時ボイス（モード示唆）",items:[
{k:"vWhite",l:"白「信じてるから…」",s:"デフォルト",dot:"#E0E0E0"},
{k:"vBlue",l:"青「一緒に頑張ろ…ね」",s:"モード示唆",dot:"#42A5F5"},
{k:"vYellow",l:"黄「私とあたるまで…」",s:"モード示唆",dot:"#FBC02D"},
{k:"vGreen",l:"緑「キリト…強さの理由を…」",s:"モード示唆",dot:"#66BB6A"},
{k:"vRed",l:"赤「ヘカートⅡ…力を貸して」",s:"モード示唆",dot:"#EF5350"},
{k:"vPurple",l:"紫「LUKガン上げ…」",h:"モードUP",s:"モードアップ濃厚🔥",dot:"#AB47BC"}]}
];
var ALL_CC_KEYS=[];
CNTS.forEach(function(s){s.items.forEach(function(it){ALL_CC_KEYS.push(it.k)})});
RARE_KEYS.forEach(function(k){ALL_CC_KEYS.push(k)});

/* ===== 状態 ===== */
var CC={};
var LOG=[];
var COL={};
var infoCol={};
var guideCol={};
var TAB="rec";
var inAT=false;
var curEv=null,curG="",curRes=null,curCztrig=null,curScr=null,curNote="",curMai="",curCzitem=null;
var rareTab="normal";
var rstP=false,rstT=null;

function initC(){
ALL_CC_KEYS.forEach(function(k){CC[k]=0});
CNTS.forEach(function(s){COL[s.id]=false});
COL["rare"]=false;
COL["kakcz"]=false;
}

function load(){
initC();
try{var d=JSON.parse(localStorage.getItem(SK+"c"));if(d)for(var k in d)if(k in CC)CC[k]=d[k]}catch(e){}
try{LOG=JSON.parse(localStorage.getItem(SK+"l"))||[]}catch(e){LOG=[]}
inAT=false;
for(var i=LOG.length-1;i>=0;i-=1){
var ev=LOG[i].ev;
if(ev==="bnend"){inAT=false;break}
if(ev==="at"||ev==="upat"||ev==="kouya"){inAT=true;break}
}
}

function save(){try{
localStorage.setItem(SK+"c",JSON.stringify(CC));
localStorage.setItem(SK+"l",JSON.stringify(LOG));
}catch(e){}}

function estX(key,v){var r=REF[key];if(!r||!v||v===Infinity)return null;var c=1,m=Infinity;for(var s=1;s<=6;s++){var d=Math.abs(v-r[s]);if(d<m){m=d;c=s}}return c}
function estPct(table,v){if(v==null||isNaN(v))return null;var c=1,m=Infinity;for(var s=1;s<=6;s++){var d=Math.abs(v-table[s]);if(d<m){m=d;c=s}}return c}
function rate(n,d){return d?(n/d*100).toFixed(1):"0"}
function gev(id){for(var i=0;i<EVS.length;i++)if(EVS[i].id===id)return EVS[i];return null}
function esc(s){return String(s).replace(/&/g,"&amp;").replace(/</g,"&lt;").replace(/>/g,"&gt;").replace(/"/g,"&quot;").replace(/'/g,"&#39;")}

/* 総ゲーム数：AT/上位AT/曠野/bnendで区切り、bnendで確定加算 */
function totalG(){
var total=0,maxInInterval=0;
for(var i=0;i<LOG.length;i++){
var e=LOG[i],g=parseInt(e.g)||0;
if(e.ev==="bnend"){total=total+maxInInterval;maxInInterval=0;continue}
if(g>maxInInterval)maxInInterval=g}
total=total+maxInInterval;
return total}

/* 集計 */
function stats(){
var s={
cz:0,czNormal:0,czNormalS:0,czS:0,kakcz:0,
czGsuu:0,czBullet:0,czCherry:0,czOther:0,
czFail:0,czItemGot:0,
atFirst:0,upat:0,kouya:0
};
for(var i=0;i<LOG.length;i++){var e=LOG[i];
if(e.ev==="cz"){
s.cz=s.cz+1;s.czNormal=s.czNormal+1;
if(e.res==="s")s.czNormalS=s.czNormalS+1;
if(e.res==="s")s.czS=s.czS+1;
if(e.res==="f"){s.czFail=s.czFail+1;if(e.czitem==="got")s.czItemGot=s.czItemGot+1}
if(e.cztrig==="gsuu")s.czGsuu=s.czGsuu+1;
if(e.cztrig==="bullet")s.czBullet=s.czBullet+1;
if(e.cztrig==="cherry")s.czCherry=s.czCherry+1;
if(e.cztrig==="other")s.czOther=s.czOther+1;
}
if(e.ev==="kakcz")s.kakcz=s.kakcz+1;
if(e.ev==="at")s.atFirst=s.atFirst+1;
if(e.ev==="upat")s.upat=s.upat+1;
if(e.ev==="kouya")s.kouya=s.kouya+1;
}
return s}

/* 確定示唆からの最低設定 */
function cMin(){var m=0;
if(CC.tNiji)m=6;
else if(CC.tIna)m=Math.max(m,5);
else if(CC.tGo)m=Math.max(m,4);
else if(CC.tSi)m=Math.max(m,3);
else if(CC.tCu)m=Math.max(m,2);
return m}

function render(){rHdr();rQS();rTabs();
if(TAB==="rec")rRec();else if(TAB==="cnt")rCnt();else if(TAB==="tl")rTL();else if(TAB==="guide")rGuide();else if(TAB==="info")rInfo();else rExp()}

function rHdr(){
var h='<div class="hr"><div><div class="ht">スマスロ SAO2</div><div class="hs">'+(inAT?'【AT/上位AT中】':'通常時')+' / '+LOG.length+'件</div></div>';
h=h+'<button type="button" class="hb'+(rstP?' p':'')+'" id="bR">'+(rstP?'確定？':'リセット')+'</button></div>';
var cm=cMin();if(cm>0)h=h+'<div class="cfm" style="background:'+SC[cm]+'22;border:1px solid '+SC[cm]+';color:'+SC[cm]+'">🎯 設定'+cm+'以上濃厚</div>';
document.getElementById("hdr").innerHTML=h;
var b=document.getElementById("bR");if(b){b.addEventListener("click",function(e){e.preventDefault();doRst()})}}

function rQS(){
var s=stats(),tG=totalG(),h="";
h=h+'<div class="qc"><span class="ql">総G</span> <span class="qv">'+tG+'</span></div>';
/* CZ確率 */
if(tG>0&&s.czNormal>0){var v=tG/s.czNormal,e=estX("cz",v);h=h+'<div class="qc hl"><span class="ql">CZ</span> <span class="qv">1/'+v.toFixed(1)+'</span>'+(e?' <span class="qe" style="color:'+SC[e]+'">設'+e+'</span>':'')+'</div>'}
/* AT初当り */
if(tG>0&&s.atFirst>0){var v2=tG/s.atFirst,e2=estX("at",v2);h=h+'<div class="qc hl"><span class="ql">AT初当</span> <span class="qv">1/'+v2.toFixed(1)+'</span>'+(e2?' <span class="qe" style="color:'+SC[e2]+'">設'+e2+'</span>':'')+'</div>'}
/* 強チェリーCZ(高確) */
if(CC.cherryH_t>0){var cr=CC.cherryH_w/CC.cherryH_t*100,ec=estPct(CHERRY_CZ.high,cr);h=h+'<div class="qc"><span class="ql">強チェCZ(高)</span> <span class="qv">'+cr.toFixed(1)+'%</span>'+(ec?' <span class="qe" style="color:'+SC[ec]+'">設'+ec+'</span>':'')+'</div>'}
/* スイカSC */
if(CC.suikaN_t>0){var sr=CC.suikaN_w/CC.suikaN_t*100,es=estPct(SUIKA_SC,sr);h=h+'<div class="qc"><span class="ql">スイカSC</span> <span class="qv">'+sr.toFixed(1)+'%</span>'+(es?' <span class="qe" style="color:'+SC[es]+'">設'+es+'</span>':'')+'</div>'}
/* CZ失敗アイテム */
if(s.czFail>0){var ir=s.czItemGot/s.czFail*100,ei=estPct(ITEM,ir);h=h+'<div class="qc"><span class="ql">CZ失敗item</span> <span class="qv">'+ir.toFixed(1)+'%</span>'+(ei?' <span class="qe" style="color:'+SC[ei]+'">設'+ei+'</span>':'')+'</div>'}
document.getElementById("qs").innerHTML=h}

function rTabs(){
var ts=[{id:"rec",ic:"✏️",l:"記録"},{id:"cnt",ic:"🔢",l:"カウンター"},{id:"guide",ic:"🎯",l:"攻略"},{id:"tl",ic:"📋",l:"履歴"},{id:"info",ic:"📖",l:"示唆"},{id:"exp",ic:"📤",l:"出力"}];
var h="";for(var i=0;i<ts.length;i++)h=h+'<div class="tb'+(TAB===ts[i].id?' a':'')+'" data-tab="'+ts[i].id+'"><span class="tb-ic">'+ts[i].ic+'</span>'+ts[i].l+'</div>';
document.getElementById("tabs").innerHTML=h}

function rRec(){
var ct=document.getElementById("ct"),h='<div class="inp">';
h=h+'<div class="ig"><label>'+(inAT?'【AT/上位中】G数':'累計G（前回AT終了後から）')+'</label><input type="number" inputmode="numeric" id="iG" value="'+esc(curG)+'" placeholder="0">';
h=h+'<span class="tot">(総G: '+totalG()+')</span></div>';
h=h+'<div class="eg">';
for(var i=0;i<EVBTNS.length;i++){var eb=EVBTNS[i];
h=h+'<button type="button" class="eb '+eb.c+(curEv===eb.id?' s':'')+'" data-ev="'+eb.id+'">'+eb.l+'</button>'}
h=h+'</div>';
if(curEv){
var ev=gev(curEv);
if(curEv==="cz"){
h=h+'<div class="dt"><div class="dt-t">突入契機</div><div class="dt-r">';
for(var ik=0;ik<CZ_KIND.length;ik++){var ck=CZ_KIND[ik];h=h+'<button type="button" class="dt-b'+(curCztrig===ck.id?' s':'')+'" data-cztrig="'+ck.id+'">'+ck.l+'</button>'}
h=h+'</div><div class="yr-hint" style="margin-top:4px">CZ確率の母数。確定CZ（THE END帯スタート）は左の専用ボタンで別記録します。</div></div>';
h=h+'<div class="dt"><div class="dt-t">結果（勝利期待度 約55%）</div><div class="dt-r">';
for(var i2=0;i2<CZ_RES.length;i2++){var r=CZ_RES[i2];h=h+'<button type="button" class="dt-b'+(curRes===r.id?' s':'')+'" data-res="'+r.id+'">'+r.l+'</button>'}
h=h+'</div></div>';
if(curRes==="f"){
h=h+'<div class="dt"><div class="dt-t">敗北後のアイテム獲得（任意・設定差）</div><div class="dt-r">';
for(var ici=0;ici<CZ_ITEM.length;ici++){var czi=CZ_ITEM[ici];h=h+'<button type="button" class="dt-b'+(curCzitem===czi.id?' s':'')+'" data-czitem="'+czi.id+'">'+czi.l+'</button>'}
h=h+'</div><div class="yr-hint" style="margin-top:4px">CZ失敗の次Gでアイテム獲得することがあり、高設定ほど獲得率が高い（設1:20.3%→設6:30.1%）。</div></div>';
}
}
if(curEv==="kakcz"){
h=h+'<div class="yr-hint" style="margin:4px 0">確定CZ（THE END状態スタート）はAT濃厚。強チャンス目A/Bからの当選で大きな設定差（設1:0.4%→設6:5.1%）。CZ確率の母数とは別カウントです。</div>';
}
if(ev&&(ev.cat==="at"||ev.cat==="upat"||ev.cat==="ep")){
h=h+'<div class="dt"><div class="dt-t">獲得枚数（任意）</div><input type="number" inputmode="numeric" class="dt-f" id="iMai" value="'+esc(curMai)+'" placeholder="枚数"></div>'}
if(curEv==="bnend"){
h=h+'<div class="dt"><div class="dt-t">終了画面</div><div class="dt-r">';
for(var i4=0;i4<END_SCR.length;i4++){var scn=END_SCR[i4];h=h+'<button type="button" class="dt-b'+(curScr===scn.id?' s':'')+'" data-scr="'+scn.id+'">'+scn.l+'</button>'}
h=h+'</div></div>';
h=h+'<div class="dt"><div class="dt-t">トータル獲得枚数（任意）</div><input type="number" inputmode="numeric" class="dt-f" id="iMai" value="'+esc(curMai)+'" placeholder="枚数"></div>';
}
h=h+'<div class="dt"><input type="text" class="dt-f" id="iN" placeholder="メモ（任意）" value="'+esc(curNote)+'"></div>'}
var ok=!!curEv;
h=h+'<button type="button" class="ab '+(ok?'ok':'no')+'" data-a="add">'+(ok?'✓ 記録する':'↑ イベントを選択')+'</button></div>';
if(LOG.length>0){h=h+'<div class="rec-t">直近</div>';h=h+buildTable(Math.max(0,LOG.length-5),LOG.length,true)}
ct.innerHTML=h}

function buildNote(e){
var b=[];
if(e.res)b.push(e.res==="s"?"勝利":"敗北");
if(e.cztrig){var cl={gsuu:"液晶G数",bullet:"バレットCT",cherry:"強チェリー",other:"その他"};b.push(cl[e.cztrig]||esc(e.cztrig))}
if(e.czitem==="got")b.push("アイテム獲得");
if(e.scr){var sl={def:"通常",s5:"画面⑥(設5期待)",other:"示唆あり"};b.push("画面："+(sl[e.scr]||esc(e.scr)))}
if(e.mai)b.push(esc(e.mai)+"枚");
if(e.note)b.push(esc(e.note));
return b.join("　");
}

function buildTable(from,to,mini){
var h='<table class="tbl"><thead><tr><th style="width:60px">ゲーム数</th><th>当選</th><th>備考</th>'+(mini?'<th style="width:28px"></th>':'')+'</tr></thead><tbody>';
for(var i=from;i<to;i++){
var e=LOG[i],ev=gev(e.ev),g=esc(e.g||"0");
var gFmt;
if(e.ev==="at"||e.ev==="upat"||e.ev==="kouya"||e.ev==="bnend")gFmt='【'+g+'】';
else gFmt='('+g+')';
h=h+'<tr><td class="gm">'+gFmt+'</td>';
h=h+'<td class="ev '+(ev?ev.c:'')+'">'+(ev?ev.l:esc(e.ev))+'</td>';
h=h+'<td class="nt">'+buildNote(e)+'</td>';
if(mini)h=h+'<td class="del-c"><button type="button" class="td-d" data-del="'+i+'">×</button></td>';
h=h+'</tr>'}
h=h+'</tbody></table>';return h}

function rTL(){
var ct=document.getElementById("ct");
if(!LOG.length){ct.innerHTML='<div class="tl-mt">まだ記録がありません</div>';return}
ct.innerHTML=buildTable(0,LOG.length,true)}

/* === カウンタータブ === */
function rCnt(){
var ct=document.getElementById("ct"),tG=totalG(),h='<div class="cnt">';
h=h+buildRareSection();
for(var si=0;si<CNTS.length;si++)h=h+buildCntSection(CNTS[si],tG);
h=h+buildKakczSection();
h=h+'</div>';ct.innerHTML=h}

/* レア役別CZ/SC当選率：状態タブ */
function buildRareSection(){
var cl=COL["rare"];
var h='<div class="pt-wrap">';
h=h+'<div class="pt-header" data-tog="rare"><div class="t">🎯 レア役別 CZ/SC当選率（要カウント）</div><span class="ar">'+(cl?'▶':'▼')+'</span></div>';
if(!cl){
var tabs=[{id:"normal",l:"通常時",color:"#7dd3fc"},{id:"high",l:"高確中",color:"#FFB300"}];
h=h+'<div class="pt-tabs">';
for(var ti=0;ti<tabs.length;ti++){var td=tabs[ti];
h=h+'<div class="pt-tab'+(rareTab===td.id?' active':'')+'" style="--tab-color:'+td.color+'" data-raretab="'+td.id+'">'+td.l+'</div>';}
h=h+'</div>';
var items=RARE_ITEMS[rareTab]||[];
var stSuf=(rareTab==="normal")?"N":"H";
h=h+'<div class="pt-body">';
for(var ii=0;ii<items.length;ii++){var it=items[ii];
var tk=it.role+stSuf+"_t",wk=it.role+stSuf+"_w";
var t=CC[tk]||0,w=CC[wk]||0;
var pr=t>0?(w/t*100):null;
var e=pr!=null?estPct(it.ref,pr):null;
var lab=e?"設"+e:"";
var col=e?SC[e]:"#7dd3fc";
h=h+'<div style="padding:8px 0;border-bottom:1px solid rgba(255,255,255,.04)">';
h=h+'<div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:5px">';
h=h+'<div><span style="font-size:13px;font-weight:700;color:rgba(255,255,255,.85)">'+it.nm+'</span>';
if(pr!=null)h=h+' <span style="font-size:15px;font-weight:800;font-family:monospace;color:'+col+'">'+pr.toFixed(1)+'%</span>'+(lab?' <span style="font-size:10px;font-weight:700;color:'+col+'">'+lab+'</span>':'');
h=h+'</div></div>';
h=h+'<div style="display:flex;gap:6px">';
h=h+'<div style="flex:1;display:flex;align-items:center;justify-content:space-between;background:rgba(255,255,255,.03);border:1px solid rgba(255,255,255,.06);border-radius:8px;padding:4px 6px">';
h=h+'<span style="font-size:10px;color:rgba(255,255,255,.4);font-weight:600">試行</span>';
h=h+'<div style="display:flex;align-items:center;gap:3px"><button type="button" class="cm" data-cd="'+tk+'">−</button><div class="vl" style="min-width:30px">'+t+'</div><button type="button" class="cp2" data-ci="'+tk+'">＋</button></div></div>';
h=h+'<div style="flex:1;display:flex;align-items:center;justify-content:space-between;background:rgba(255,255,255,.03);border:1px solid rgba(255,255,255,.06);border-radius:8px;padding:4px 6px">';
h=h+'<span style="font-size:10px;color:rgba(255,255,255,.4);font-weight:600">'+(it.kind==="sc"?"当選":"当選")+'</span>';
h=h+'<div style="display:flex;align-items:center;gap:3px"><button type="button" class="cm" data-cd="'+wk+'">−</button><div class="vl" style="min-width:30px">'+w+'</div><button type="button" class="cp2" data-ci="'+wk+'">＋</button></div></div>';
h=h+'</div>';
h=h+'<div style="font-size:9px;color:rgba(255,255,255,.3);margin-top:4px;font-family:monospace">';
var refparts=[];for(var st=1;st<=6;st++)refparts.push('<span style="color:'+SC[st]+'">'+it.ref[st].toFixed(1)+'</span>');
h=h+'設1〜6: '+refparts.join(' / ')+'%';
h=h+'</div></div>';
}
if(rareTab==="normal"){
h=h+'<div class="cc" style="margin-top:8px"><div class="cc-sub">通常滞在時。強チェリーのCZ当選率は偶数かつ高設定で優遇（特に設6=33%が頭一つ抜ける）。スイカのシューティングチャージ当選率は設6=55%と高い。</div></div>';
}else{
h=h+'<div class="cc" style="margin-top:8px"><div class="cc-sub">高確滞在時。強チェリーのCZ当選率は設1=50%→設6=60%と段階的に優遇。高確は酒場/公園/SBCグロッケンなどのステージで示唆。</div></div>';
}
h=h+'</div>';
}
h=h+'</div>';
return h;
}

/* 確定CZ(THE END) ヒーローパネル */
function buildKakczSection(){
var s=stats();
var cl=COL["kakcz"];
var h='<div class="haji-hero"><div class="haji-hh" data-tog="kakcz"><div class="t">💜 確定CZ(THE END) 出現状況</div><span class="ar">'+(cl?'▶':'▼')+'</span></div>';
if(!cl){
h=h+'<div class="haji-body">';
h=h+'<div class="haji-big">';
h=h+'<div class="haji-rate" style="color:#ea80fc">'+s.kakcz+'<span style="font-size:14px">回</span></div>';
h=h+'<div class="haji-lab">確定CZ(THE END帯スタート)の累計</div>';
h=h+'</div>';
h=h+'<div style="margin-top:6px">';
h=h+'<div style="font-size:10px;color:rgba(255,255,255,.4);font-weight:700;margin-bottom:4px">強チャンス目→確定CZ 当選率（最大の設定差）</div>';
for(var st=1;st<=6;st++){var pct=KAKCZ[st];var w=(pct/KAKCZ[6]*100).toFixed(0);
h=h+'<div class="sbar"><div class="sbar-l" style="color:'+SC[st]+'">設'+st+'</div>';
h=h+'<div class="sbar-track"><div class="sbar-fill" style="width:'+w+'%;background:'+SC[st]+'99"></div></div>';
h=h+'<div class="sbar-v">'+pct.toFixed(1)+'%</div></div>';
}
h=h+'</div>';
h=h+'<div class="cc-sub" style="margin-top:8px">確定CZは設定差が最大（設1=0.4%→設6=5.1%）だが、強チャンス目自体が約1/1057と重く試行が貯まりにくい。出れば高設定の大きな手がかり。記録は左の「確定CZ」ボタンから。</div>';
h=h+'</div>';
}
h=h+'</div>';
return h;
}

function buildCntSection(sec,tG){
var cl=COL[sec.id];
var h='<div class="cs"><div class="cs-h" data-tog="'+sec.id+'"><div class="t">'+sec.t+'</div><span class="ar">'+(cl?'▶':'▼')+'</span></div>';
if(!cl){h=h+'<div class="cs-b">';
for(var ii=0;ii<sec.items.length;ii++){var it=sec.items[ii];
h=h+'<div class="ci"><div class="ci-l"><div class="ci-n">';
if(it.dot)h=h+'<span style="display:inline-block;width:8px;height:8px;border-radius:50%;background:'+it.dot+';margin-right:4px"></span>';
h=h+it.l+'</div>';if(it.h)h=h+'<div class="ci-h">'+it.h+'</div>';if(it.s)h=h+'<div class="ci-s">'+it.s+'</div>';
h=h+'</div><div class="cw"><button type="button" class="cm" data-cd="'+it.k+'">−</button><div class="vl">'+CC[it.k]+'</div><button type="button" class="cp2" data-ci="'+it.k+'">＋</button></div></div>'}
h=h+'</div>'}h=h+'</div>';
return h}

/* === 示唆タブ === */
var INFO=[
{id:"i_rates",t:"📈 設定別 主要確率（CZ/AT/出玉率）",custom:"rates",note:"AT初当りは設定差が大きい（設1=1/386→設6=1/270）。CZ確率は設6が頭一つ抜ける（1/191.7）が設3〜5は僅差。複数の要素を併せて判断。"},
{id:"i_kakcz",t:"💜 強チャンス目→確定CZ当選率（最大設定差）",rows:[
["設1","0.4%",1],["設2","0.8%",2],["設3","0.8%",3],
["設4","1.6%",4],["設5","2.3%",5],["設6","5.1%",6]
],note:"確定CZはTHE END状態からスタートしAT濃厚。強チャンス目A/B成立時の当選率に最大の設定差。ただし強チャンス目自体が約1/1057と重く、サンプルは貯まりにくい。"},
{id:"i_cherry",t:"🍒 強チェリー→CZ当選率",custom:"cherry",note:"通常滞在時は偶数かつ高設定で優遇（特に設6=33%）。高確滞在時は設1=50%→設6=60%と段階的に優遇。状態（ステージ）の見極めが前提になる。"},
{id:"i_suika",t:"🍉 通常中スイカ→シューティングチャージ当選率",rows:[
["設1","40.2%",1],["設2","44.5%",2],["設3","41.0%",3],
["設4","48.4%",4],["設5","42.2%",5],["設6","55.1%",6]
],note:"非高確中のスイカからのゲーム数加算ゾーン「シューティングチャージ」当選率。偶数設定（特に設6=55.1%）で優遇。比較的サンプルが貯まりやすい注目要素。"},
{id:"i_item",t:"🎁 CZ失敗時アイテム獲得率",rows:[
["設1","20.3%",1],["設2","21.1%",2],["設3","21.9%",3],
["設4","22.7%",4],["設5","25.0%",5],["設6","30.1%",6]
],note:"CZ失敗の次GでAT強化アイテムを獲得することがあり、高設定ほど獲得率が高い。設5・6で明確に上昇。CZ失敗のたびに必ずチェック。"},
{id:"i_kouya",t:"🤠 CZ失敗時「曠野の決闘」突入率",rows:[
["設1","1/128.0",1],["設6","1/64.0",6]
],note:"CZ失敗時の一部でフリーズから突入するAT濃厚＋αのエピソードボーナス。高設定ほど突入しやすい（設1=1/128、設6=1/64）。中間設定の詳細値は調査中。"},
{id:"i_trophy",t:"🏆 コパンダトロフィー",rows:[
["銅","設定2以上濃厚",2],["銀","設定3以上濃厚",3],["金","設定4以上濃厚",4],
["イナズマ","設定5以上濃厚",5],["虹","設定6濃厚",6]
],note:"AT終了画面・CZ失敗画面で出現する可能性あり。出現すれば該当設定以上が濃厚。"},
{id:"i_end",t:"🏁 AT終了画面",rows:[
["画面⑥","設5期待度UP（設6より出やすい）",5]
],note:"AT終了画面に設定示唆パターンあり（多くは詳細調査中）。画面⑥は設5期待度UP。キャラ誕生日のお祝い画面は設定示唆と無関係。"},
{id:"i_ggo",t:"🎮 GGOモード（高設定ほど滞在しやすい）",rows:[
["キリト","天井が500G以内に短縮"],
["詩乃","CZ当選をAT直撃に変換"],
["シノン","AT中 常にスナイパーチャンス高確"],
["死銃","スナイパーチャンス1戦目がVSデス・ガン"]
],note:"内部モードとは別のGGOモード。設定1で滞在率約20%、高設定ほどいずれかに滞在しやすい。設定変更時は死銃モードが優遇。規定G到達時に液晶左のアイテムで示唆（メニューで確認可）。"},
{id:"i_kappa",t:"⚙️ 出玉率（参考）",rows:[
["設1","97.6%",1],["設2","98.8%",2],["設3","100.2%",3],
["設4","105.3%",4],["設5","110.4%",5],["設6","114.9%",6]
],note:"設1のコイン単価は約4.1円と高め。設4から明確にプラス域。AT初当りの設定差が大きいため、初当り回数が高設定判別の柱になる。"}
];

function buildRatesTable(){
var s=stats(),tG=totalG();
var czEst=(tG>0&&s.czNormal>0)?estX("cz",tG/s.czNormal):null;
var atEst=(tG>0&&s.atFirst>0)?estX("at",tG/s.atFirst):null;
var h='<div class="cyc3"><table><thead><tr><th>設定</th><th>CZ</th><th>AT初当</th><th>出玉率</th></tr></thead><tbody>';
for(var st=1;st<=6;st++){
var hi=(czEst===st||atEst===st);
h=h+'<tr'+(hi?' class="cur"':'')+'>';
h=h+'<td style="color:'+SC[st]+';font-weight:800">設'+st+'</td>';
h=h+'<td style="color:'+SC[st]+'">1/'+REF.cz[st].toFixed(1)+'</td>';
h=h+'<td style="color:'+SC[st]+'">1/'+REF.at[st].toFixed(1)+'</td>';
h=h+'<td style="color:'+SC[st]+'">'+KAPPA[st].toFixed(1)+'%</td>';
h=h+'</tr>';
}
h=h+'</tbody></table></div>';
var lines=[];
if(czEst)lines.push('CZ実測 1/'+(tG/s.czNormal).toFixed(1)+' → 設'+czEst+'付近');
if(atEst)lines.push('AT初当実測 1/'+(tG/s.atFirst).toFixed(1)+' → 設'+atEst+'付近');
if(lines.length){
h=h+'<div class="cc" style="margin-top:8px"><div class="cc-t">あなたの実測</div>';
for(var li=0;li<lines.length;li++)h=h+'<div class="cc-l">'+lines[li]+'</div>';
h=h+'<div class="cc-sub">該当設定の行をハイライトしています</div></div>';
}else{
h=h+'<div style="font-size:10px;color:rgba(255,255,255,.3);margin-top:6px">記録タブでCZ・AT初当りを記録すると、実測に近い設定行がハイライトされます。</div>';
}
return h;
}

function buildCherryTable(){
var h='<div class="cyc3"><table><thead><tr><th>設定</th><th>通常時</th><th>高確中</th></tr></thead><tbody>';
for(var st=1;st<=6;st++){
h=h+'<tr><td style="color:'+SC[st]+';font-weight:800">設'+st+'</td>';
h=h+'<td style="color:'+SC[st]+'">'+CHERRY_CZ.normal[st].toFixed(1)+'%</td>';
h=h+'<td style="color:'+SC[st]+'">'+CHERRY_CZ.high[st].toFixed(1)+'%</td></tr>';
}
h=h+'</tbody></table></div>';
var n=CC.cherryN_t||0,nh=CC.cherryH_t||0;
if(n>0||nh>0){
h=h+'<div class="cc" style="margin-top:8px"><div class="cc-t">あなたの実測</div>';
if(n>0){var pr=CC.cherryN_w/n*100,e=estPct(CHERRY_CZ.normal,pr);h=h+'<div class="cc-l">通常: '+CC.cherryN_w+'/'+n+' ('+pr.toFixed(1)+'%)'+(e?' →設'+e+'付近':'')+'</div>'}
if(nh>0){var ph=CC.cherryH_w/nh*100,eh=estPct(CHERRY_CZ.high,ph);h=h+'<div class="cc-l">高確: '+CC.cherryH_w+'/'+nh+' ('+ph.toFixed(1)+'%)'+(eh?' →設'+eh+'付近':'')+'</div>'}
h=h+'</div>';
}else{
h=h+'<div style="font-size:10px;color:rgba(255,255,255,.3);margin-top:6px">カウンタータブの「レア役別CZ/SC当選率」で記録すると、ここに実測と推定設定が出ます。</div>';
}
return h;
}

function rInfo(){
var ct=document.getElementById("ct");
var h='<div class="info">';
h=h+'<div style="font-size:10px;color:rgba(255,255,255,.35);margin-bottom:10px;line-height:1.6">2026年解析（ちょんぼりすた/なな徹/p-world 照合）にもとづく設定示唆まとめ。各項目をタップで開閉。<b style="color:#38BDF8">AT初当りとCZ確率が判別の柱</b>です。</div>';
for(var i=0;i<INFO.length;i++){
var sec=INFO[i],cl=infoCol[sec.id];
h=h+'<div class="isec"><div class="isec-h" data-itog="'+sec.id+'"><div class="t">'+sec.t+'</div><span class="ar">'+(cl?'▶':'▼')+'</span></div>';
if(!cl){
h=h+'<div class="isec-b">';
if(sec.custom==="rates"){h=h+buildRatesTable();}
else if(sec.custom==="cherry"){h=h+buildCherryTable();}
else{
h=h+'<table class="itbl"><tbody>';
for(var j=0;j<sec.rows.length;j++){
var row=sec.rows[j];var lvl=row[2];
h=h+'<tr><td>';
if(lvl)h=h+'<span class="idot" style="background:'+SC[lvl]+'"></span>';
h=h+row[0]+'</td><td class="v">';
if(lvl)h=h+'<span class="ibadge" style="background:'+SC[lvl]+'">'+row[1]+'</span>';
else h=h+row[1];
h=h+'</td></tr>';
}
h=h+'</tbody></table>';
}
if(sec.note)h=h+'<div class="inote">'+sec.note+'</div>';
h=h+'</div>';
}
h=h+'</div>';
}
h=h+'</div>';
ct.innerHTML=h;
}

/* === 攻略タブ === */
var GUIDE=[
{id:"g_tenjo",t:"⏱️ 天井・狙い目",custom:"tenjo",note:""},
{id:"g_yame",t:"🛑 やめどき（引き戻し・天国確認）",custom:"yame",note:""},
{id:"g_mode",t:"🎚️ 内部モードと液晶G数天井",custom:"mode",note:""},
{id:"g_ggo",t:"🎮 GGOモード（アイテムで示唆）",custom:"ggo",note:""},
{id:"g_route",t:"⚔️ 上位ATルート（デス・ガン/絶剣）",custom:"route",note:""},
{id:"g_reset",t:"🌅 朝イチ・リセット",custom:"reset",note:""}
];

function rGuide(){
var ct=document.getElementById("ct");
var h='<div class="info">';
h=h+'<div style="font-size:10px;color:rgba(255,255,255,.35);margin-bottom:10px;line-height:1.6">設定に関係なく使える実戦メモ。天井・やめどき・GGOモード・上位ATルートなど。タップで開閉。</div>';
for(var i=0;i<GUIDE.length;i++){
var sec=GUIDE[i],cl=guideCol[sec.id];
h=h+'<div class="isec"><div class="isec-h" data-gtog="'+sec.id+'"><div class="t">'+sec.t+'</div><span class="ar">'+(cl?'▶':'▼')+'</span></div>';
if(!cl){
h=h+'<div class="isec-b">';
if(sec.custom==="tenjo"){h=h+buildTenjo();}
else if(sec.custom==="yame"){h=h+buildYame();}
else if(sec.custom==="mode"){h=h+buildMode();}
else if(sec.custom==="ggo"){h=h+buildGgo();}
else if(sec.custom==="route"){h=h+buildRoute();}
else if(sec.custom==="reset"){h=h+buildReset();}
if(sec.note)h=h+'<div class="inote">'+sec.note+'</div>';
h=h+'</div>';
}
h=h+'</div>';
}
h=h+'</div>';
ct.innerHTML=h;
}

function buildTenjo(){
var h='<div class="cyc3"><table><thead><tr><th>天井</th><th>G数</th></tr></thead><tbody>';
h=h+'<tr><td style="font-weight:700;color:rgba(255,255,255,.7)">AT間天井</td><td style="color:#FFB300">1200G</td></tr>';
h=h+'<tr><td style="font-weight:700;color:rgba(255,255,255,.7)">CZ間天井(実G)</td><td style="color:#38BDF8">499G+α</td></tr>';
h=h+'<tr><td style="font-weight:700;color:rgba(255,255,255,.7)">CZ間天井(液晶)</td><td style="color:#7dd3fc">モード別 最大800G</td></tr>';
h=h+'</tbody></table></div>';
h=h+'<div class="cc" style="margin-top:8px"><div class="cc-t">狙い目の考え方</div>';
h=h+'<div class="cc-l">・CZ天井は<b>実G数（499G+α）</b>と<b>液晶G数（モード別）</b>のいずれか早い方で当選。</div>';
h=h+'<div class="cc-l">・<b style="color:#FFB300">設定変更後／初回の上位CZ（デス・ガンバトル）失敗後</b>は実G数のCZ天井が256G+αに短縮。</div>';
h=h+'<div class="cc-l">・AT終了時にCZ天井を350G+αへ短縮する抽選あり。GGOモード「キリト」滞在中は液晶天井500G以内に短縮。</div>';
h=h+'<div class="cc-sub">※上位AT経由の上位CZ失敗後は256短縮の対象外。前日の上位CZ失敗ヤメ台には注意。</div></div>';
return h;
}

function buildYame(){
var h='';
h=h+'<div class="cc"><div class="cc-t">AT後のやめどき手順</div>';
h=h+'<div class="cc-l">① AT後<b style="color:#FFB300">50G</b>は引き戻し区間。最低ここまで回す（50G目のレア役は引き戻し濃厚）。</div>';
h=h+'<div class="cc-l">② 液晶G数が<b>100Gに近い</b>場合は天国（液晶天井100G）の確認後にヤメ推奨。</div>';
h=h+'<div class="cc-l">③ <span class="cc-hl">上位AT後は引き戻しを必ず確認</span>（引き戻し時は上位AT・勝利数引き継ぎ）。</div>';
h=h+'<div class="cc-sub">天国に移行するまでモードダウンは無し。AT後も天国以外ならモード維持。</div></div>';
h=h+'<div class="cc" style="margin-top:6px"><div class="cc-t">ヤメ前チェックリスト</div>';
h=h+'<div class="cc-l">□ 50Gの引き戻し区間を消化したか</div>';
h=h+'<div class="cc-l">□ 液晶100G（天国）を確認したか</div>';
h=h+'<div class="cc-l">□ 上位AT後の引き戻しを見たか</div>';
h=h+'<div class="cc-l">□ GGOモードのアイテム（メニュー）を確認したか</div></div>';
return h;
}

function buildMode(){
var h='<div class="cyc3"><table><thead><tr><th>滞在モード</th><th>液晶G数天井</th></tr></thead><tbody>';
var rows=[["通常A","800G"],["通常B","800G"],["通常C","650G"],["通常D","350G"],["天国","100G"]];
for(var i=0;i<rows.length;i++)h=h+'<tr><td style="color:rgba(255,255,255,.7);font-weight:700">'+rows[i][0]+'</td><td style="color:#7dd3fc">'+rows[i][1]+'</td></tr>';
h=h+'</tbody></table></div>';
h=h+'<div class="cc" style="margin-top:8px"><div class="cc-t">モードの特徴</div>';
h=h+'<div class="cc-l">・CZ/AT終了後にモード昇格を抽選。<b>天国に行くまでモードダウンなし</b>。</div>';
h=h+'<div class="cc-l">・CZ終了後は天国移行抽選を別途実施。AT駆け抜け（SC未勝利）時はモード昇格抽選あり。</div>';
h=h+'<div class="cc-sub">高設定ほどCZ失敗後の天国移行・モード昇格期待度が優遇との示唆あり。</div></div>';
return h;
}

function buildGgo(){
var h='<div class="cyc3"><table><thead><tr><th style="text-align:left">モード</th><th>恩恵</th></tr></thead><tbody>';
var rows=[
["キリト","天井が500G以内に短縮"],
["詩乃","CZ当選をAT直撃に変換"],
["シノン","AT中 常にSC高確"],
["死銃","SC1戦目がVSデス・ガン"]
];
for(var i=0;i<rows.length;i++)h=h+'<tr><td style="text-align:left;color:rgba(255,255,255,.7);font-weight:700">'+rows[i][0]+'</td><td style="font-size:10px;color:#7dd3fc">'+rows[i][1]+'</td></tr>';
h=h+'</tbody></table></div>';
h=h+'<div class="cc" style="margin-top:8px"><div class="cc-t">アイテムで示唆（メニューで確認）</div>';
h=h+'<div class="cc-l">光剣＝キリト／アミュスフィア＝詩乃／ヘカートⅡ＝シノン／黒星＝死銃／バギー＝全モード対応</div>';
h=h+'<div class="cc-l">規定G到達時に液晶左にアイテム表示。色は青＜緑＜赤。<b style="color:#FFB300">総督府のVS銃士X失敗＝死銃濃厚</b>。</div>';
h=h+'<div class="cc-sub">設定変更時・CZ後・AT後に移行抽選。設定変更時は死銃が優遇。高設定ほどいずれかに滞在しやすい（設1で約20%）。</div></div>';
return h;
}

function buildRoute(){
var h='';
h=h+'<div class="cc"><div class="cc-t">上位ATまでの流れ</div>';
h=h+'<div class="cc-l">① AT中<b>スナイパーチャンス（SC）</b>を抽選 → 最大3戦目までに<b style="color:#FFB300">デス・ガン</b>を撃破。</div>';
h=h+'<div class="cc-l">② デス・ガン撃破で上位CZ<b>「デス・ガンバトル」</b>の権利獲得（勝利期待度約50%）。</div>';
h=h+'<div class="cc-l">③ 勝利で<b>ウルティマナイトバトル</b>or<b style="color:#EF5350">絶剣</b>を経由して上位AT（純増約7.2枚）へ。</div>';
h=h+'<div class="cc-sub">設定5はSC1・2戦目のデス・ガン選択率が優遇→上位ATに行きやすい。死銃モードは1戦目VSデス・ガン確定。</div></div>';
h=h+'<div class="cc" style="margin-top:6px"><div class="cc-t">注目ポイント</div>';
h=h+'<div class="cc-l">・<b style="color:#EF5350">絶剣</b>＝最強特化（2200枚+α上乗せ＋ウルティマ状態濃厚、平均約3300枚）。</div>';
h=h+'<div class="cc-l">・ウルティマ状態＝デス・ガンバトル勝率大幅UP（上位ATの約2回に1回・期待約7000枚）。</div>';
h=h+'<div class="cc-l">・SCジャッジのレバーON後PUSH／ヘカートⅡトリガーで勝利時の告知率UP（裏ボタン）。</div></div>';
return h;
}

function buildReset(){
var h='';
h=h+'<div class="cc"><div class="cc-t">設定変更／電源OFF・ON</div>';
h=h+'<div class="cc-l">設定変更：有利区間・天井・内部状態リセット。<b style="color:#FFB300">実GのCZ天井が256G+αに短縮</b>、死銃モード移行が優遇。</div>';
h=h+'<div class="cc-l">電源OFF/ON（据え置き）：有利区間・天井とも引き継ぎ。</div>';
h=h+'<div class="cc-sub">ステージ等による有効なリセット判別は現時点で未判明。実戦上、エンディング等で有利区間リセットすると特化ゾーン（ウルティマナイトバトル/絶剣）からスタートと予想。</div></div>';
return h;
}

/* === 出力タブ === */
function rExp(){
var ct=document.getElementById("ct"),s=stats(),tG=totalG();
var t="━━ スマスロ SAO2 ━━\n"+new Date().toLocaleString("ja-JP")+"\n\n";
t=t+"【タイムライン】\n";
for(var i=0;i<LOG.length;i++){var e=LOG[i],ev=gev(e.ev),g=e.g||"0";
var gF=(e.ev==="at"||e.ev==="upat"||e.ev==="kouya"||e.ev==="bnend")?"【"+g+"】":"("+g+")";
t=t+gF+"　"+(ev?ev.l:e.ev)+"　"+buildNote(e)+"\n"}
t=t+"\n【集計】\n総G: "+tG+"\n";
if(tG>0&&s.czNormal>0){var v=tG/s.czNormal;var e=estX("cz",v);t=t+"CZ: 1/"+v.toFixed(1)+" ["+s.czNormal+"回]"+(e?" →設"+e+"付近":"")+"\n"}
if(s.czNormal>0)t=t+"CZ勝率: "+s.czNormalS+"/"+s.czNormal+" ("+rate(s.czNormalS,s.czNormal)+"%)\n";
if(s.czGsuu||s.czBullet||s.czCherry||s.czOther)t=t+"　契機内訳: 液晶G"+s.czGsuu+" / バレットCT"+s.czBullet+" / 強チェ"+s.czCherry+" / その他"+s.czOther+"\n";
if(s.kakcz>0)t=t+"確定CZ(THE END): "+s.kakcz+"回\n";
if(tG>0&&s.atFirst>0){var v2=tG/s.atFirst;var e2=estX("at",v2);t=t+"AT初当り: 1/"+v2.toFixed(1)+" ["+s.atFirst+"回]"+(e2?" →設"+e2+"付近":"")+"\n"}
t=t+"上位AT:"+s.upat+" 曠野の決闘:"+s.kouya+"\n";
if(s.czFail>0){var ir=rate(s.czItemGot,s.czFail);var ei=estPct(ITEM,parseFloat(ir));t=t+"CZ失敗時アイテム獲得: "+s.czItemGot+"/"+s.czFail+" ("+ir+"%)"+(ei?" →設"+ei+"付近":"")+"\n"}
/* レア役別 */
if(CC.cherryN_t>0){var pr=rate(CC.cherryN_w,CC.cherryN_t);var e3=estPct(CHERRY_CZ.normal,parseFloat(pr));t=t+"強チェCZ(通常): "+CC.cherryN_w+"/"+CC.cherryN_t+" ("+pr+"%)"+(e3?" →設"+e3+"付近":"")+"\n"}
if(CC.cherryH_t>0){var ph=rate(CC.cherryH_w,CC.cherryH_t);var e4=estPct(CHERRY_CZ.high,parseFloat(ph));t=t+"強チェCZ(高確): "+CC.cherryH_w+"/"+CC.cherryH_t+" ("+ph+"%)"+(e4?" →設"+e4+"付近":"")+"\n"}
if(CC.suikaN_t>0){var sr=rate(CC.suikaN_w,CC.suikaN_t);var e5=estPct(SUIKA_SC,parseFloat(sr));t=t+"スイカSC(通常): "+CC.suikaN_w+"/"+CC.suikaN_t+" ("+sr+"%)"+(e5?" →設"+e5+"付近":"")+"\n"}
/* 示唆 */
var sugg=[];
var labelMap={};CNTS.forEach(function(sec){sec.items.forEach(function(it){labelMap[it.k]=it.l})});
["endS5","tCu","tSi","tGo","tIna","tNiji","vPurple"].forEach(function(k){
if(CC[k]>0)sugg.push(labelMap[k]+"×"+CC[k]);});
if(sugg.length)t=t+"示唆: "+sugg.join(" / ")+"\n";
var cm=cMin();if(cm>0)t=t+"★設定"+cm+"以上濃厚\n";
var h='<div class="exp"><div class="exp-h">長押し→すべてを選択→コピー</div>';
h=h+'<textarea class="exp-ta" id="eTA" readonly>'+t.replace(/</g,"&lt;")+'</textarea></div>';
ct.innerHTML=h;var ta=document.getElementById("eTA");if(ta){ta.focus();ta.setSelectionRange(0,ta.value.length)}}

/* === 記録追加 === */
function addEntry(){
if(!curEv)return;
var ev=gev(curEv);
var e={ev:curEv,g:curG||"0"};
if(curRes)e.res=curRes;
if(curNote)e.note=curNote;
if(curMai)e.mai=curMai;
if(curEv==="cz"){e.cztrig=curCztrig||"other";if(curRes==="f"&&curCzitem)e.czitem=curCzitem}
if(curEv==="bnend"){if(curScr)e.scr=curScr}
if(curEv==="at"||curEv==="upat"||curEv==="kouya")inAT=true;
if(curEv==="bnend")inAT=false;
LOG.push(e);
curEv=null;curG="";curRes=null;curCztrig=null;curScr=null;curNote="";curMai="";curCzitem=null;
save();render()}

function doRst(){
if(!rstP){rstP=true;if(rstT)clearTimeout(rstT);rstT=setTimeout(function(){rstP=false;render()},3000);render();return}
LOG=[];initC();inAT=false;save();rstP=false;render()}

/* === イベントハンドラ === */
document.getElementById("W").addEventListener("click",function(ev){
var el=ev.target;
for(var i=0;i<6&&el&&el!==this;i++){if(el.dataset){
if(el.dataset.tab){TAB=el.dataset.tab;render();return}
if(el.dataset.ev){curEv=(curEv===el.dataset.ev?null:el.dataset.ev);curRes=null;curCztrig=null;curScr=null;curMai="";curCzitem=null;render();return}
if(el.dataset.res){curRes=(curRes===el.dataset.res?null:el.dataset.res);render();return}
if(el.dataset.cztrig){curCztrig=(curCztrig===el.dataset.cztrig?null:el.dataset.cztrig);render();return}
if(el.dataset.czitem){curCzitem=(curCzitem===el.dataset.czitem?null:el.dataset.czitem);render();return}
if(el.dataset.scr){curScr=(curScr===el.dataset.scr?null:el.dataset.scr);render();return}
if(el.dataset.a==="add"){addEntry();return}
if(el.dataset.del!==undefined){LOG.splice(parseInt(el.dataset.del),1);save();load();render();return}
if(el.dataset.tog){COL[el.dataset.tog]=!COL[el.dataset.tog];render();return}
if(el.dataset.itog){infoCol[el.dataset.itog]=!infoCol[el.dataset.itog];render();return}
if(el.dataset.gtog){guideCol[el.dataset.gtog]=!guideCol[el.dataset.gtog];render();return}
if(el.dataset.raretab){rareTab=el.dataset.raretab;render();return}
if(el.dataset.ci){CC[el.dataset.ci]=CC[el.dataset.ci]+1;save();render();return}
if(el.dataset.cd){var k2=el.dataset.cd;if(CC[k2]>0)CC[k2]=CC[k2]-1;save();render();return}
}el=el.parentElement}});

document.getElementById("W").addEventListener("input",function(ev){
if(ev.target.id==="iG")curG=ev.target.value;
if(ev.target.id==="iN")curNote=ev.target.value;
if(ev.target.id==="iMai")curMai=ev.target.value;});

load();render();
</script>
</body>
</html>
