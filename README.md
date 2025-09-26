import React from 'react'

export default function UniqueGithubProfile({username='devlohani99',name='Dev Lohani',role='Full-Stack Developer',location='India 🇮🇳',bio='Backend Architecture · Clean Code · Competitive Programming',profiles=[]}){
  const hash=(s)=>{let h=2166136261;for(let i=0;i<s.length;i++){h=((h^s.charCodeAt(i))*16777619)>>>0}return h}
  const seed=hash(username).toString()
  const rnd=(n)=>{let x=Number('0.'+((parseInt(seed,10)*9301+49297)%233280));return Math.floor(x*n)}
  const palette=['#0f172a','#0ea5a4','#60a5fa','#f97316','#a78bfa']
  const p1=palette[seed.charCodeAt(0)%palette.length]
  const p2=palette[(seed.charCodeAt(1)||1)%palette.length]
  const wobble=(i)=>((seed.charCodeAt(i%seed.length)%7)-3)
  const glyphPath=(()=>{
    const pts=[]
    for(let i=0;i<6;i++){pts.push([20+i*12+ wobble(i),40+Math.sin((parseInt(seed)%100+i)/10)*18 +wobble(i)])}
    let d=`M ${pts[0][0]} ${pts[0][1]}`
    for(let i=1;i<pts.length;i++){d+=` C ${pts[i-1][0]+6} ${pts[i-1][1]-10} ${pts[i][0]-6} ${pts[i][1]+10} ${pts[i][0]} ${pts[i][1]}`}
    return d
  })()
  return(
    <div className="min-h-screen bg-gradient-to-b from-gray-900 to-gray-800 flex items-center justify-center p-8">
      <div className="max-w-4xl w-full bg-white/5 backdrop-blur-md rounded-2xl shadow-2xl border border-white/5 overflow-hidden">
        <div className="grid md:grid-cols-3 grid-cols-1 gap-6 p-8">
          <div className="md:col-span-1 flex flex-col items-center justify-center gap-4">
            <svg viewBox="0 0 240 140" className="w-56 h-36" preserveAspectRatio="xMidYMid meet">
              <defs>
                <linearGradient id="g1" x1="0" x2="1">
                  <stop offset="0" stopColor={p1} stopOpacity="0.95"/>
                  <stop offset="1" stopColor={p2} stopOpacity="0.8"/>
                </linearGradient>
                <filter id="f1" x="-20%" y="-20%" width="140%" height="140%">
                  <feTurbulence baseFrequency="0.8" numOctaves="1" seed={seed.charCodeAt(0)%100} result="t"/>
                  <feDisplacementMap in="SourceGraphic" in2="t" scale="6" xChannelSelector="R" yChannelSelector="G"/>
                </filter>
              </defs>
              <rect x="0" y="0" width="240" height="140" rx="18" fill="url(#g1)" filter="url(#f1)"/>
              <path d={glyphPath} fill="none" stroke="#081125" strokeWidth="3" strokeLinejoin="round" strokeLinecap="round" opacity="0.85"/>
              <g transform="translate(140,28)">
                <circle cx="0" cy="0" r="22" fill="rgba(255,255,255,0.06)"/>
                <text x="0" y="6" fontSize="11" fontFamily="ui-sans-serif,system-ui,Segoe UI,Roboto" textAnchor="middle" fill="#fff">{username}</text>
              </g>
            </svg>
            <h2 className="text-white text-xl font-semibold">{name}</h2>
            <p className="text-slate-300 text-sm text-center">{role} · {location}</p>
            <div className="flex gap-3 mt-2">
              {profiles.map((p,i)=> (
                <a key={i} href={p.url} target="_blank" rel="noreferrer" className="w-9 h-9 flex items-center justify-center rounded-full bg-white/6 border border-white/6 hover:scale-110 transition-transform"> 
                  <img src={p.icon} alt={p.name} className="w-5 h-5"/>
                </a>
              ))}
            </div>
          </div>
          <div className="md:col-span-2 p-4 flex flex-col gap-4">
            <div className="flex items-center justify-between">
              <div>
                <h3 className="text-slate-200 text-lg font-medium">About</h3>
                <p className="text-slate-300 mt-1">{bio}</p>
              </div>
              <div className="flex gap-2 items-center">
                <div className="text-xs text-slate-400">Unique seed</div>
                <div className="px-2 py-1 rounded-md bg-white/6 text-xs text-white">{seed}</div>
              </div>
            </div>
            <div className="grid grid-cols-2 md:grid-cols-4 gap-3 mt-1">
              {['Next.js','React','TypeScript','Node.js','MongoDB','Tailwind','C++','Python'].map((t,i)=> (
                <div key={i} className="p-3 rounded-xl bg-white/3 border border-white/4 flex items-center justify-between">
                  <div className="text-sm font-semibold text-white">{t}</div>
                  <div className="text-xs text-slate-300">{(seed.charCodeAt(i%seed.length)%900)+100}pts</div>
                </div>
              ))}
            </div>
            <div className="mt-2 bg-white/3 p-4 rounded-xl border border-white/5">
              <h4 className="text-slate-100 font-medium">Procedural signature</h4>
              <div className="mt-3 flex gap-3 items-center">
                <svg viewBox="0 0 380 80" className="w-full h-20">
                  <defs>
                    <linearGradient id="sig" x1="0" x2="1">
                      <stop offset="0" stopColor={p2}/>
                      <stop offset="1" stopColor={p1}/>
                    </linearGradient>
                  </defs>
                  <path d={glyphPath.replace(/M /,'M 20 ')} fill="none" stroke="url(#sig)" strokeWidth="4" strokeLinecap="round" strokeLinejoin="round"/>
                </svg>
                <div className="text-xs text-slate-300">Deterministic glyph generated from your username</div>
              </div>
            </div>
            <div className="mt-auto flex gap-3 justify-end">
              <button className="px-4 py-2 rounded-lg bg-white/6 hover:bg-white/8 transition">Download SVG</button>
              <button className="px-4 py-2 rounded-lg bg-gradient-to-r from-teal-400 to-blue-500 text-black font-semibold">Use on GitHub</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  )
}
