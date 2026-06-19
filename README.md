Kiimport { useState, useEffect, useRef } from "react";

/* ─── LOGO ── */
function Logo({ size = 28 }) {
  return (
    <svg width={size} height={size} viewBox="0 0 500 500" style={{ flexShrink: 0, borderRadius: size * 0.22 }}>
      <defs>
        <linearGradient id="a" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" stopColor="#FFD700" /><stop offset="100%" stopColor="#FB923C" /></linearGradient>
        <linearGradient id="b" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" stopColor="#4ADE80" /><stop offset="100%" stopColor="#60A5FA" /></linearGradient>
        <linearGradient id="c" x1="0%" y1="100%" x2="100%" y2="0%"><stop offset="0%" stopColor="#A78BFA" /><stop offset="100%" stopColor="#60A5FA" /></linearGradient>
        <linearGradient id="d" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" stopColor="#0D0F1E" /><stop offset="100%" stopColor="#0A1628" /></linearGradient>
      </defs>
      <rect width="500" height="500" rx="110" fill="url(#d)" />
      <polygon points="250,74 378,148 378,296 250,370 122,296 122,148" fill="none" stroke="url(#c)" strokeWidth="2" opacity="0.35" />
      <circle cx="250" cy="210" r="75" fill="#111827" stroke="rgba(167,139,250,0.25)" strokeWidth="2" />
      <g strokeLinecap="round" opacity="0.6">
        <path d="M210,190 Q200,202 205,216" fill="none" stroke="url(#c)" strokeWidth="2.5" />
        <path d="M205,216 Q197,229 211,233" fill="none" stroke="url(#c)" strokeWidth="2.5" />
        <path d="M290,190 Q300,202 295,216" fill="none" stroke="url(#b)" strokeWidth="2.5" />
        <path d="M295,216 Q303,229 289,233" fill="none" stroke="url(#b)" strokeWidth="2.5" />
        <path d="M216,202 Q233,197 250,199 Q267,197 284,202" fill="none" stroke="rgba(255,215,0,0.45)" strokeWidth="1.5" />
      </g>
      <circle cx="210" cy="190" r="3.5" fill="url(#c)" /><circle cx="205" cy="216" r="3" fill="url(#c)" /><circle cx="211" cy="233" r="3.5" fill="url(#c)" />
      <circle cx="290" cy="190" r="3.5" fill="url(#b)" /><circle cx="295" cy="216" r="3" fill="url(#b)" /><circle cx="289" cy="233" r="3.5" fill="url(#b)" />
      <circle cx="250" cy="210" r="6" fill="url(#a)" />
      <path d="M148,330 Q148,290 178,268" fill="none" stroke="url(#c)" strokeWidth="5" strokeLinecap="round" />
      <polygon points="178,258 167,278 189,278" fill="url(#c)" />
      <path d="M250,346 L250,297" fill="none" stroke="url(#a)" strokeWidth="6" strokeLinecap="round" />
      <polygon points="250,283 239,303 261,303" fill="url(#a)" />
      <path d="M352,330 Q352,290 322,268" fill="none" stroke="url(#b)" strokeWidth="5" strokeLinecap="round" />
      <polygon points="322,258 311,278 333,278" fill="url(#b)" />
      <circle cx="250" cy="115" r="7" fill="url(#a)" />
      <circle cx="322" cy="137" r="5" fill="#4ADE80" opacity="0.9" /><circle cx="349" cy="201" r="5" fill="#4ADE80" opacity="0.9" />
      <circle cx="178" cy="137" r="5" fill="#4ADE80" opacity="0.9" /><circle cx="151" cy="201" r="5" fill="#60A5FA" opacity="0.8" />
      <circle cx="322" cy="273" r="4" fill="#A78BFA" opacity="0.7" /><circle cx="178" cy="273" r="4" fill="#A78BFA" opacity="0.7" />
    </svg>
  );
}

/* ─── DATA ── */
const MOODS = [
  { id: "great", emoji: "🌟", label: "Amazing", color: "#FFD700" },
  { id: "good",  emoji: "😊", label: "Good",    color: "#4ADE80" },
  { id: "okay",  emoji: "😐", label: "Okay",    color: "#60A5FA" },
  { id: "low",   emoji: "😔", label: "Low",     color: "#A78BFA" },
  { id: "tired", emoji: "😴", label: "Tired",   color: "#FB923C" },
];
const CHS = {
  great:[{id:1,icon:"🏃",title:"Power Walk",desc:"Take a brisk 5-min walk. Feel that energy!",xp:20,secs:300},{id:2,icon:"📓",title:"Gratitude Burst",desc:"Write 3 things making you smile today.",xp:15,secs:180},{id:3,icon:"🤝",title:"Spread the Vibe",desc:"Send a kind message to someone you appreciate.",xp:25,secs:120}],
  good: [{id:4,icon:"💧",title:"Hydration Check",desc:"Drink a full glass of water right now. Go!",xp:10,secs:60},{id:5,icon:"🧘",title:"Breathe Deep",desc:"4-7-8 breathing: inhale 4s, hold 7s, exhale 8s. 3×.",xp:15,secs:180},{id:6,icon:"📚",title:"Learn One Thing",desc:"Read one interesting fact and share it.",xp:20,secs:300}],
  okay: [{id:7,icon:"🌱",title:"Tiny Win",desc:"Do one small task you've been avoiding.",xp:20,secs:300},{id:8,icon:"🎵",title:"Mood Lift",desc:"Play your fave upbeat song. Dance a little!",xp:15,secs:180},{id:9,icon:"☀️",title:"Sunlight Dose",desc:"Stand by a window or outside for 3 minutes.",xp:10,secs:180}],
  low:  [{id:10,icon:"🫂",title:"Self Hug",desc:"Hand on heart. Take 5 slow, gentle breaths.",xp:15,secs:120},{id:11,icon:"🍵",title:"Comfort Ritual",desc:"Make a warm drink. Sit with it. No phone.",xp:15,secs:300},{id:12,icon:"✍️",title:"Brain Dump",desc:"Write whatever's on your mind. No filter.",xp:20,secs:240}],
  tired:[{id:13,icon:"💤",title:"Nap Plan",desc:"Set a 20-min nap alarm. Your brain needs it.",xp:10,secs:60},{id:14,icon:"🚿",title:"Cold Splash",desc:"Splash cold water on your face. Instant wake-up.",xp:10,secs:60},{id:15,icon:"🍌",title:"Energy Snack",desc:"Eat something natural — fruit, nuts, banana.",xp:15,secs:180}],
};
const HISTORY = [{day:"Mon",mood:4,xp:55},{day:"Tue",mood:3,xp:40},{day:"Wed",mood:5,xp:65},{day:"Thu",mood:4,xp:50},{day:"Fri",mood:2,xp:25},{day:"Sat",mood:4,xp:60},{day:"Today",mood:4,xp:45}];
const FRIENDS = [{name:"Jordan",av:"⚡",streak:21,xp:1340},{name:"Alex K.",av:"🦊",streak:12,xp:840},{name:"Mia R.",av:"🌸",streak:7,xp:620},{name:"You",av:"🌟",streak:5,xp:480,isYou:true}];
const INSIGHTS = ["You feel best on days you complete morning habits 🌅","Your energy peaks mid-week — Tues & Wed ⚡","Hydration challenges boost your mood score by 18% 💧","You're 3× more likely to finish all tasks before noon ☀️"];
const NOTIFS = [
  {id:1,icon:"🔥",title:"Don't break the streak!",body:"You haven't checked in today. 5 days waiting.",time:"9:00 AM",type:"streak"},
  {id:2,icon:"⚡",title:"Jordan just overtook you!",body:"They earned 60 XP this morning. Time to catch up.",time:"10:32 AM",type:"social"},
  {id:3,icon:"✦",title:"Daily challenges are ready",body:"3 fresh challenges based on your mood profile.",time:"8:00 AM",type:"daily"},
  {id:4,icon:"🏆",title:"Weekly recap is in!",body:"You completed 18/21 challenges this week. Top 12%!",time:"Sun 8 PM",type:"insight"},
  {id:5,icon:"🌸",title:"Mia completed all 3 today",body:"Send her a high-five to keep her motivated.",time:"Yesterday",type:"social"},
];
const OB = [
  {logo:true,title:"Welcome to DailyMind",sub:"Your personal micro-habit & mood companion.",cta:"Let's go →"},
  {emoji:"🧠",title:"Pick your daily mood",sub:"We build 3 tiny challenges around how you feel.",cta:"Got it →"},
  {emoji:"⚡",title:"Earn XP & grow streaks",sub:"Small actions compound into life-changing habits.",cta:"Love it →"},
  {emoji:"👥",title:"Challenge your friends",sub:"Accountability makes habits stick 3× better.",cta:"I'm in →"},
  {emoji:"🌟",title:"What's your name?",sub:"Let's personalise your experience.",cta:"Start my journey →",input:true},
];
const PRO_F = ["Unlimited custom challenges","Full mood & XP history forever","AI insight reports & 30-day trends","Unlimited squad & leaderboards","Exclusive Pro badges","Priority support"];
const FREE_F = ["3 daily mood-based challenges","7-day mood & XP history","Basic streak tracking","Up to 3 friends on leaderboard","Core badges"];
const fmt = s => `${Math.floor(s/60)}:${String(s%60).padStart(2,"0")}`;

