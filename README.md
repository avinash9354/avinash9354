from pathlib import Path
import re

path = Path("/mnt/data/README.md")
old = path.read_text(encoding="utf-8")

# Rebuild the visual shell while preserving the large content body.
# GitHub README itself does not allow arbitrary CSS/JS, so "animation" is
# implemented through animated SVG/image services that render in GitHub.
hero = r'''<div align="center">

<!-- ═══════════════════════ NEON HERO ═══════════════════════ -->

<img width="100%" src="https://capsule-render.vercel.app/api?type=venom&height=360&section=header&text=AVINASH%20PANDEY&fontSize=82&fontColor=ffffff&fontAlignY=42&desc=AI%20ENGINEERING%20%E2%80%A2%20iOS%20%E2%80%A2%20FLUTTER%20%E2%80%A2%20FULL%20STACK&descSize=19&descAlignY=67&descColor=67e8f9&stroke=00f5ff&strokeWidth=2&color=0:050014,18:160b38,36:312e81,55:7e22ce,72:0e7490,88:064e3b,100:020617&animation=twinkling"/>

<img src="https://readme-typing-svg.demolab.com?font=Space+Grotesk&weight=800&size=25&duration=2300&pause=550&color=00F5FF&center=true&vCenter=true&width=1050&height=70&lines=%E2%9A%A1+WELCOME+TO+AVINASH.OS;%F0%9F%A7%A0+AI+SYSTEMS+%E2%80%A2+MOBILE+ENGINEERING+%E2%80%A2+PRODUCT+BUILDING;%F0%9F%9A%80+TURNING+IMPOSSIBLE+IDEAS+INTO+REAL+SOFTWARE;%F0%9F%94%A5+SWIFTUI+%2B+FLUTTER+%2B+PYTHON+%2B+TYPESCRIPT;%F0%9F%8C%8C+BUILDING+THE+FUTURE%2C+ONE+SYSTEM+AT+A+TIME" alt="Animated typing header"/>

<br/>

<img src="https://img.shields.io/badge/%E2%9A%A1%20AI%20ENGINEERING-00F5FF?style=for-the-badge&labelColor=080014&logoColor=white"/>
<img src="https://img.shields.io/badge/%F0%9F%92%9C%20CREATIVE%20CODING-FF2BD6?style=for-the-badge&labelColor=080014"/>
<img src="https://img.shields.io/badge/%F0%9F%94%A5%20BUILDING-FF7A00?style=for-the-badge&labelColor=080014"/>
<img src="https://img.shields.io/badge/%F0%9F%8C%8A%20EXPLORING-7C3AED?style=for-the-badge&labelColor=080014"/>

<br/><br/>

<img src="https://komarev.com/ghpvc/?username=avinash9354&style=for-the-badge&color=00f5ff&label=VISITORS"/>
<img src="https://img.shields.io/github/followers/avinash9354?style=for-the-badge&color=ff2bd6&labelColor=10002b&label=FOLLOWERS"/>
<img src="https://img.shields.io/github/stars/avinash9354?style=for-the-badge&color=ffb000&labelColor=10002b&label=STARS"/>

<br/><br/>

### 🌈 `NEON SIGNAL ONLINE` · `AI LAB ACTIVE` · `BUILD MODE ENABLED`

</div>

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=rect&height=3&section=header&color=0:00F5FF,25:7C3AED,50:FF2BD6,75:FF7A00,100:00F5FF"/>

</div>

> ### 💎 **I don't just write code — I design systems, build experiences, and turn ideas into products.**

'''

# Remove the previous hero up to the first "01 · IDENTITY" section.
marker = "# 01 · `IDENTITY`"
idx = old.find(marker)
if idx == -1:
    raise RuntimeError("Expected README structure not found.")

body = old[idx:]

# Replace bland section separators/headings with a more colorful visual system.
body = body.replace(
    "---\n\n# ",
    '<div align="center">\n\n<img src="https://capsule-render.vercel.app/api?type=rect&height=2&section=header&color=0:00F5FF,33:7C3AED,66:FF2BD6,100:FF7A00"/>\n\n</div>\n\n# '
)

