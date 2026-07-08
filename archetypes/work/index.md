+++
title    = '{{ replace .File.ContentBaseName "-" " " | title }}'
date     = '{{ .Date }}'
draft    = true

# ── Basic info ────────────────────────────────────────────────────────────────
year     = {{ now.Year }}
client   = ""                        # e.g. "Studio Maison"
role     = ""                        # e.g. "Art Direction, Brand Identity"
summary  = ""                        # one sentence shown on the Work grid

# ── Tags ─────────────────────────────────────────────────────────────────────
# Add as many as you like. Shown on the project page.
tags     = []                        # e.g. ["Branding", "Print", "Identity"]

# ── Layout ───────────────────────────────────────────────────────────────────
# false = simple layout (hero image + gallery only)
# true  = full case-study layout (adds The Challenge + The Solution sections)
flagship = false

# ── Case study fields (only needed when flagship = true) ─────────────────────
challenge = ""
solution  = ""
+++

<!-- Optional: add any extra text about the project here. Delete this line if you don't need it. -->