/* ─── CONFETTI ── */
function Confetti() {
  const p = Array.from({length:30},(_,i)=>({id:i,x:Math.random()*100,c:["#FFD700","#4ADE80","#60A5FA","#A78BFA","#FB923C","#F472B6"][i%6],d:Math.random()*0.5,s:5+Math.random()*8}));
  return <div style={{position:"fixed",inset:0,pointerEvents:"none",zIndex:999,overflow:"hidden"}}>{p.map(x=><div key={x.id} style={{position:"absolute",top:-10,left:`${x.x}%`,width:x.s,height:x.s,background:x.c,borderRadius:2,animation:`cf 2.5s ease-in ${x.d}s forwards`}}/>)}</div>;
}

/* ─── TIMER MODAL ── */
function TimerModal({ch,onClose,onDone}){
  const [secs,setSecs]=useState(ch.secs);
  const [run,setRun]=useState(false);
  const [done,setDone]=useState(false);
  const r=useRef();
  useEffect(()=>{
    if(run&&secs>0){r.current=setInterval(()=>setSecs(s=>s-1),1000);}
    else if(secs===0&&run){clearInterval(r.current);setRun(false);setDone(true);}
    return()=>clearInterval(r.current);
  },[run,secs]);
  const pct=((ch.secs-secs)/ch.secs)*100, circ=2*Math.PI*54;
  return(
    <div onClick={onClose} style={{position:"fixed",inset:0,background:"rgba(0,0,0,0.8)",zIndex:200,display:"flex",alignItems:"center",justifyContent:"center",backdropFilter:"blur(8px)"}}>
      <div onClick={e=>e.stopPropagation()} style={{background:"#0f1220",border:"1px solid rgba(255,255,255,0.1)",borderRadius:24,padding:28,maxWidth:320,width:"90%",display:"flex",flexDirection:"column",alignItems:"center",gap:16,position:"relative"}}>
        <button onClick={onClose} style={{position:"absolute",top:14,right:16,background:"none",border:"none",color:"#555",fontSize:18,cursor:"pointer"}}>✕</button>
        <span style={{fontSize:40}}>{ch.icon}</span>
        <div style={{textAlign:"center"}}><p style={{color:"#fff",fontWeight:700,fontSize:17,margin:"0 0 4px"}}>{ch.title}</p><p style={{color:"#888",fontSize:12,margin:0}}>{ch.desc}</p></div>
        <div style={{position:"relative",width:130,height:130,display:"flex",alignItems:"center",justifyContent:"center"}}>
          <svg width="130" height="130" style={{transform:"rotate(-90deg)",position:"absolute"}}>
            <circle cx="65" cy="65" r="54" fill="none" stroke="rgba(255,255,255,0.06)" strokeWidth="8"/>
            <circle cx="65" cy="65" r="54" fill="none" stroke={done?"#4ADE80":run?"#FFD700":"#A78BFA"} strokeWidth="8" strokeLinecap="round" strokeDasharray={circ} strokeDashoffset={circ-(circ*pct/100)} style={{transition:"stroke-dashoffset 0.9s ease,stroke 0.4s"}}/>
          </svg>
          <span style={{fontSize:done?30:22,color:"#fff",fontWeight:800}}>{done?"✓":fmt(secs)}</span>
        </div>
        {done
          ?<button onClick={()=>{onDone(ch);onClose();}} style={C.goldBtn}>Claim +{ch.xp} XP 🏆</button>
          :<div style={{display:"flex",flexDirection:"column",gap:8,width:"100%"}}>
            <button onClick={()=>setRun(r=>!r)} style={C.purpleBtn}>{run?"⏸ Pause":secs===ch.secs?"▶ Start Timer":"▶ Resume"}</button>
            <button onClick={()=>{onDone(ch);onClose();}} style={{padding:"9px",background:"none",border:"1px solid rgba(255,255,255,0.08)",borderRadius:12,color:"#555",cursor:"pointer",fontSize:12}}>Skip timer</button>
          </div>
        }
      </div>
    </div>
  );
}

