# Fun-facts-about-earth-
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Earth Facts</title>
  <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Inter:wght@300;400;500&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --deep: #0a1628;
      --crust: #1c2e4a;
      --lava: #e8541e;
      --ice: #a8d8ea;
      --fossil: #c9a96e;
      --light: #eef2f7;
      --muted: #7a8fa6;
    }

    body {
      background: var(--deep);
      color: var(--light);
      font-family: 'Inter', sans-serif;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 2rem 1rem;
      overflow-x: hidden;
    }

    /* Layered earth rings in background */
    .bg-rings {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      pointer-events: none;
      z-index: 0;
    }
    .bg-rings span {
      display: block;
      border-radius: 50%;
      border: 1px solid rgba(168, 216, 234, 0.06);
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
    .bg-rings span:nth-child(1) { width: 300px; height: 300px; }
    .bg-rings span:nth-child(2) { width: 500px; height: 500px; border-color: rgba(232, 84, 30, 0.05); }
    .bg-rings span:nth-child(3) { width: 700px; height: 700px; }
    .bg-rings span:nth-child(4) { width: 900px; height: 900px; border-color: rgba(201, 169, 110, 0.04); }
    .bg-rings span:nth-child(5) { width: 1100px; height: 1100px; }

    .wrapper {
      position: relative;
      z-index: 1;
      width: 100%;
      max-width: 680px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 2rem;
    }

    header {
      text-align: center;
    }

    .eyebrow {
      font-size: 0.7rem;
      font-weight: 500;
      letter-spacing: 0.2em;
      text-transform: uppercase;
      color: var(--lava);
      margin-bottom: 0.5rem;
    }

    h1 {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(3.5rem, 10vw, 6rem);
      letter-spacing: 0.04em;
      line-height: 0.9;
      color: var(--light);
    }

    h1 span {
      color: var(--ice);
    }

    .card {
      background: var(--crust);
      border: 1px solid rgba(168, 216, 234, 0.12);
      border-radius: 2px;
      padding: 2.5rem;
      width: 100%;
      position: relative;
      overflow: hidden;
      min-height: 220px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      gap: 1.5rem;
    }

    /* Accent stripe */
    .card::before {
      content: '';
      position: absolute;
      top: 0; left: 0;
      width: 4px; height: 100%;
      background: var(--lava);
      transition: background 0.4s;
    }

    .era-badge {
      display: inline-block;
      font-size: 0.65rem;
      font-weight: 500;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      color: var(--fossil);
      background: rgba(201, 169, 110, 0.1);
      border: 1px solid rgba(201, 169, 110, 0.25);
      padding: 0.25rem 0.75rem;
      border-radius: 1px;
      align-self: flex-start;
    }

    .fact-text {
      font-size: clamp(1rem, 2.5vw, 1.2rem);
      font-weight: 300;
      line-height: 1.7;
      color: var(--light);
      flex: 1;
    }

    .fact-text strong {
      color: var(--ice);
      font-weight: 500;
    }

    .fact-meta {
      font-size: 0.75rem;
      color: var(--muted);
      letter-spacing: 0.06em;
    }

    .btn-wrap {
      display: flex;
      gap: 1rem;
      flex-wrap: wrap;
      justify-content: center;
    }

    button {
      font-family: 'Inter', sans-serif;
      font-size: 0.8rem;
      font-weight: 500;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      cursor: pointer;
      border: none;
      border-radius: 1px;
      padding: 0.85rem 2rem;
      transition: all 0.2s ease;
    }

    #btn-next {
      background: var(--lava);
      color: #fff;
    }
    #btn-next:hover { background: #c9441a; }
    #btn-next:active { transform: scale(0.97); }

    #btn-random-era {
      background: transparent;
      color: var(--ice);
      border: 1px solid rgba(168, 216, 234, 0.3);
    }
    #btn-random-era:hover {
      border-color: var(--ice);
      background: rgba(168, 216, 234, 0.05);
    }

    .era-filter {
      display: flex;
      gap: 0.5rem;
      flex-wrap: wrap;
      justify-content: center;
    }

    .era-pill {
      font-size: 0.65rem;
      font-weight: 500;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      background: transparent;
      color: var(--muted);
      border: 1px solid rgba(122, 143, 166, 0.3);
      padding: 0.3rem 0.9rem;
      border-radius: 999px;
      cursor: pointer;
      transition: all 0.2s;
    }

    .era-pill.active, .era-pill:hover {
      color: var(--light);
      border-color: var(--fossil);
      background: rgba(201, 169, 110, 0.1);
    }

    .counter {
      font-size: 0.7rem;
      color: var(--muted);
      letter-spacing: 0.08em;
    }

    .fade-in {
      animation: fadeIn 0.35s ease;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(6px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    @media (max-width: 480px) {
      .card { padding: 1.75rem; }
    }
  </style>
</head>
<body>

<div class="bg-rings">
  <span></span><span></span><span></span><span></span><span></span>
</div>

<div class="wrapper">
  <header>
    <p class="eyebrow">4.5 Billion Years of Story</p>
    <h1>EARTH<br/><span>FACTS</span></h1>
  </header>

  <div class="era-filter" id="era-filter">
    <button class="era-pill active" data-era="all">All Eras</button>
    <button class="era-pill" data-era="hadean">Hadean</button>
    <button class="era-pill" data-era="archean">Archean</button>
    <button class="era-pill" data-era="proterozoic">Proterozoic</button>
    <button class="era-pill" data-era="paleozoic">Paleozoic</button>
    <button class="era-pill" data-era="mesozoic">Mesozoic</button>
    <button class="era-pill" data-era="cenozoic">Cenozoic</button>
    <button class="era-pill" data-era="modern">Modern Earth</button>
  </div>

  <div class="card" id="fact-card">
    <span class="era-badge" id="fact-era">Loading…</span>
    <p class="fact-text" id="fact-text"></p>
    <p class="fact-meta" id="fact-meta"></p>
  </div>

  <div class="btn-wrap">
    <button id="btn-next">Next Fact →</button>
  </div>

  <p class="counter" id="counter"></p>
</div>

<script>
  const facts = [
    { era: "hadean", text: "Earth formed about <strong>4.54 billion years ago</strong> from a cloud of gas and dust swirling around the young Sun — the same cloud that built all the other planets.", time: "~4.54 billion years ago" },
    { era: "hadean", text: "A <strong>Mars-sized body called Theia</strong> slammed into the early Earth. The debris flung into orbit clumped together to form the Moon — our only large natural satellite.", time: "~4.5 billion years ago" },
    { era: "hadean", text: "For the first 600 million years, Earth's surface was a <strong>global ocean of magma</strong>. The planet was so hot that rocks couldn't solidify before being remelted.", time: "~4.5–3.9 billion years ago" },
    { era: "hadean", text: "Earth was bombarded by thousands of asteroids and comets in an event called the <strong>Late Heavy Bombardment</strong>, which delivered much of the water now in our oceans.", time: "~4.1–3.8 billion years ago" },
    { era: "archean", text: "The <strong>oldest rocks on Earth</strong> — the Acasta Gneiss in Canada — are 4.03 billion years old, giving us a rare solid window into the deep past.", time: "~4.03 billion years ago" },
    { era: "archean", text: "Life may have appeared on Earth as early as <strong>3.7 billion years ago</strong>, in the form of microbial mats called stromatolites found in what is now Greenland.", time: "~3.7 billion years ago" },
    { era: "archean", text: "The early atmosphere had <strong>no free oxygen</strong> — it was mostly methane, ammonia, and carbon dioxide. Breathing it today would be instantly fatal.", time: "~3.5 billion years ago" },
    { era: "proterozoic", text: "Cyanobacteria began releasing oxygen as a waste product. This <strong>Great Oxidation Event</strong> was essentially a mass extinction — most life at the time couldn't survive oxygen.", time: "~2.4 billion years ago" },
    { era: "proterozoic", text: "Earth became a <strong>Snowball Earth</strong> — glaciers stretched all the way to the equator and the oceans may have frozen over entirely.", time: "~720–635 million years ago" },
    { era: "proterozoic", text: "All land on Earth was once joined in a supercontinent called <strong>Rodinia</strong>, before it broke apart and the pieces began their long wandering.", time: "~1.1 billion years ago" },
    { era: "paleozoic", text: "The <strong>Cambrian Explosion</strong> saw nearly all major animal body plans appear within just 20 million years — a blink in geological time — including the ancestors of every animal alive today.", time: "~541 million years ago" },
    { era: "paleozoic", text: "Fish were the <strong>first vertebrates</strong> to evolve jaws, around 440 million years ago. Before that, all vertebrates had to filter-feed or suck up food.", time: "~440 million years ago" },
    { era: "paleozoic", text: "Plants colonised the land about <strong>470 million years ago</strong>, eventually turning barren rocky continents into lush forests — and in doing so, dramatically changed the atmosphere.", time: "~470 million years ago" },
    { era: "paleozoic", text: "The <strong>Permian mass extinction</strong>, triggered by massive volcanic eruptions in Siberia, wiped out 96% of all marine species and 70% of land vertebrates — the worst extinction in Earth's history.", time: "~252 million years ago" },
    { era: "mesozoic", text: "Dinosaurs dominated Earth for about <strong>165 million years</strong> — roughly 40 times longer than modern humans have existed.", time: "~230–66 million years ago" },
    { era: "mesozoic", text: "The <strong>first flowering plants</strong> appeared during the Cretaceous, kickstarting an evolutionary partnership with insects that transformed ecosystems worldwide.", time: "~130 million years ago" },
    { era: "mesozoic", text: "A <strong>6-mile-wide asteroid</strong> struck what is now Mexico's Yucatán Peninsula with the force of 10 billion atomic bombs, ending the reign of non-avian dinosaurs.", time: "~66 million years ago" },
    { era: "mesozoic", text: "During the Jurassic, all continents were still joined as the supercontinent <strong>Pangaea</strong>. A sauropod dinosaur could theoretically have walked from what is now Europe to North America.", time: "~200 million years ago" },
    { era: "cenozoic", text: "Mammals rapidly diversified after the dinosaur extinction in an event called the <strong>Mammalian Radiation</strong> — filling every ecological niche left vacant.", time: "~66–50 million years ago" },
    { era: "cenozoic", text: "The <strong>Himalayas</strong> started forming when India crashed into Asia, a collision still ongoing — the mountains are still rising about 5mm per year.", time: "~50 million years ago" },
    { era: "cenozoic", text: "Around 3 million years ago, a <strong>land bridge formed between North and South America</strong>, triggering the Great American Interchange — a dramatic reshuffling of wildlife on both continents.", time: "~3 million years ago" },
    { era: "cenozoic", text: "The last great <strong>Ice Age peaked</strong> about 20,000 years ago. Sea levels were 120 metres lower than today, and humans could walk across what is now the English Channel.", time: "~20,000 years ago" },
    { era: "modern", text: "Earth's <strong>magnetic poles have reversed</strong> over 170 times in the last 76 million years. The last reversal was about 780,000 years ago — and scientists think we may be overdue for another.", time: "Ongoing phenomenon" },
    { era: "modern", text: "Tectonic plates move at roughly the <strong>speed your fingernails grow</strong> — about 2–10 cm per year. Over millions of years, this reshapes entire continents.", time: "Ongoing" },
    { era: "modern", text: "Earth is not a perfect sphere — it <strong>bulges at the equator</strong> due to its rotation, making the equatorial diameter 43 km wider than the polar diameter.", time: "Present" },
    { era: "modern", text: "The <strong>deepest point on Earth</strong>, the Challenger Deep in the Mariana Trench, is 11 km below sea level — deeper than Mount Everest is tall.", time: "Present" },
    { era: "modern", text: "Lightning strikes Earth about <strong>8 million times per day</strong>. Over geological time, lightning may have played a key role in creating the first organic molecules.", time: "Present" },
  ];

  let selectedEra = "all";
  let usedIndices = [];
  let currentIndex = null;

  function getPool() {
    return facts
      .map((f, i) => ({ ...f, i }))
      .filter(f => selectedEra === "all" || f.era === selectedEra);
  }

  function nextFact() {
    let pool = getPool();
    if (pool.length === 0) return;

    // Avoid immediate repeat; reset if all shown
    let available = pool.filter(f => !usedIndices.includes(f.i));
    if (available.length === 0) {
      usedIndices = currentIndex !== null ? [currentIndex] : [];
      available = pool.filter(f => !usedIndices.includes(f.i));
    }

    const pick = available[Math.floor(Math.random() * available.length)];
    usedIndices.push(pick.i);
    currentIndex = pick.i;

    const card = document.getElementById('fact-card');
    card.classList.remove('fade-in');
    void card.offsetWidth;
    card.classList.add('fade-in');

    document.getElementById('fact-era').textContent = pick.era.charAt(0).toUpperCase() + pick.era.slice(1) + (pick.era !== "modern" ? " Eon/Era" : "");
    document.getElementById('fact-text').innerHTML = pick.text;
    document.getElementById('fact-meta').textContent = "⏱ " + pick.time;

    // Stripe color per era
    const colors = { hadean: '#e8541e', archean: '#c9441a', proterozoic: '#c9a96e', paleozoic: '#4caf7d', mesozoic: '#4a90d9', cenozoic: '#a8d8ea', modern: '#8e79d0' };
    card.style.setProperty('--stripe', colors[pick.era] || '#e8541e');
    card.style.cssText = card.style.cssText.replace(/--stripe:[^;]+;/, '') + `--stripe: ${colors[pick.era] || '#e8541e'};`;
    card.querySelector('::before'); // trigger repaint via class toggle trick below

    // Update stripe via data attribute + CSS var workaround
    card.setAttribute('data-era', pick.era);

    updateCounter();
  }

  function updateCounter() {
    const pool = getPool();
    document.getElementById('counter').textContent = `${usedIndices.filter(i => getPool().some(f => f.i === i)).length} of ${pool.length} facts explored`;
  }

  // Dynamic stripe colour
  const styleEl = document.createElement('style');
  document.head.appendChild(styleEl);
  function updateStripe(era) {
    const colors = { hadean: '#e8541e', archean: '#c9441a', proterozoic: '#c9a96e', paleozoic: '#4caf7d', mesozoic: '#4a90d9', cenozoic: '#a8d8ea', modern: '#8e79d0' };
    styleEl.textContent = `.card::before { background: ${colors[era] || '#e8541e'} !important; }`;
  }

  const origNext = nextFact;
  window.nextFact = function() {
    origNext();
    const era = document.getElementById('fact-card').getAttribute('data-era');
    updateStripe(era);
  };

  document.getElementById('btn-next').addEventListener('click', window.nextFact);

  document.getElementById('era-filter').addEventListener('click', e => {
    if (!e.target.classList.contains('era-pill')) return;
    document.querySelectorAll('.era-pill').forEach(p => p.classList.remove('active'));
    e.target.classList.add('active');
    selectedEra = e.target.dataset.era;
    usedIndices = [];
    currentIndex = null;
    window.nextFact();
  });

  // Keyboard support
  document.addEventListener('keydown', e => {
    if (e.key === 'ArrowRight' || e.key === ' ') window.nextFact();
  });

  window.nextFact();
</script>
</body>
</html>
