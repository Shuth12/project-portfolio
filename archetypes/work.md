+++
title       = '{{ replace .File.ContentBaseName "-" " " | title }}'
date        = '{{ .Date }}'
draft       = true

# Project metadata
year        = {{ now.Year }}
client      = ""
role        = ""          # e.g. "Art Direction, Branding"
tags        = []          # e.g. ["Branding", "Print", "Identity"]

# Display
cover       = ""          # path to cover image, e.g. "images/cover.jpg"
gallery     = []          # ordered list of image paths
flagship    = false       # true = render full case-study layout

# Case-study fields (only used when flagship = true)
summary     = ""          # one-line teaser shown in the grid
challenge   = ""
solution    = ""
+++

<!-- Project narrative (used in case-study layout) -->