/* ─── TOAST ── */
function Toast({msg,onDismiss}){
  useEffect(()=>{const t=setTimeout(onDismiss,3500);return()=>clearTimeout(t);},[]);
  return(
    <div onClick={onDismiss} style={{position:"fixed",top:16,left:"50%",transform:"translateX(-50%)",maxWidth:340,width:"calc(100% - 32px)",background:"rgba(10,12,24,0.97)",border:"1px solid rgba(255,255,255,0.1)",borderRadius:16,padding:"12px 14px",display:"flex",gap:10,alignItems:"center",zIndex:300,backdropFilter:"blur(12px)",boxShadow:"0 8px 32px rgba(0,0,0,0.5)",animation:"td 0.3s ease"}}>
      <span style={{fontSize:20}}>{msg.icon}</span>
      <div style={{flex:1}}><p style={{color:"#fff",fontWeight:700,fontSize:13,margin:"0 0 2px"}}>{msg.title}</p><p style={{color:"#777",fontSize:11,margin:0}}>{msg.body}</p></div>
      <button onClick={onDismiss} style={{background:"none",border:"none",color:"#555",fontSize:14,cursor:"pointer"}}>✕</button>
    </div>
  );
}

/* ─── PRO MODAL ── */
function ProModal({onClose}){
  return(
    <div onClick={onClose} style={{position:"fixed",inset:0,background:"rgba(0,0,0,0.8)",zIndex:200,display:"flex",alignItems:"center",justifyContent:"center",backdropFilter:"blur(8px)"}}>
      <div onClick={e=>e.stopPropagation()} style={{background:"#0f1220",border:"1px solid rgba(255,215,0,0.2)",borderRadius:24,padding:28,maxWidth:340,width:"90%",display:"flex",flexDirection:"column",alignItems:"center",gap:12,position:"relative",maxHeight:"85vh",overflowY:"auto"}}>
        <button onClick={onClose} style={{position:"absolute",top:14,right:16,background:"none",border:"none",color:"#555",fontSize:18,cursor:"pointer"}}>✕</button>
        <Logo size={52}/>
        <p style={{color:"#fff",fontWeight:700,fontSize:18,margin:0}}>DailyMind Pro</p>
        <p style={{color:"#FFD700",fontWeight:800,fontSize:32,margin:0}}>$4.99<span style={{color:"#777",fontSize:13,fontWeight:600}}>/month</span></p>
        <ul style={{listStyle:"none",width:"100%",display:"flex",flexDirection:"column",gap:9}}>
          {PRO_F.map((f,i)=><li key={i} style={{fontSize:13,color:"#ccc",display:"flex",gap:8}}><span style={{color:"#4ADE80"}}>✓</span>{f}</li>)}
        </ul>
        <button style={{...C.goldBtn,width:"100%"}}>Upgrade Now →</button>
        <p style={{color:"#555",fontSize:11,margin:0,textAlign:"center"}}>14-day money-back guarantee. Cancel anytime.</p>
      </div>
    </div>
  );
}

/* ─── LEGAL SCREENS ── */
function LegalScreen({page,onBack}){
  const pages={
    pricing:{title:"Pricing",content:<>
      <div style={{display:"grid",gridTemplateColumns:"1fr 1fr",gap:12,marginBottom:16}}>
        <div style={{background:"rgba(255,255,255,0.04)",border:"1px solid rgba(255,255,255,0.08)",borderRadius:16,padding:16}}>
          <p style={{color:"#fff",fontWeight:700,marginBottom:6}}>Free</p>
          <p style={{color:"#fff",fontWeight:800,fontSize:24,marginBottom:10}}>$0</p>
          <ul style={{listStyle:"none",display:"flex",flexDirection:"column",gap:7}}>{FREE_F.map((f,i)=><li key={i} style={{fontSize:11,color:"#bbb",display:"flex",gap:6}}><span style={{color:"#60A5FA"}}>✓</span>{f}</li>)}</ul>
        </div>
        <div style={{background:"linear-gradient(135deg,rgba(255,215,0,0.07),rgba(251,146,60,0.04))",border:"1px solid rgba(255,215,0,0.25)",borderRadius:16,padding:16}}>
          <p style={{color:"#FFD700",fontWeight:700,marginBottom:6}}>Pro</p>
          <p style={{color:"#fff",fontWeight:800,fontSize:24,marginBottom:10}}>$4.99<span style={{fontSize:11,color:"#777",fontWeight:600}}>/mo</span></p>
          <ul style={{listStyle:"none",display:"flex",flexDirection:"column",gap:7}}>{PRO_F.map((f,i)=><li key={i} style={{fontSize:11,color:"#bbb",display:"flex",gap:6}}><span style={{color:"#4ADE80"}}>✓</span>{f}</li>)}</ul>
        </div>
      </div>
      <p style={{fontSize:11,color:"#555",lineHeight:1.6}}>Prices shown in USD. Subscriptions renew automatically until cancelled. See Refund Policy for details.</p>
    </>},
    terms:{title:"Terms of Service",content:<>
      <p style={lp}>Last updated: June 18, 2026</p>
      <p style={lp}>By using DailyMind you agree to these Terms.</p>
      <p style={lh}>1. Eligibility</p><p style={lp}>You must be at least 13 years old to use this Service.</p>
      <p style={lh}>2. Subscriptions</p><p style={lp}>Pro is billed at $4.99/month via Paddle.com and renews automatically. Cancel anytime in settings.</p>
      <p style={lh}>3. Acceptable Use</p><p style={lp}>Do not misuse, scrape, or use DailyMind for unlawful purposes.</p>
      <p style={lh}>4. Health Disclaimer</p><p style={lp}>DailyMind is a habit tool, not a substitute for professional medical or mental health care.</p>
      <p style={lh}>5. Liability</p><p style={lp}>Service is provided "as is". DailyMind is not liable for indirect or consequential damages.</p>
      <p style={lh}>6. Contact</p><p style={lp}>support@dailymind.app</p>
    </>},
    privacy:{title:"Privacy Policy",content:<>
      <p style={lp}>Last updated: June 18, 2026</p>
      <p style={lh}>What we collect</p><p style={lp}>Name, email, mood logs, XP, streaks, and general device data. Payments handled entirely by Paddle — we never see your card.</p>
      <p style={lh}>How we use it</p><p style={lp}>To operate the app, generate AI insights, process subscriptions, and send optional reminders.</p>
      <p style={lh}>Sharing</p><p style={lp}>We never sell your data. We only share with payment processors, hosting providers, or when legally required.</p>
      <p style={lh}>Your rights</p><p style={lp}>Request access, correction, or deletion anytime at privacy@dailymind.app.</p>
      <p style={lh}>Children</p><p style={lp}>DailyMind is not for users under 13.</p>
    </>},
    refund:{title:"Refund Policy",content:<>
      <p style={lp}>Last updated: June 18, 2026</p>
      <div style={{background:"rgba(74,222,128,0.07)",border:"1px solid rgba(74,222,128,0.2)",borderRadius:12,padding:"12px 14px",marginBottom:12}}>
        <p style={{margin:0,color:"#bbb",fontSize:13}}><strong>14-day money-back guarantee.</strong> Not happy with Pro? Full refund, no questions asked.</p>
      </div>
      <p style={lh}>Eligibility</p><p style={lp}>First-time subscribers can request a refund within 14 days of first payment. Renewals are non-refundable except where required by law.</p>
      <p style={lh}>How to request</p><p style={lp}>Email support@dailymind.app. Refunds via Paddle appear within 5–10 business days.</p>
      <p style={lh}>Cancelling</p><p style={lp}>Cancel in account settings anytime. Access continues until end of paid period.</p>
    </>},
  };
  const pg=pages[page];
  return(
    <div style={{animation:"fu 0.35s ease"}}>
      <button onClick={onBack} style={{background:"none",border:"none",color:"#666",fontSize:13,cursor:"pointer",marginBottom:16,fontFamily:"inherit"}}>← Back</button>
      <h2 style={C.h2}>{pg.title}</h2>
      <div style={{marginTop:14}}>{pg.content}</div>
    </div>
  );
}
const lh={fontSize:13,color:"#fff",fontWeight:700,margin:"14px 0 4px"};
const lp={fontSize:12,color:"#999",lineHeight:1.7,margin:0};

