# Sharepoint-FIFA

Live at <iframe src="(https://melcervera.github.io/Sharepoint-FIFA/ )"
        width="100%" height="900" frameborder="0" style="border:0;"></iframe>

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FIFA World Cup 2026 — Country Profiles</title>
<style>
  :root{
    --teal:#00a3a1;
    --teal-dark:#007e7c;
    --orange:#ff5a36;
    --ink:#0f1c2e;
    --muted:#5a6b7b;
    --bg:#f3f6f8;
    --card:#ffffff;
    --border:#e2e8ee;
  }
  *{box-sizing:border-box;margin:0;padding:0;}
  body{
    font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;
    background:var(--bg);color:var(--ink);line-height:1.5;
  }
  header{
    background:linear-gradient(120deg,var(--teal-dark),var(--teal));
    color:#fff;padding:40px 24px 32px;text-align:center;
  }
  header h1{font-size:2rem;font-weight:800;letter-spacing:-.5px;}
  header p{opacity:.9;margin-top:8px;font-size:1rem;}
  .accent{height:5px;background:var(--orange);}
  .controls{
    max-width:1200px;margin:24px auto 0;padding:0 24px;
    display:flex;flex-wrap:wrap;gap:12px;align-items:center;justify-content:space-between;
  }
  #search{
    flex:1;min-width:220px;padding:12px 16px;border:1px solid var(--border);
    border-radius:10px;font-size:1rem;outline:none;background:#fff;
  }
  #search:focus{border-color:var(--teal);box-shadow:0 0 0 3px rgba(0,163,161,.15);}
  .count{color:var(--muted);font-size:.9rem;white-space:nowrap;}
  .grid{
    max-width:1200px;margin:24px auto 60px;padding:0 24px;
    display:grid;grid-template-columns:repeat(auto-fill,minmax(280px,1fr));gap:20px;
  }
  .card{
    background:var(--card);border:1px solid var(--border);border-radius:16px;
    overflow:hidden;display:flex;flex-direction:column;
    transition:transform .15s ease,box-shadow .15s ease;
  }
  .card:hover{transform:translateY(-4px);box-shadow:0 12px 30px rgba(15,28,46,.12);}
  .flag-wrap{
    position:relative;background:#eef2f5;aspect-ratio:3/2;overflow:hidden;
    display:flex;align-items:center;justify-content:center;
  }
  .flag-wrap img{width:100%;height:100%;object-fit:cover;display:block;}
  .rank{
    position:absolute;top:10px;left:10px;background:rgba(15,28,46,.82);color:#fff;
    font-size:.72rem;font-weight:700;padding:4px 9px;border-radius:20px;
  }
  .body{padding:16px 18px 18px;display:flex;flex-direction:column;gap:10px;flex:1;}
  .name{font-size:1.2rem;font-weight:800;letter-spacing:-.3px;}
  .group-tag{
    display:inline-block;background:rgba(0,163,161,.12);color:var(--teal-dark);
    font-size:.7rem;font-weight:700;padding:3px 8px;border-radius:6px;margin-left:6px;
    vertical-align:middle;
  }
  .stat{display:flex;align-items:baseline;gap:6px;font-size:.92rem;}
  .stat .lbl{color:var(--muted);font-size:.78rem;text-transform:uppercase;letter-spacing:.04em;}
  .pop{font-weight:700;}
  .fact{
    font-size:.9rem;color:#33424f;background:#f7fafb;border-left:3px solid var(--orange);
    padding:8px 10px;border-radius:0 8px 8px 0;
  }
  .anthem{
    margin-top:auto;display:inline-flex;align-items:center;gap:8px;
    background:var(--orange);color:#fff;text-decoration:none;font-weight:700;font-size:.85rem;
    padding:9px 14px;border-radius:9px;justify-content:center;transition:background .15s;
  }
  .anthem:hover{background:#e63f1d;}
  .anthem svg{width:15px;height:15px;fill:#fff;}
  footer{text-align:center;color:var(--muted);font-size:.8rem;padding:0 24px 40px;}
  .no-results{grid-column:1/-1;text-align:center;color:var(--muted);padding:40px;}
</style>
</head>
<body>
  <div class="accent"></div>
  <header>
    <h1>FIFA World Cup 2026 — Country Profiles</h1>
    <p>All 48 qualified nations · United States · Mexico · Canada · June 11 – July 19, 2026</p>
  </header>
  <div class="accent"></div>

  <div class="controls">
    <input id="search" type="text" placeholder="Search a country or group…" autocomplete="off">
    <span class="count" id="count"></span>
  </div>

  <main class="grid" id="grid"></main>

  <footer>
    Population figures are approximate (latest UN/national estimates). Anthem links open a YouTube search for the official national anthem. Flags via flagcdn.com.
  </footer>

<script>
// Each country: name, iso (for flag), pop (approx), group, fact
const countries = [
  {name:"United States", iso:"us", pop:"335 million", group:"D", fact:"Co-host of the 2026 World Cup; this is the country's first men's World Cup since hosting in 1994."},
  {name:"Mexico", iso:"mx", pop:"129 million", group:"A", fact:"The opening match is at Mexico City's Estadio Azteca — the first stadium ever to host three World Cup openers."},
  {name:"Canada", iso:"ca", pop:"40 million", group:"B", fact:"Canada is the second-largest country on Earth by area, yet most of its population lives within 160 km of the US border."},
  {name:"Japan", iso:"jp", pop:"124 million", group:"F", fact:"Japan has more than 3,000 KitKat flavours over the years — and was the first nation to qualify for 2026, back in March 2025."},
  {name:"Iran", iso:"ir", pop:"89 million", group:"G", fact:"Iran is home to some of the world's oldest continuously inhabited cities, including Susa, settled over 6,000 years ago."},
  {name:"South Korea", iso:"kr", pop:"52 million", group:"A", fact:"South Korea reached the World Cup semi-finals as co-hosts in 2002 — its best-ever finish."},
  {name:"Australia", iso:"au", pop:"27 million", group:"D", fact:"Australia is the only nation that is also a whole continent, and is home to more kangaroos than people."},
  {name:"Saudi Arabia", iso:"sa", pop:"37 million", group:"H", fact:"Saudi Arabia has no permanent rivers — a remarkable feat for a country larger than Western Europe."},
  {name:"Qatar", iso:"qa", pop:"3 million", group:"B", fact:"Qatar hosted the 2022 World Cup and is one of the richest countries per capita in the world."},
  {name:"Uzbekistan", iso:"uz", pop:"36 million", group:"K", fact:"Making its World Cup debut. Uzbekistan is one of only two 'doubly landlocked' countries on Earth."},
  {name:"Jordan", iso:"jo", pop:"11 million", group:"J", fact:"World Cup debutant. Home to Petra, the rose-red ancient city carved into rock over 2,000 years ago."},
  {name:"Iraq", iso:"iq", pop:"45 million", group:"I", fact:"The last team to qualify, beating Bolivia 2-1. Iraq sits on land once known as Mesopotamia, the 'cradle of civilisation'."},
  {name:"Argentina", iso:"ar", pop:"46 million", group:"J", fact:"Defending champions. Argentina's Aconcagua is the tallest mountain outside Asia at 6,961 m."},
  {name:"Brazil", iso:"br", pop:"216 million", group:"C", fact:"Five-time World Cup winners — more than any other nation. The Amazon rainforest produces around 20% of the world's oxygen."},
  {name:"Uruguay", iso:"uy", pop:"3.4 million", group:"H", fact:"Won the very first World Cup in 1930. It's one of the smallest nations ever to lift the trophy."},
  {name:"Colombia", iso:"co", pop:"52 million", group:"K", fact:"Colombia is the world's second most biodiverse country and the only South American nation with coastlines on both the Pacific and Caribbean."},
  {name:"Ecuador", iso:"ec", pop:"18 million", group:"E", fact:"Named after the Equator, which runs through it. The Galápagos Islands inspired Darwin's theory of evolution."},
  {name:"Paraguay", iso:"py", pop:"6.9 million", group:"D", fact:"One of only two landlocked countries in South America, with Guaraní as a widely spoken official language alongside Spanish."},
  {name:"New Zealand", iso:"nz", pop:"5.2 million", group:"G", fact:"New Zealand has roughly five sheep for every person and was the last major landmass settled by humans."},
  {name:"Morocco", iso:"ma", pop:"38 million", group:"C", fact:"Reached the semi-finals in 2022 — the first African and Arab nation ever to do so."},
  {name:"Senegal", iso:"sn", pop:"18 million", group:"I", fact:"Home to Lake Retba, a naturally pink lake coloured by salt-loving algae."},
  {name:"Egypt", iso:"eg", pop:"112 million", group:"G", fact:"The Great Pyramid of Giza is the only surviving wonder of the ancient world."},
  {name:"Algeria", iso:"dz", pop:"46 million", group:"J", fact:"Africa's largest country by area — over 80% of it is covered by the Sahara Desert."},
  {name:"Tunisia", iso:"tn", pop:"12 million", group:"F", fact:"Parts of Star Wars were filmed in the Tunisian desert; the planet Tatooine is named after the town of Tataouine."},
  {name:"South Africa", iso:"za", pop:"60 million", group:"A", fact:"South Africa has three capital cities and 12 official languages."},
  {name:"Ivory Coast", iso:"ci", pop:"29 million", group:"E", fact:"The world's largest cocoa producer — the source of much of the planet's chocolate."},
  {name:"Ghana", iso:"gh", pop:"34 million", group:"L", fact:"Lake Volta in Ghana is the largest reservoir by surface area in the world."},
  {name:"Cape Verde", iso:"cv", pop:"525,000", group:"E", fact:"World Cup debutant. An island nation off West Africa with more citizens living abroad than at home."},
  {name:"DR Congo", iso:"cd", pop:"102 million", group:"K", fact:"Qualified via the intercontinental playoff. The Congo River is the world's deepest, reaching over 220 m."},
  {name:"England", iso:"gb-eng", pop:"57 million", group:"L", fact:"Won the World Cup as hosts in 1966. England is where modern football's rules were first codified in 1863."},
  {name:"France", iso:"fr", pop:"68 million", group:"I", fact:"Top of the FIFA rankings and two-time champions. France is the most visited country on Earth."},
  {name:"Spain", iso:"es", pop:"48 million", group:"H", fact:"2010 champions. Spain has the second-highest number of UNESCO World Heritage Sites in the world."},
  {name:"Germany", iso:"de", pop:"84 million", group:"E", fact:"Four-time champions. Germany has over 1,500 different types of beer and 1,200+ breweries."},
  {name:"Portugal", iso:"pt", pop:"10 million", group:"K", fact:"Portugal is home to the oldest bookshop in the world, Livraria Bertrand, open since 1732."},
  {name:"Netherlands", iso:"nl", pop:"18 million", group:"F", fact:"Three-time runners-up. About a third of the country lies below sea level."},
  {name:"Belgium", iso:"be", pop:"12 million", group:"G", fact:"Belgium produces around 220,000 tonnes of chocolate a year and invented the modern praline."},
  {name:"Croatia", iso:"hr", pop:"3.9 million", group:"L", fact:"2018 runners-up. The necktie ('cravat') originated with Croatian soldiers."},
  {name:"Switzerland", iso:"ch", pop:"8.8 million", group:"B", fact:"Switzerland has four official languages and is where the World Wide Web was invented at CERN."},
  {name:"Austria", iso:"at", pop:"9 million", group:"J", fact:"Finished third in 1954. Austria gave the world the croissant's ancestor and the modern grand piano."},
  {name:"Scotland", iso:"gb-sct", pop:"5.5 million", group:"C", fact:"Back at the World Cup for the first time since 1998. Scotland has over 790 islands."},
  {name:"Norway", iso:"no", pop:"5.5 million", group:"I", fact:"Norway's coastline, including fjords, is long enough to wrap around the Earth more than twice."},
  {name:"Bosnia and Herzegovina", iso:"ba", pop:"3.2 million", group:"B", fact:"Qualified via playoff, beating Italy. Home to the rebuilt Stari Most, a UNESCO-listed 16th-century bridge."},
  {name:"Sweden", iso:"se", pop:"10.5 million", group:"F", fact:"1958 runners-up. Sweden recycles so efficiently it has imported waste to fuel its power plants."},
  {name:"Türkiye", iso:"tr", pop:"85 million", group:"D", fact:"Finished third in 2002. Istanbul is the only major city that straddles two continents, Europe and Asia."},
  {name:"Czechia", iso:"cz", pop:"10.9 million", group:"A", fact:"Czechs drink more beer per person than any other nation. The word 'robot' comes from a Czech play."},
  {name:"Panama", iso:"pa", pop:"4.5 million", group:"L", fact:"The Panama Canal links the Atlantic and Pacific — one of the few places you can watch the sun rise over the Pacific."},
  {name:"Curacao", iso:"cw", pop:"156,000", group:"E", fact:"The smallest nation by population ever to qualify for a men's World Cup, and the bright-blue Curaçao liqueur's namesake."},
  {name:"Haiti", iso:"ht", pop:"11.7 million", group:"C", fact:"Back at the World Cup for the first time since 1974. Haiti was the first nation founded by a successful slave revolt, in 1804."}
];

const grid = document.getElementById('grid');
const search = document.getElementById('search');
const count = document.getElementById('count');

function anthemUrl(name){
  const q = encodeURIComponent(name + " national anthem official");
  return "https://www.youtube.com/results?search_query=" + q;
}

function render(list){
  grid.innerHTML = "";
  if(list.length === 0){
    grid.innerHTML = '<div class="no-results">No countries match your search.</div>';
    count.textContent = "";
    return;
  }
  count.textContent = list.length + " of 48 nations";
  list.forEach(c => {
    const card = document.createElement('div');
    card.className = 'card';
    card.innerHTML = `
      <div class="flag-wrap">
        <span class="rank">Group ${c.group}</span>
        <img loading="lazy" src="https://flagcdn.com/h240/${c.iso}.png"
             srcset="https://flagcdn.com/h480/${c.iso}.png 2x"
             alt="Flag of ${c.name}"
             onerror="this.style.display='none';this.parentNode.style.minHeight='120px';">
      </div>
      <div class="body">
        <div class="name">${c.name}</div>
        <div class="stat">
          <span class="lbl">Population</span>
          <span class="pop">${c.pop}</span>
        </div>
        <div class="fact">${c.fact}</div>
        <a class="anthem" href="${anthemUrl(c.name)}" target="_blank" rel="noopener">
          <svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg>
          National anthem
        </a>
      </div>`;
    grid.appendChild(card);
  });
}

search.addEventListener('input', () => {
  const q = search.value.trim().toLowerCase();
  const filtered = countries.filter(c =>
    c.name.toLowerCase().includes(q) || ("group " + c.group).toLowerCase().includes(q) || c.group.toLowerCase() === q
  );
  render(filtered);
});

render(countries);
</script>
</body>
</html>
