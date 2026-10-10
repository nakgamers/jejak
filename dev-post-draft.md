<!--
  DEV POST DRAFT — Hacktoberfest Week 1: Touch Grass
  Cara pakai: copy seluruh isi di bawah garis ke editor DEV,
  ganti [BRACKET] dengan link aslimu, lalu publish dengan tags:
  devchallenge, hf26challenge, hacktoberfest, opensource, ai
--------------------------------------------------------------------------------
-->

# Jejak: an Open-Weight AI That Tells Indonesians Which Mountain to Climb Next 🌿

### Hacktoberfest Open-Source AI Challenge Week 1: Touch Grass Submission 🌿

Indonesia has over 130 volcanoes, and somehow planning a weekend hike still
means drowning in scattered blog posts, outdated forum threads, and WhatsApp
groups where the loudest voice wins. I built **Jejak** ("footprint" in
Indonesian) to fix that: tell it who you are as a hiker, and an open-weight
model matches you against a curated dataset of 18 Indonesian mountains —
then hands you a plan, a packing list, and an honest safety briefing.

🔗 **Try it:** [RENDER_URL]
💻 **Code:** [GITHUB_URL]

---

## The problem

"Gunung mana yang cocok buat pemula?" is one of the most-asked questions in
every Indonesian hiking community — and the answers are always anecdotal.
Someone's epic Semeru story convinces a first-timer to attempt a 3,676m
volcano. Generic AI chatbots don't help either: they hallucinate trails,
invent basecamps, and have no idea what "simaksi" (our hiking permit system)
even is.

## What I built

Jejak is a single-page web app, in Indonesian, with one job: **grounded
mountain recommendations.**

1. You fill in your hiker profile — experience level, trip duration, what
   you're chasing (sunrise? crater? waterfall?), departure city, month.
2. The app injects a **curated dataset of 18 Indonesian mountains** (height,
   difficulty 1–5, basecamp, permit info, highlights) into the prompt.
3. **`gpt-oss-20b`, an open-weight model**, reasons over that dataset and returns:
   a ranked shortlist, a trip sketch for the top pick, a packing list, and
   safety warnings tuned to your level and the season.
4. A hard rule in the system prompt: the model may **only** recommend
   mountains from the dataset. No invented trails, ever.

The screen is deliberately the shortest part of the experience — five minutes
of planning, then you close the laptop and go outside. That's the whole point
of Touch Grass.

## Demo

[Screenshot / short screen recording here — show: fill profile → recommendation]

I tested it with my own profile (intermediate, 2D1N, chasing sunrises from
Jakarta). It gave me Papandayan and Prau over the sexier-but-harder options,
and told me *why* — including the honest bit that my fitness wasn't ready for
Ciremai yet. A closed chatbot would have just flattered me.

## The open-source AI core

Everything that makes Jejak work is open:

- **Model:** `openai/gpt-oss-20b`, an open-weight model (Apache 2.0) called
  through Groq's OpenAI-compatible API. The model name is a setting, not a
  marriage — anyone can swap in Llama, Qwen, or any other open-weight model,
  or self-host it with Ollama/llama.cpp and run the whole thing offline.
- **Data:** the trail dataset is a plain JS array in the repo. Fork it, fix
  my mistakes, add your local mountain.
- **No middleman server:** your Groq API key lives only in your
  browser's localStorage. There is no backend harvesting queries.

## Why open innovation matters for this

Three reasons — and the third one happened to me last night:

1. **It can go where the signal doesn't.** Indonesian trailheads famously
   have no reception. Because the model is open-weight, Jejak's roadmap is
   a fully offline build — a small quantized model bundled with the app.
   Try that with a closed API.
2. **Location privacy.** Hikers share departure cities, dates, and fitness
   levels. With open weights I can promise users their data never touches a
   server I control — because there *is* no server. A closed model makes
   that promise impossible.
3. **The model is portable; the vendor isn't.** The night before the
   deadline, my original inference provider (Hugging Face) turned out to
   need paid credits. Because the model was open-weight, switching vendors
   meant changing one endpoint URL and one model name — same prompt, same
   dataset, same app, back online in twenty minutes. If I had built on a
   closed model, that night would have been a rewrite. *That's* what open
   buys you.

## Partner tech

- **Best Use of Render:** Jejak is deployed as a static site on Render
  (deployed with my Hacktoberfest credits). Zero-config hosting for a
  zero-backend app.

## What's next

- Offline bundle (quantized open-weight model + dataset) for no-signal trailheads
- Community trail reports: let hikers flag closed routes / bad weather
- English version — the dataset logic already supports it

---

Built in one night for Hacktoberfest 2026. If it gets even one person off
their screen and onto a mountain, it worked. 🌿

*Tags: devchallenge, hf26challenge, hacktoberfest, opensource, ai*