/* ─── MAIN APP ── */
export default function DailyMind(){
  const [step,setStep]=useState(-1); // -1 = onboarding
  const [obIdx,setObIdx]=useState(0);
  const [name,setName]=useState("");
  const [tab,setTab]=useState("today");
  const [screen,setScreen]=useState("home");
  const [mood,setMood]=useState(null);
  const [chs,setChs]=useState([]);
  const [done,setDone]=useState([]);
  const [xp,setXp]=useState(480);
  const [streak]=useState(5);
  const [confetti,setConfetti]=useState(false);
  const [timer,setTimer]=useState(null);
  const [toast,setToast]=useState(null);
  const [readN,setReadN]=useState([]);
  const [iIdx,setIIdx]=useState(0);
  const [notifOn,setNotifOn]=useState(true);
  const [remTime,setRemTime]=useState("08:00");
  const [showPro,setShowPro]=useState(false);
  const [legal,setLegal]=useState(null);

  const level=Math.floor(xp/200)+1;
  const lvlPct=((xp%200)/200)*100;
  const unread=NOTIFS.filter(n=>!readN.includes(n.id)).length;

  useEffect(()=>{const t=setInterval(()=>setIIdx(i=>(i+1)%INSIGHTS.length),4000);return()=>clearInterval(t);},[]);

  const goTab=(t)=>{setTab(t);setScreen("home");setLegal(null);};

  // Onboarding
  if(step===-1){
    const ob=OB[obIdx];
    return(
      <div style={C.root}>
        <Blobs/>
        <div style={{display:"flex",flexDirection:"column",alignItems:"center",justifyContent:"center",minHeight:"100vh",padding:"0 28px",textAlign:"center",position:"relative",zIndex:1}}>
          <div style={{display:"flex",gap:6,marginBottom:40}}>
            {OB.map((_,i)=><div key={i} style={{width:8,height:8,borderRadius:4,background:i===obIdx?"#FFD700":i<obIdx?"#4ADE80":"rgba(255,255,255,0.15)",transition:"all 0.3s"}}/>)}
          </div>
          {ob.logo?<div style={{marginBottom:20}}><Logo size={90}/></div>:<div style={{fontSize:64,marginBottom:20}}>{ob.emoji}</div>}
          <h1 style={{fontFamily:"Georgia,serif",fontSize:26,color:"#fff",fontWeight:400,margin:"0 0 12px",lineHeight:1.3}}>{ob.title}</h1>
          <p style={{fontSize:14,color:"#888",margin:"0 0 32px",lineHeight:1.6}}>{ob.sub}</p>
          {ob.input&&<input value={name} onChange={e=>setName(e.target.value)} placeholder="Your first name…" maxLength={20} style={{width:"100%",padding:"13px 18px",background:"rgba(255,255,255,0.06)",border:"1px solid rgba(255,255,255,0.12)",borderRadius:14,color:"#fff",fontSize:15,outline:"none",marginBottom:20,textAlign:"center",fontFamily:"inherit"}}/>}
          <button onClick={()=>{if(obIdx===OB.length-1){setStep(0);}else setObIdx(i=>i+1);}} disabled={ob.input&&!name.trim()} style={{...C.goldBtn,width:"100%",fontSize:15,padding:"15px",opacity:(ob.input&&!name.trim())?0.4:1}}>{ob.cta}</button>
          {obIdx>0&&<button onClick={()=>setStep(0)} style={{marginTop:14,background:"none",border:"none",color:"#444",fontSize:13,cursor:"pointer",fontFamily:"inherit"}}>Skip intro</button>}
        </div>
      </div>
    );
  }

  const pickMood=(m)=>{setMood(m);setChs(CHS[m.id]);setDone([]);setScreen("challenges");};
  const complete=(ch)=>{
    if(done.includes(ch.id))return;
    const next=[...done,ch.id];
    setDone(next);
    setXp(p=>p+ch.xp);
    setToast({icon:"⚡",title:`+${ch.xp} XP earned!`,body:`"${ch.title}" completed!`});
    if(next.length===chs.length){setConfetti(true);setTimeout(()=>setConfetti(false),3000);}
  };

  return(
    <div style={C.root}>
      <Blobs/>
      {confetti&&<Confetti/>}
      {toast&&<Toast msg={toast} onDismiss={()=>setToast(null)}/>}
      {timer&&<TimerModal ch={timer} onClose={()=>setTimer(null)} onDone={(ch)=>{complete(ch);setTimer(null);}}/>}
      {showPro&&<ProModal onClose={()=>setShowPro(false)}/>}

      <div style={{width:"100%",maxWidth:430,minHeight:"100vh",display:"flex",flexDirection:"column",position:"relative",zIndex:1,paddingBottom:40}}>

        {/* HEADER */}
        <header style={{display:"flex",justifyContent:"space-between",alignItems:"center",padding:"18px 18px 8px"}}>
          <div style={{display:"flex",alignItems:"center",gap:8}}>
            <Logo size={26}/>
            <span style={{fontFamily:"Georgia,serif",fontSize:18,color:"#fff"}}>DailyMind</span>
          </div>
          <div style={{display:"flex",gap:7,alignItems:"center"}}>
            <div style={{display:"flex",alignItems:"center",gap:4,background:"rgba(255,215,0,0.12)",border:"1px solid rgba(255,215,0,0.25)",borderRadius:20,padding:"4px 10px"}}>
              <span style={{fontSize:12}}>⚡</span><span style={{fontSize:12,color:"#FFD700",fontWeight:700}}>{xp} XP</span>
            </div>
            <div style={{display:"flex",alignItems:"center",gap:3,background:"rgba(251,146,60,0.15)",border:"1px solid rgba(251,146,60,0.3)",borderRadius:20,padding:"4px 10px"}}>
              <span style={{fontSize:12}}>🔥</span><span style={{fontSize:12,color:"#FB923C",fontWeight:700}}>{streak}</span>
            </div>
            <button onClick={()=>goTab("notifs")} style={{position:"relative",background:"rgba(255,255,255,0.06)",border:"1px solid rgba(255,255,255,0.1)",borderRadius:20,padding:"5px 10px",fontSize:14,cursor:"pointer"}}>
              🔔{unread>0&&<span style={{position:"absolute",top:-4,right:-4,background:"#FF4444",color:"#fff",fontSize:8,fontWeight:800,borderRadius:10,padding:"1px 4px"}}>{unread}</span>}
            </button>
          </div>
        </header>

        {/* LEVEL BAR */}
        <div style={{display:"flex",alignItems:"center",gap:8,padding:"0 18px 12px"}}>
          <span style={{fontSize:10,color:"#555",fontWeight:700,minWidth:28}}>Lv {level}</span>
          <div style={{flex:1,height:4,background:"rgba(255,255,255,0.08)",borderRadius:4,overflow:"hidden"}}>
            <div style={{height:"100%",width:`${lvlPct}%`,background:"linear-gradient(90deg,#A78BFA,#60A5FA)",borderRadius:4,transition:"width 1s ease"}}/>
          </div>
          <span style={{fontSize:10,color:"#555",fontWeight:700,minWidth:28}}>Lv {level+1}</span>
        </div>

        {/* NAV */}
        <nav style={{display:"flex",gap:4,padding:"0 14px 16px"}}>
          {[["today","✦ Today"],["insights","◈ Insights"],["friends","◉ Squad"],["notifs","🔔"],["profile","◐ Me"]].map(([t,l])=>(
            <button key={t} onClick={()=>goTab(t)} style={{flex:1,padding:"7px 2px",background:tab===t&&screen!=="challenges"&&!legal?"rgba(255,215,0,0.1)":"rgba(255,255,255,0.05)",border:`1px solid ${tab===t&&screen!=="challenges"&&!legal?"rgba(255,215,0,0.3)":"rgba(255,255,255,0.08)"}`,borderRadius:11,color:tab===t&&screen!=="challenges"&&!legal?"#FFD700":"#555",fontSize:10,fontWeight:700,cursor:"pointer",position:"relative"}}>
              {t==="notifs"?<span style={{position:"relative"}}>{l}{unread>0&&<span style={{position:"absolute",top:-6,right:-6,background:"#FF4444",color:"#fff",fontSize:7,fontWeight:800,borderRadius:8,padding:"1px 3px"}}>{unread}</span>}</span>:l}
            </button>
          ))}
        </nav>

        <main style={{flex:1,padding:"0 16px",overflowY:"auto"}}>

          {/* LEGAL */}
          {legal&&<LegalScreen page={legal} onBack={()=>setLegal(null)}/>}

          {/* TODAY */}
          {!legal&&screen==="home"&&tab==="today"&&(
            <div style={{animation:"fu 0.35s ease"}}>
              <h1 style={C.h1}>Good day{name?`, ${name}`:""}. ✦</h1>
              <p style={C.sub}>How are you feeling right now?</p>
              <div style={{display:"grid",gridTemplateColumns:"repeat(5,1fr)",gap:7,marginBottom:24}}>
                {MOODS.map(m=>(
                  <button key={m.id} onClick={()=>pickMood(m)} style={{display:"flex",flexDirection:"column",alignItems:"center",gap:4,padding:"12px 4px",background:"rgba(255,255,255,0.04)",border:"1px solid rgba(255,255,255,0.07)",borderRadius:14,cursor:"pointer"}}>
                    <span style={{fontSize:22}}>{m.emoji}</span>
                    <span style={{fontSize:9,color:"#777",fontWeight:600}}>{m.label}</span>
                  </button>
                ))}
              </div>
              <p style={C.sec}>THIS WEEK</p>
              <div style={{display:"flex",gap:5,alignItems:"flex-end",marginBottom:20}}>
                {HISTORY.map((d,i)=>(
                  <div key={i} style={{display:"flex",flexDirection:"column",alignItems:"center",gap:4,flex:1}}>
                    <div style={{width:9,height:9,borderRadius:"50%",background:d.day==="Today"?"#FFD700":d.xp>50?"#4ADE80":d.xp>30?"#60A5FA":"#2a2a3a",boxShadow:d.day==="Today"?"0 0 10px #FFD70080":"none"}}/>
                    <span style={{fontSize:8,color:"#444",fontWeight:600}}>{d.day}</span>
                  </div>
                ))}
              </div>
              <div style={{background:"rgba(167,139,250,0.08)",border:"1px solid rgba(167,139,250,0.18)",borderRadius:14,padding:"12px 14px"}}>
                <div style={{display:"flex",gap:6,alignItems:"center",marginBottom:5}}><span style={{color:"#A78BFA",fontSize:12}}>◈</span><span style={{fontSize:9,color:"#A78BFA",fontWeight:700,letterSpacing:"0.1em"}}>AI INSIGHT</span></div>
                <p style={{fontSize:12,color:"#bbb",lineHeight:1.5,margin:0}}>{INSIGHTS[iIdx]}</p>
              </div>
            </div>
          )}

          {/* CHALLENGES */}
          {!legal&&screen==="challenges"&&(
            <div style={{animation:"fu 0.35s ease"}}>
              <div style={{display:"flex",justifyContent:"space-between",alignItems:"center",marginBottom:14}}>
                <button onClick={()=>setScreen("home")} style={{background:"none",border:"none",color:"#666",fontSize:13,cursor:"pointer",fontFamily:"inherit"}}>← Back</button>
                <div style={{display:"flex",alignItems:"center",gap:6,background:"rgba(255,255,255,0.06)",borderRadius:20,padding:"5px 12px"}}>
                  <span>{mood?.emoji}</span><span style={{fontSize:11,color:"#ccc",fontWeight:600}}>Feeling {mood?.label}</span>
                </div>
              </div>
              <h2 style={C.h2}>Your 3 challenges</h2>
              <p style={C.sub}>Small steps. Big difference.</p>
              <div style={{display:"flex",flexDirection:"column",gap:12,marginBottom:18}}>
                {chs.map((ch,i)=>{
                  const isDone=done.includes(ch.id);
                  return(
                    <div key={ch.id} style={{background:isDone?"rgba(74,222,128,0.05)":"rgba(255,255,255,0.04)",border:`1px solid ${isDone?"rgba(74,222,128,0.2)":"rgba(255,255,255,0.08)"}`,borderRadius:18,padding:"15px 15px 12px",position:"relative",overflow:"hidden"}}>
                      <div style={{display:"flex",alignItems:"center",gap:10,marginBottom:7}}>
                        <span style={{fontSize:22}}>{ch.icon}</span>
                        <div style={{flex:1}}><p style={{fontSize:14,color:"#fff",fontWeight:700,margin:"0 0 2px"}}>{ch.title}</p><p style={{fontSize:10,color:"#555",margin:0}}>⏱ {fmt(ch.secs)}</p></div>
                        <span style={{fontSize:11,color:"#FFD700",fontWeight:700,background:"rgba(255,215,0,0.1)",borderRadius:10,padding:"2px 8px"}}>+{ch.xp} XP</span>
                      </div>
                      <p style={{fontSize:12,color:"#777",lineHeight:1.5,margin:"0 0 10px"}}>{ch.desc}</p>
                      <div style={{display:"flex",gap:8}}>
                        {!isDone&&<button onClick={()=>setTimer(ch)} style={C.purpleBtn}>▶ Start Timer</button>}
                        <button disabled={isDone} onClick={()=>complete(ch)} style={{flex:1,padding:"9px",borderRadius:10,background:isDone?"rgba(74,222,128,0.15)":"rgba(255,255,255,0.08)",border:`1px solid ${isDone?"rgba(74,222,128,0.3)":"rgba(255,255,255,0.12)"}`,color:isDone?"#4ADE80":"#ccc",fontFamily:"inherit",fontSize:12,fontWeight:700,cursor:isDone?"default":"pointer"}}>
                          {isDone?"✓ Done!":"Mark Done"}
                        </button>
                      </div>
                    </div>
                  );
                })}
              </div>
              {done.length===3&&(
                <div style={{background:"linear-gradient(135deg,rgba(255,215,0,0.1),rgba(251,146,60,0.08))",border:"1px solid rgba(255,215,0,0.22)",borderRadius:18,padding:22,textAlign:"center"}}>
                  <div style={{fontSize:44,marginBottom:8}}>🏆</div>
                  <h3 style={{fontFamily:"Georgia,serif",fontSize:20,color:"#fff",fontWeight:400,margin:"0 0 6px"}}>All done! Incredible!</h3>
                  <p style={{fontSize:12,color:"#888",margin:0}}>You earned <strong style={{color:"#FFD700"}}>{chs.reduce((s,c)=>s+c.xp,0)} XP</strong> today 🔥</p>
                </div>
              )}
            </div>
          )}

          {/* INSIGHTS */}
          {!legal&&screen==="home"&&tab==="insights"&&(
            <div style={{animation:"fu 0.35s ease"}}>
              <h2 style={C.h2}>Your Mind Map ◈</h2>
              <p style={C.sub}>AI patterns found in your data</p>
              {[{lbl:"MOOD THIS WEEK",key:"mood",max:5,multi:18},{lbl:"XP EARNED THIS WEEK",key:"xp",max:65,multi:1}].map(({lbl,key,multi})=>(
                <div key={lbl} style={{background:"rgba(255,255,255,0.03)",border:"1px solid rgba(255,255,255,0.06)",borderRadius:16,padding:14,marginBottom:12}}>
                  <p style={C.sec}>{lbl}</p>
                  <div style={{display:"flex",alignItems:"flex-end",gap:5,height:100}}>
                    {HISTORY.map((d,i)=>(
                      <div key={i} style={{display:"flex",flexDirection:"column",alignItems:"center",flex:1,gap:3,justifyContent:"flex-end"}}>
                        <div style={{width:"100%",borderRadius:"4px 4px 0 0",minHeight:4,height:`${d[key]*multi}px`,background:d.day==="Today"?key==="mood"?"linear-gradient(180deg,#FFD700,#FB923C)":"linear-gradient(180deg,#A78BFA,#60A5FA)":key==="mood"?"linear-gradient(180deg,#4ADE8066,#60A5FA66)":"linear-gradient(180deg,#A78BFA44,#60A5FA44)",transition:"height 0.5s ease"}}/>
                        <span style={{fontSize:8,color:"#444",fontWeight:600}}>{d.day}</span>
                      </div>
                    ))}
                  </div>
                </div>
              ))}
              {INSIGHTS.map((ins,i)=>(
                <div key={i} style={{display:"flex",gap:8,alignItems:"flex-start",background:"rgba(167,139,250,0.06)",border:"1px solid rgba(167,139,250,0.1)",borderRadius:12,padding:"9px 13px",marginBottom:8}}>
                  <span style={{color:"#A78BFA",fontSize:10,marginTop:1}}>◆</span>
                  <span style={{fontSize:11,color:"#bbb",lineHeight:1.5}}>{ins}</span>
                </div>
              ))}
              <div style={{display:"flex",gap:10,alignItems:"center",background:"linear-gradient(135deg,rgba(255,215,0,0.08),rgba(251,146,60,0.05))",border:"1px solid rgba(255,215,0,0.18)",borderRadius:16,padding:"13px",marginTop:10}}>
                <span style={{fontSize:20,color:"#FFD700"}}>✦</span>
                <div style={{flex:1}}><p style={{fontSize:12,color:"#fff",fontWeight:700,margin:"0 0 2px"}}>Unlock Full AI Insights</p><p style={{fontSize:10,color:"#777",margin:0}}>30-day trends, patterns & more.</p></div>
                <button onClick={()=>setShowPro(true)} style={C.goldSmBtn}>Go Pro</button>
              </div>
            </div>
          )}

          {/* FRIENDS */}
          {!legal&&screen==="home"&&tab==="friends"&&(
            <div style={{animation:"fu 0.35s ease"}}>
              <h2 style={C.h2}>Squad Leaderboard ◉</h2>
              <p style={C.sub}>This week's top minds</p>
              <div style={{display:"flex",flexDirection:"column",gap:9,marginBottom:14}}>
                {[...FRIENDS].sort((a,b)=>b.xp-a.xp).map((f,i)=>(
                  <div key={f.name} style={{display:"flex",alignItems:"center",gap:11,background:f.isYou?"rgba(255,215,0,0.06)":"rgba(255,255,255,0.04)",border:`1px solid ${f.isYou?"rgba(255,215,0,0.18)":"rgba(255,255,255,0.07)"}`,borderRadius:14,padding:"12px 14px"}}>
                    <span style={{fontSize:18,width:26,textAlign:"center"}}>{i===0?"🥇":i===1?"🥈":i===2?"🥉":`#${i+1}`}</span>
                    <span style={{fontSize:22}}>{f.av}</span>
                    <div style={{flex:1}}><p style={{fontSize:13,color:"#fff",fontWeight:700,margin:"0 0 2px"}}>{f.name}{f.isYou?" (You)":""}</p><p style={{fontSize:10,color:"#555",margin:0}}>🔥 {f.streak}-day streak</p></div>
                    <div style={{textAlign:"center"}}><p style={{fontSize:15,color:"#FFD700",fontWeight:800,margin:0}}>{f.xp}</p><p style={{fontSize:9,color:"#555",margin:0}}>XP</p></div>
                  </div>
                ))}
              </div>
              <div style={{display:"flex",gap:10,alignItems:"center",background:"rgba(96,165,250,0.08)",border:"1px solid rgba(96,165,250,0.18)",borderRadius:14,padding:"12px 14px",marginBottom:10}}>
                <span style={{fontSize:20}}>⚡</span>
                <div style={{flex:1}}><p style={{fontSize:12,color:"#fff",fontWeight:700,margin:"0 0 2px"}}>Challenge Jordan</p><p style={{fontSize:10,color:"#777",margin:0}}>860 XP ahead — close the gap this week?</p></div>
                <button style={{padding:"7px 12px",background:"rgba(96,165,250,0.18)",border:"1px solid rgba(96,165,250,0.35)",borderRadius:10,color:"#60A5FA",fontSize:11,fontWeight:700,cursor:"pointer"}}>Challenge</button>
              </div>
              <div style={{display:"flex",alignItems:"center",justifyContent:"space-between",background:"rgba(255,255,255,0.03)",border:"1px solid rgba(255,255,255,0.07)",borderRadius:14,padding:"12px 14px"}}>
                <p style={{fontSize:11,color:"#777",margin:0}}>🔗 Invite friends — both earn <strong style={{color:"#FFD700"}}>+50 XP</strong></p>
                <button style={{padding:"7px 12px",background:"rgba(255,255,255,0.07)",border:"1px solid rgba(255,255,255,0.1)",borderRadius:10,color:"#ccc",fontSize:11,fontWeight:700,cursor:"pointer"}}>Share</button>
              </div>
            </div>
          )}

          {/* NOTIFICATIONS */}
          {!legal&&screen==="home"&&tab==="notifs"&&(
            <div style={{animation:"fu 0.35s ease"}}>
              <div style={{display:"flex",justifyContent:"space-between",alignItems:"center",marginBottom:4}}>
                <h2 style={C.h2}>Notifications 🔔</h2>
                <button onClick={()=>setReadN(NOTIFS.map(n=>n.id))} style={{background:"none",border:"none",color:"#A78BFA",fontSize:11,fontWeight:700,cursor:"pointer",fontFamily:"inherit"}}>Mark all read</button>
              </div>
              <p style={C.sub}>{unread} unread</p>
              <div style={{display:"flex",flexDirection:"column",gap:9,marginBottom:16}}>
                {NOTIFS.map(n=>{
                  const read=readN.includes(n.id);
                  return(
                    <div key={n.id} onClick={()=>setReadN(p=>[...new Set([...p,n.id])])} style={{display:"flex",gap:12,alignItems:"flex-start",background:read?"rgba(255,255,255,0.02)":"rgba(255,255,255,0.04)",border:`1px solid ${read?"rgba(255,255,255,0.04)":"rgba(255,255,255,0.08)"}`,borderRadius:14,padding:"12px 14px",cursor:"pointer",opacity:read?0.6:1}}>
                      <div style={{width:36,height:36,borderRadius:10,display:"flex",alignItems:"center",justifyContent:"center",fontSize:18,flexShrink:0,background:n.type==="streak"?"rgba(251,146,60,0.15)":n.type==="social"?"rgba(96,165,250,0.15)":n.type==="insight"?"rgba(167,139,250,0.15)":"rgba(255,215,0,0.1)"}}>{n.icon}</div>
                      <div style={{flex:1}}>
                        <p style={{fontSize:12,color:read?"#555":"#fff",fontWeight:700,margin:"0 0 3px"}}>{n.title}</p>
                        <p style={{fontSize:11,color:"#666",margin:"0 0 4px",lineHeight:1.4}}>{n.body}</p>
                        <p style={{fontSize:9,color:"#444",margin:0}}>{n.time}</p>
                      </div>
                      {!read&&<div style={{width:7,height:7,borderRadius:"50%",background:"#FFD700",flexShrink:0,marginTop:4}}/>}
                    </div>
                  );
                })}
              </div>
              <div style={{background:"rgba(255,255,255,0.03)",border:"1px solid rgba(255,255,255,0.07)",borderRadius:16,padding:"14px"}}>
                <p style={{...C.sec,marginBottom:12}}>NOTIFICATION SETTINGS</p>
                <div style={{display:"flex",alignItems:"center",justifyContent:"space-between",marginBottom:12}}>
                  <div><p style={{fontSize:12,color:"#ddd",fontWeight:700,margin:"0 0 2px"}}>Daily reminder</p><p style={{fontSize:10,color:"#555",margin:0}}>We'll nudge you to check in</p></div>
                  <div onClick={()=>setNotifOn(v=>!v)} style={{width:44,height:24,borderRadius:12,background:notifOn?"#FFD700":"rgba(255,255,255,0.1)",position:"relative",cursor:"pointer",transition:"background 0.3s",flexShrink:0}}>
                    <div style={{position:"absolute",top:3,left:3,width:18,height:18,borderRadius:9,background:"#fff",transition:"transform 0.3s",transform:notifOn?"translateX(20px)":"none"}}/>
                  </div>
                </div>
                {notifOn&&<div style={{display:"flex",alignItems:"center",justifyContent:"space-between",marginBottom:12}}>
                  <p style={{fontSize:12,color:"#ddd",fontWeight:700,margin:0}}>Reminder time</p>
                  <input type="time" value={remTime} onChange={e=>setRemTime(e.target.value)} style={{background:"rgba(255,255,255,0.08)",border:"1px solid rgba(255,255,255,0.12)",borderRadius:10,color:"#fff",fontSize:13,padding:"6px 10px",outline:"none",colorScheme:"dark"}}/>
                </div>}
              </div>
            </div>
          )}

          {/* PROFILE */}
          {!legal&&screen==="home"&&tab==="profile"&&(
            <div style={{animation:"fu 0.35s ease"}}>
              <div style={{display:"flex",flexDirection:"column",alignItems:"center",marginBottom:22}}>
                <div style={{marginBottom:10}}><Logo size={60}/></div>
                <h2 style={{...C.h2,margin:0}}>{name||"You"}</h2>
                <p style={{fontSize:12,color:"#555",margin:"3px 0 14px"}}>@{(name||"you").toLowerCase().replace(/\s/g,"_")}</p>
                <div style={{display:"flex",alignItems:"center",background:"rgba(255,255,255,0.04)",border:"1px solid rgba(255,255,255,0.08)",borderRadius:14,padding:"12px 0",width:"100%"}}>
                  {[["5","Day Streak"],["480","Total XP"],[`Lv ${level}`,"Level"]].map(([v,l],i,arr)=>(
                    <div key={l} style={{flex:1,display:"flex",flexDirection:"column",alignItems:"center",gap:2,borderRight:i<arr.length-1?"1px solid rgba(255,255,255,0.08)":"none"}}>
                      <span style={{fontSize:17,color:"#fff",fontWeight:800}}>{v}</span>
                      <span style={{fontSize:9,color:"#555",fontWeight:600}}>{l}</span>
                    </div>
                  ))}
                </div>
              </div>

              <p style={C.sec}>BADGES EARNED</p>
              <div style={{display:"grid",gridTemplateColumns:"repeat(3,1fr)",gap:8,marginBottom:20}}>
                {[{i:"🔥",n:"5-Day Streak",e:true},{i:"💧",n:"Hydration King",e:true},{i:"🧘",n:"Zen Master",e:true},{i:"🏆",n:"10-Day Streak",e:false},{i:"⚡",n:"500 XP Club",e:false},{i:"🌙",n:"Night Owl",e:false}].map(b=>(
                  <div key={b.n} style={{display:"flex",flexDirection:"column",alignItems:"center",gap:4,background:b.e?"rgba(255,255,255,0.04)":"rgba(255,255,255,0.02)",border:`1px solid ${b.e?"rgba(255,255,255,0.08)":"rgba(255,255,255,0.04)"}`,borderRadius:13,padding:"11px 6px"}}>
                    <span style={{fontSize:22,filter:b.e?"none":"grayscale(1) opacity(0.3)"}}>{b.i}</span>
                    <span style={{fontSize:9,fontWeight:600,textAlign:"center",color:b.e?"#ccc":"#444",lineHeight:1.3}}>{b.n}</span>
                  </div>
                ))}
              </div>

              <p style={C.sec}>SETTINGS</p>
              <div style={{display:"flex",flexDirection:"column",gap:1,marginBottom:16}}>
                {["Edit Profile","Notification Preferences","Privacy Settings","Invite Friends","Rate the App","Sign Out"].map((item,i)=>(
                  <div key={i} style={{display:"flex",justifyContent:"space-between",alignItems:"center",padding:"12px 14px",background:"rgba(255,255,255,0.03)",borderBottom:"1px solid rgba(255,255,255,0.04)",cursor:"pointer"}}>
                    <span style={{fontSize:13,color:"#ccc"}}>{item}</span><span style={{color:"#444",fontSize:12}}>›</span>
                  </div>
                ))}
              </div>

              <p style={C.sec}>LEGAL</p>
              <div style={{display:"flex",flexDirection:"column",gap:1,marginBottom:16}}>
                {[["pricing","Pricing"],["terms","Terms of Service"],["privacy","Privacy Policy"],["refund","Refund Policy"]].map(([key,lbl])=>(
                  <div key={key} onClick={()=>setLegal(key)} style={{display:"flex",justifyContent:"space-between",alignItems:"center",padding:"12px 14px",background:"rgba(255,255,255,0.03)",borderBottom:"1px solid rgba(255,255,255,0.04)",cursor:"pointer"}}>
                    <span style={{fontSize:13,color:"#ccc"}}>{lbl}</span><span style={{color:"#444",fontSize:12}}>›</span>
                  </div>
                ))}
              </div>

              <div style={{display:"flex",gap:10,alignItems:"center",background:"linear-gradient(135deg,rgba(255,215,0,0.08),rgba(251,146,60,0.05))",border:"1px solid rgba(255,215,0,0.18)",borderRadius:16,padding:"13px"}}>
                <span style={{fontSize:20,color:"#FFD700"}}>✦</span>
                <div style={{flex:1}}><p style={{fontSize:12,color:"#fff",fontWeight:700,margin:"0 0 2px"}}>DailyMind Pro — $4.99/mo</p><p style={{fontSize:10,color:"#777",margin:0}}>AI insights · Full history · Custom habits</p></div>
                <button onClick={()=>setShowPro(true)} style={C.goldSmBtn}>Upgrade</button>
              </div>
            </div>
          )}

        </main>
      </div>

      <style>{`
        @keyframes fu { from{opacity:0;transform:translateY(12px)} to{opacity:1;transform:translateY(0)} }
        @keyframes cf { to{transform:translateY(110vh) rotate(720deg);opacity:0} }
        @keyframes td { from{opacity:0;transform:translateX(-50%) translateY(-10px)} to{opacity:1;transform:translateX(-50%) translateY(0)} }
        * { box-sizing:border-box; margin:0; padding:0; }
        ::-webkit-scrollbar { display:none; }
        button { font-family:inherit; }
        button:active { opacity:0.85; transform:scale(0.97); }
      `}</style>
    </div>
  );
}

