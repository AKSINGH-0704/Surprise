<div align="center">

<br/>

<h1>Surprise</h1>

### Send someone a moment they won't forget.

*A shareable interactive surprise experience! Balloon pops, personal messages, photos, piano music, and a final reveal. One link. No app. No login.*

<br/>

[![Live](https://img.shields.io/badge/Try_It-Live_Demo-FF6B9D?style=flat-square)](https://surprise-xi-sand.vercel.app)&nbsp;
[![Vercel](https://img.shields.io/badge/Deployed_on-Vercel-000000?style=flat-square&logo=vercel&logoColor=white)](https://vercel.com)&nbsp;
[![JavaScript](https://img.shields.io/badge/Vanilla-JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)&nbsp;
[![No Backend](https://img.shields.io/badge/Backend-None-3ECF8E?style=flat-square)](https://surprise-xi-sand.vercel.app)&nbsp;
[![Zero Dependencies](https://img.shields.io/badge/Dependencies-Zero-7B61FF?style=flat-square)](https://surprise-xi-sand.vercel.app)

<br/>

**[→ Try It Live](https://surprise-xi-sand.vercel.app)**

<br/>

</div>

---

<br/>

## What Is This

You build a surprise. You send one link. They experience it.

The creator goes through a guided flow, picks an occasion, writes personal messages for each balloon, optionally uploads photos, and writes a final message. The app compresses all of it into a single shareable URL using LZ-string encoding. No server. No database. No account.

The recipient opens the link and gets a full interactive experience: themed animations, floating particles, balloons to pop one by one, a photo and message revealed per balloon, and a final typewriter reveal with piano music playing in the background.

Everything lives in the URL.

<br/>

## Occasions

<div align="center">

| Occasion | Theme |
|:---------|:------|
| 🌸 Women's Day | Soft pink palette, Dancing Script font, floral particles |
| 🎂 Birthday | Warm orange, Pacifico font, balloon and star particles |
| 💑 Anniversary | Deep red and gold, Playfair Display, rose particles |
| ❤️ Valentine's Day | Pink and crimson, Dancing Script, heart particles |
| 🎆 New Year | Dark navy with gold, Montserrat, firework particles |
| 🎓 Graduation | Navy and amber, Merriweather, cap and star particles |
| 💐 Mother's Day | Purple and lavender, Dancing Script, floral particles |
| 🤝 Friendship Day | Warm yellow, Pacifico, rainbow particles |

Each occasion has its own color palette, typography, particle system, balloon colors, confetti palette, and a unique piano melody.

</div>

<br/>

## How It Works

```
Creator Flow                          Recipient Flow
────────────────────────────────      ────────────────────────────────
1. Pick occasion + recipient name     1. Open the shared link
2. Write 3–9 balloon messages         2. Welcome screen with their name
3. Upload photos (optional)           3. Pop each balloon one by one
4. Write a final personal message     4. Each pop reveals photo + message
5. Copy the generated link            5. Final typewriter reveal
6. Send it                            6. Piano music plays throughout
```

Everything is encoded into the URL hash using LZ-string compression. The recipient's browser decodes and renders the full experience client-side.

<br/>

## Technical Design

**Zero backend architecture**
All surprise data — messages, images, occasion, name — is JSON-serialized, LZ-string compressed, and encoded into the URL hash (`#s=...`). The recipient's browser decompresses and renders it entirely client-side. No server receives or stores anything.

**Image handling**
Uploaded photos are compressed to a maximum of 280px on the longer axis at 45% JPEG quality using a canvas element before encoding. This keeps the URL within browser limits while preserving enough quality for the reveal experience.

**Audio system**
Piano notes are synthesized in real time using the Web Audio API — no audio files downloaded. Each note uses four harmonic oscillators with a convolver reverb. Each occasion has its own melody sequence with a bass octave layer. The audio loops seamlessly and stops cleanly when the creator exits preview mode.

**Pop sound**
Every balloon pop is a synthesized noise burst through a band-pass filter combined with a frequency-swept sine oscillator — no sound effects library, no audio files.

**Particle system**
Background particles use a 3D perspective projection (focal length 600) to simulate depth — particles at different Z values scale and fade accordingly, creating a parallax float effect. Per-occasion emoji sets and counts.

**Confetti system**
Two modes: burst (radial explosion from balloon click position) and fall (full-screen cascade on final reveal). Burst uses CSS transitions with cubic-bezier easing. Fall uses CSS keyframe animation.

**Typewriter reveal**
Speed adapts to message length — shorter messages type faster, longer ones pace to finish in roughly the same total time window. Cursor blinks after completion then fades out.

<br/>

## Creator Flow Detail

| Step | What Happens |
|:-----|:-------------|
| Occasion select | Theme applied live — colors, fonts, particles all switch instantly |
| Balloon setup | 3 to 9 balloons, each with a message (120 chars) and optional photo |
| First balloon's photo | Used as the profile image on the recipient's welcome screen |
| Final message | Up to 800 characters — revealed with typewriter effect at the end |
| Link generation | Full surprise compressed to a single shareable URL |
| Preview mode | Creator can experience the full recipient flow before sending |

<br/>

## Recipient Flow Detail

| Screen | Experience |
|:-------|:-----------|
| Welcome | Personalized greeting, their name, profile photo (or initial), themed animation |
| Balloon stage | All balloons floating with gentle physics, each clickable |
| Pop | Balloon pops with sound, confetti burst, modal reveals photo + message |
| Final reveal | Full-screen themed reveal, typewriter message, piano music, confetti rain |

<br/>

## Running Locally

No build step. No dependencies. Open and go.

```bash
git clone https://github.com/AKSINGH-0704/Surprise.git
cd Surprise
# Open index.html in any browser
open index.html
```

For the share link to work correctly across devices, serve it over HTTP:

```bash
npx serve .
# → http://localhost:3000
```

<br/>

## Project Structure

```
Surprise/
├── index.html        # Full app markup — all screens
├── app.js            # All logic — themes, audio, particles, encoding, flow
├── style.css         # All styles — animations, themes, layouts
├── package.json      # Minimal — serve script only
└── vercel.json       # Vercel routing config
```

No frameworks. No bundler. No node_modules required to run.

<br/>

---

<div align="center">

Built by **[AKSINGH-0704](https://github.com/AKSINGH-0704)**

*Because some things deserve more than a text message.*

</div>