# Make major section headings visually richer without changing the underlying content.
colors = [
    ("00F5FF", "CYAN"),
    ("7C3AED", "VIOLET"),
    ("FF2BD6", "MAGENTA"),
    ("FF7A00", "ORANGE"),
    ("22C55E", "GREEN"),
]
sections = re.findall(r"(?m)^# (\d+) · `([^`]+)`", body)
for i, (num, title) in enumerate(sections):
    c, _ = colors[i % len(colors)]
    old_heading = f"# {num} · `{title}`"
    new_heading = (
        f'<div align="center">\n\n'
        f'<img src="https://img.shields.io/badge/SECTION%20{num}-{title.replace(" ", "%20")}-{c}?style=for-the-badge&labelColor=080014&logoColor=white"/>\n\n'
        f'</div>\n\n'
    )
    body = body.replace(old_heading, new_heading, 1)

# Add animated visual panels at useful points.
inject_ai = r'''
<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=700&size=18&duration=1800&pause=500&color=FF2BD6&center=true&vCenter=true&width=900&height=45&lines=NEURAL+SYSTEMS+ONLINE+%E2%80%A2+COMPUTER+VISION+ONLINE+%E2%80%A2+GENAI+ONLINE" alt="AI lab animation"/>

</div>

'''
body = body.replace("## 🧠 Areas of Exploration", inject_ai + "## 🧠 Areas of Exploration", 1)

inject_mobile = r'''
<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=700&size=17&duration=1700&pause=500&color=00F5FF&center=true&vCenter=true&width=900&height=42&lines=SWIFTUI+%E2%86%92+COREML+%E2%86%92+ON-DEVICE+INTELLIGENCE+%E2%9A%A1;FLUTTER+%E2%86%92+RIVERPOD+%E2%86%92+CROSS-PLATFORM+EXPERIENCES+%F0%9F%8C%88" alt="Mobile engineering animation"/>

</div>

'''
body = body.replace("## 🍎 iOS", inject_mobile + "## 🍎 iOS", 1)

# Replace GitHub telemetry URLs with more colorful configurations.
body = body.replace(
    "bg_color=020617&color=67e8f9&line=6366f1&point=f97316&area=true",
    "bg_color=070014&color=00f5ff&line=ff2bd6&point=ffb000&area=true"
)
body = body.replace(
    "theme=algolia&no-frame=true",
    "theme=discord&no-frame=true"
)
body = body.replace(
    "bg_color=020617&title_color=67e8f9&text_color=e2e8f0",
    "bg_color=070014&title_color=00f5ff&text_color=f5f3ff"
)

# Replace final footer with a stronger animated neon outro.
footer_start = body.find("# 66 ·")
if footer_start != -1:
    body = body[:footer_start] + r'''<div align="center">

<img src="https://capsule-render.vercel.app/api?type=rect&height=4&section=header&color=0:00F5FF,20:7C3AED,40:FF2BD6,60:FF7A00,80:22C55E,100:00F5FF"/>

<br/>

<img src="https://readme-typing-svg.demolab.com?font=Space+Grotesk&weight=900&size=30&duration=2200&pause=650&color=00F5FF&center=true&vCenter=true&width=1000&height=70&lines=KEEP+BUILDING.+KEEP+EXPLORING.+KEEP+SHIPPING.;THE+NEXT+IDEA+STARTS+HERE.+%F0%9F%9A%80;SYSTEM+STATUS%3A+ONLINE+%E2%80%A2+AI+LAB%3A+ACTIVE+%E2%80%A2+FUTURE%3A+LOADING..." alt="Animated footer"/>

<br/><br/>

<img src="https://img.shields.io/badge/%E2%9A%A1%20BUILD-00F5FF?style=for-the-badge&labelColor=080014"/>
<img src="https://img.shields.io/badge/%F0%9F%92%9C%20CREATE-FF2BD6?style=for-the-badge&labelColor=080014"/>
<img src="https://img.shields.io/badge/%F0%9F%A7%A0%20LEARN-7C3AED?style=for-the-badge&labelColor=080014"/>
<img src="https://img.shields.io/badge/%F0%9F%94%A5%20SHIP-FF7A00?style=for-the-badge&labelColor=080014"/>

<br/><br/>

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&height=230&section=footer&color=0:020617,18:064e3b,38:0e7490,58:312e81,78:7e22ce,100:10002b&animation=twinkling"/>

</div>
'''

new = hero + body
path.write_text(new, encoding="utf-8")

print(f"Updated: {path}")
print(f"Lines: {len(new.splitlines()):,}")
print(f"Characters: {len(new):,}")
print("Visual system: neon cyan + violet + magenta + orange + green")
print("Animated elements: hero typing + AI lab + mobile lab + telemetry + footer")