const Blobs=()=>(
  <div style={{position:"fixed",inset:0,zIndex:0,pointerEvents:"none"}}>
    <div style={{position:"absolute",top:"-20%",left:"-10%",width:500,height:500,borderRadius:"50%",background:"radial-gradient(circle,#1a1060 0%,transparent 70%)",filter:"blur(50px)"}}/>
    <div style={{position:"absolute",bottom:"10%",right:"-15%",width:400,height:400,borderRadius:"50%",background:"radial-gradient(circle,#0a2a1a 0%,transparent 70%)",filter:"blur(50px)"}}/>
    <div style={{position:"absolute",top:"40%",left:"30%",width:300,height:300,borderRadius:"50%",background:"radial-gradient(circle,#1a0a30 0%,transparent 70%)",filter:"blur(60px)"}}/>
  </div>
);

const C={
  root:{minHeight:"100vh",background:"#080B14",display:"flex",justifyContent:"center",fontFamily:"'DM Sans','Segoe UI',sans-serif",position:"relative",overflow:"hidden"},
  h1:{fontFamily:"Georgia,serif",fontSize:24,color:"#fff",margin:"0 0 5px",fontWeight:400,lineHeight:1.2},
  h2:{fontFamily:"Georgia,serif",fontSize:21,color:"#fff",margin:"0 0 4px",fontWeight:400},
  sub:{fontSize:13,color:"#555",margin:"0 0 16px"},
  sec:{fontSize:10,color:"#444",fontWeight:700,letterSpacing:"0.1em",margin:"0 0 10px"},
  goldBtn:{padding:"13px 24px",background:"linear-gradient(135deg,#FFD700,#FB923C)",border:"none",borderRadius:14,color:"#000",fontSize:14,fontWeight:800,cursor:"pointer"},
  goldSmBtn:{flexShrink:0,padding:"8px 14px",background:"linear-gradient(135deg,#FFD700,#FB923C)",border:"none",borderRadius:10,color:"#000",fontSize:11,fontWeight:800,cursor:"pointer"},
  purpleBtn:{flex:1,padding:"9px",borderRadius:10,background:"rgba(167,139,250,0.15)",border:"1px solid rgba(167,139,250,0.3)",color:"#A78BFA",fontSize:12,fontWeight:700,cursor:"pointer"},
}
