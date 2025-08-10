<html lang="ka">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>ძლიერი პაროლების გენერატორი — PasswordForge</title>
  <style>
    :root{--bg:#0f1724;--card:#0b1220;--accent:#7c5cff;--glass:rgba(255,255,255,0.04);--muted:#9aa4b2}
    *{box-sizing:border-box}
    body{margin:0;font-family:Inter, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial; background:linear-gradient(180deg,#071226 0%, #0b1424 100%); color:#e6eef8;min-height:100vh;display:flex;align-items:center;justify-content:center;padding:24px}
    .wrap{width:960px;max-width:96%;display:grid;grid-template-columns:1fr 420px;gap:20px}
    .card{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01)); border:1px solid rgba(255,255,255,0.04); padding:22px;border-radius:14px;box-shadow:0 8px 30px rgba(2,6,23,0.6)}

    h1{margin:0 0 6px;font-size:20px}
    p.lead{margin:0 0 16px;color:var(--muted);font-size:13px}

    label{display:block;font-size:13px;color:var(--muted);margin-bottom:6px}
    input[type=text], input[type=number], select{width:100%;padding:10px;border-radius:10px;border:1px solid rgba(255,255,255,0.04);background:transparent;color:inherit;font-size:15px}
    .row{display:grid;grid-template-columns:1fr 1fr;gap:12px}
    .controls{display:flex;gap:8px;align-items:center;margin-top:12px}

    .btn{background:var(--accent);border:none;color:#fff;padding:10px 14px;border-radius:10px;font-weight:600;cursor:pointer}
    .btn.ghost{background:transparent;border:1px solid rgba(255,255,255,0.06)}

    .result{font-family:monospace;background:linear-gradient(90deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));padding:12px;border-radius:10px;margin-top:14px;display:flex;gap:8px;align-items:center}
    .result .txt{flex:1;word-break:break-all}

    .meter{height:10px;background:rgba(255,255,255,0.04);border-radius:10px;overflow:hidden;margin-top:10px}
    .meter > i{display:block;height:100%;width:0%;background:linear-gradient(90deg,#10b981,#60a5fa);transition:width .25s ease}

    .tips{font-size:13px;color:var(--muted);margin-top:10px}

    /* right column */
    .preview{display:flex;flex-direction:column;gap:12px}
    .sample{padding:12px;border-radius:10px;background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01))}
    .kicker{font-size:12px;color:var(--muted)}

    footer{grid-column:1/-1;text-align:center;color:var(--muted);font-size:12px;margin-top:12px}

    @media (max-width:900px){.wrap{grid-template-columns:1fr} .preview{order:2}}
  </style>
</head>
<body>
  <div class="wrap">
    <div class="card">
      <h1>პაროლის გენერატორი — PasswordForge</h1>
      <p class="lead">ჩაწერე ინფორმაცია, დააჭირე <strong>Enter</strong> — მოიჭრება ძლიერი, ადვილად დასამახსოვრებელი პაროლი.</p>

      <div>
        <label>სახელი</label>
        <input id="name" type="text" placeholder="სახელი" autocomplete="off">
      </div>

      <div style="margin-top:10px">
        <label>ასაკი</label>
        <input id="age" type="number" min="1" max="120" placeholder="ასაკი">
      </div>

      <div style="margin-top:10px">
        <label>საყვარელი ცხოველი</label>
        <input id="animal" type="text" placeholder="ცხოველი">
      </div>

      <div style="margin-top:10px">
        <label>ფერი</label>
        <input id="color" type="text" placeholder="ფერი">
      </div>

      <div class="row" style="margin-top:12px">
        <div>
          <label>სიმბოლოების რაოდენობა (რჩეული მინ.)</label>
          <select id="minSpecial">
            <option value="1">1 სიმბოლო</option>
            <option value="2">2 სიმბოლო</option>
            <option value="3">3 სიმბოლო</option>
          </select>
        </div>
        <div>
          <label>დამატებითი სიგრძე</label>
          <input id="extraLen" type="number" min="0" max="8" value="2">
        </div>
      </div>

      <div class="controls">
        <button class="btn" id="genBtn">Enter</button>
        <button class="btn ghost" id="copyBtn">კოპირება</button>
        <button class="btn ghost" id="shuffleBtn">პაროლის შეცვლა</button>
      </div>

      <div class="result" id="resultBox" style="display:none">
        <div class="txt" id="resultText">D@vIt1black_dog3</div>
        <div style="display:flex;flex-direction:column;align-items:flex-end">
          <div class="kicker" id="scoreLabel">Strength</div>
        </div>
      </div>

      <div class="meter" id="meter" style="display:none"><i></i></div>

      <div class="tips" id="tips" style="display:none"></div>
    </div>

    <div class="card preview">
      <div class="sample">
        <div class="kicker">მაგალითი</div>
        <div style="font-family:monospace;margin-top:8px;font-size:18px">D@vIt1_black-dog3!</div>
      </div>

      <div class="sample">
        <div class="kicker">როგორ ჩნდება ძლიერი პაროლი</div>
        <ul style="margin:8px 0 0 18px;color:var(--muted)">
          <li>წარმოშობის სიტყვები → მცირე ცვლილებები (@, 1, 3)</li>
          <li>შეერთებული ელემენტები: სახელი + ფერი + ცხოველი</li>
          <li>დამატებითი სიმბოლოები და რანდომი ციფრები</li>
        </ul>
      </div>

      <div class="sample">
        <div class="kicker">წესები</div>
        <div style="color:var(--muted);margin-top:6px">თქვენი სახელი, საყვარელი ცხოველი და ფერი დაწერეთ ინგლისურად ხოლო ასაკი ციფრებით.</div>
      </div>

    </div>

    <footer>დავით გრძელიძე</footer>
  </div>

  <script>
    const nameIn = document.getElementById('name')
    const ageIn = document.getElementById('age')
    const animalIn = document.getElementById('animal')
    const colorIn = document.getElementById('color')
    const genBtn = document.getElementById('genBtn')
    const copyBtn = document.getElementById('copyBtn')
    const shuffleBtn = document.getElementById('shuffleBtn')
    const resultBox = document.getElementById('resultBox')
    const resultText = document.getElementById('resultText')
    const meter = document.getElementById('meter')
    const meterFill = meter.querySelector('i')
    const tips = document.getElementById('tips')

    function sanitize(s){ return (s||'').toString().trim() }

    function altCase(s){ return s.split('').map((ch,i)=> i%2? ch.toLowerCase(): ch.toUpperCase()).join('') }
    function leetSub(s){ return s.replace(/a/gi, '@').replace(/i/gi, '1').replace(/e/gi,'3').replace(/o/gi,'0').replace(/s/gi,'$') }

    function randomChoice(arr){ return arr[Math.floor(Math.random()*arr.length)] }
    function randomInt(min,max){ return Math.floor(Math.random()*(max-min+1))+min }

    function buildBase(name, age, color, animal){
      name = sanitize(name)
      color = sanitize(color)
      animal = sanitize(animal)
      age = sanitize(age)
      if(!name && !color && !animal) return ''

      // take first 3 of name + alt case + leet
      let n = name.length>=3? name.slice(0,3): name
      n = altCase(n)
      n = leetSub(n)

      // color + animal normalized
      let c = color.replace(/\s+/g,'')
      let a = animal.replace(/\s+/g,'_')

      // combine with separators
      let parts = [n]
      if(c) parts.push(c.toLowerCase())
      if(a) parts.push(a.toLowerCase())

      // include age digit or two
      if(age) parts.push(age.toString().slice(-2))

      return parts.join('_')
    }

    function addSpecials(str, minSpecial){
      const symbols = ['!','@','#','$','%','&','*','?','-','+']
      // insert minSpecial random symbols in random places
      let arr = str.split('')
      for(let i=0;i<minSpecial;i++){
        const pos = randomInt(1, Math.max(1, arr.length-1))
        arr.splice(pos,0, randomChoice(symbols) )
      }
      return arr.join('')
    }

    function shuffleString(s){ return s.split('').sort(()=>0.5-Math.random()).join('') }

    function scorePassword(s){
      let score = 0
      if(s.length>=10) score += 40
      else score += s.length*4
      if(/[A-Z]/.test(s)) score += 15
      if(/[a-z]/.test(s)) score += 10
      if(/[0-9]/.test(s)) score += 15
      if(/[^A-Za-z0-9]/.test(s)) score += 20
      return Math.min(100, score)
    }

    function describeScore(n){
      if(n>80) return ['ძლიერია', '#10b981']
      if(n>60) return ['საშუალოზე მაღლა', '#60a5fa']
      if(n>40) return ['საშუალო', '#f59e0b']
      return ['მათეა', '#ef4444']
    }

    function generate(options={shuffle:false}){
      const name = nameIn.value
      const age = ageIn.value
      const animal = animalIn.value
      const color = colorIn.value
      const minSpecial = parseInt(document.getElementById('minSpecial').value || '1')
      const extraLen = parseInt(document.getElementById('extraLen').value || '2')

      let base = buildBase(name, age, color, animal)
      if(!base) { alert('გთხოვ ჩაწერე მინიმუმ ერთი ველი (სახელი, ფერი ან ცხოველი).'); return }

      let pass = base
      pass = addSpecials(pass, minSpecial)

      // add extra random chars
      const extras = 'abcdefghijklmnopqrstuvwxyz0123456789'
      for(let i=0;i<extraLen;i++) pass += randomChoice(extras)

      if(options.shuffle) pass = shuffleString(pass)

      // ensure a special at end sometimes
      if(!/[^A-Za-z0-9]/.test(pass)) pass += '!'

      const score = scorePassword(pass)
      const [label, colorHex] = describeScore(score)

      resultText.textContent = pass
      resultBox.style.display = 'flex'
      meter.style.display = 'block'
      meterFill.style.width = Math.round(score)+'%'
      meterFill.style.background = 'linear-gradient(90deg, #10b981, #60a5fa)'
      document.getElementById('scoreLabel').textContent = label + ' ('+score+'%)'
      tips.style.display = 'block'
      tips.textContent = 'წესები: გამოიყენე სხვადასხვა სიმბოლოები, მეტი სიგრძე და არ გახსოვდეს ზუსტად ამავე პაროლზე.'

      // visually accent meter color
      return pass
    }

    genBtn.addEventListener('click',()=>{ generate({shuffle:false}) })
    shuffleBtn.addEventListener('click',()=>{ generate({shuffle:true}) })

    copyBtn.addEventListener('click',()=>{
      const text = resultText.textContent
      if(!text) return alert('ჯერ გენერაცია ჩაატარე')
      navigator.clipboard.writeText(text).then(()=>{ alert('პაროლი კოპირებულია კლიპბორდში') })
    })

    // Enter key on inputs
    [nameIn, ageIn, animalIn, colorIn].forEach(el=>{
      el.addEventListener('keydown', (e)=>{ if(e.key === 'Enter'){ e.preventDefault(); generate({shuffle:false}) } })
    })

  </script>
</body>
