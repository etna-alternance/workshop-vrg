---
title: Quake palette - Quake Wiki
source: https://quakewiki.org/wiki/Quake_palette
---

# Quake Palette

![](https://quakewiki.org/w/images/0/09/Qpalette.png)

The Quake palette.

Color 255 is transparent for sprites, 2d lmps, and gfx.wad entries (excluding [conchars](https://quakewiki.org/w/index.php?title=conchars&action=edit&redlink=1 "conchars (page does not exist)"), in which case it is black (color 0) that's made transparent). It is important that palette index 0 is black. The parameters for the [color](https://quakewiki.org/w/index.php?title=color&action=edit&redlink=1 "color (page does not exist)") console command are the row #, but is restricted to rows 0 - 13.

It is important that the latter 8 palette rows are "backwards" (light-to-dark instead of dark-to-light). It appears that the [ID](https://quakewiki.org/wiki/id_Software "id Software") artists did this for no good reason in the original Quake palette, and the engine programmers were forced to add a hack to accommodate it (along with the comment "the artists made some backwards ranges. sigh"). The only area this affects is player shirt/pants color translation (where one palette row must be mapped to another).

| White (0) | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Brown (1) | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 | 30 | 31 |
| Light blue (2) | 32 | 33 | 34 | 35 | 36 | 37 | 38 | 39 | 40 | 41 | 42 | 43 | 44 | 45 | 46 | 47 |
| Green (3) | 48 | 49 | 50 | 51 | 52 | 53 | 54 | 55 | 56 | 57 | 58 | 59 | 60 | 61 | 62 | 63 |
| Red (4) | 64 | 65 | 66 | 67 | 68 | 69 | 70 | 71 | 72 | 73 | 74 | 75 | 76 | 77 | 78 | 79 |
| Orange (5) | 80 | 81 | 82 | 83 | 84 | 85 | 86 | 87 | 88 | 89 | 90 | 91 | 92 | 93 | 94 | 95 |
| Gold (6) | 96 | 97 | 98 | 99 | 100 | 101 | 102 | 103 | 104 | 105 | 106 | 107 | 108 | 109 | 110 | 111 |
| Peach (7) | 112 | 113 | 114 | 115 | 116 | 117 | 118 | 119 | 120 | 121 | 122 | 123 | 124 | 125 | 126 | 127 |
| Purple (8) | 128 | 129 | 130 | 131 | 132 | 133 | 134 | 135 | 136 | 137 | 138 | 139 | 140 | 141 | 142 | 143 |
| Magenta (9) | 144 | 145 | 146 | 147 | 148 | 149 | 150 | 151 | 152 | 153 | 154 | 155 | 156 | 157 | 158 | 159 |
| Tan (10) | 160 | 161 | 162 | 163 | 164 | 165 | 166 | 167 | 168 | 169 | 170 | 171 | 172 | 173 | 174 | 175 |
| Light green (11) | 176 | 177 | 178 | 179 | 180 | 181 | 182 | 183 | 184 | 185 | 186 | 187 | 188 | 189 | 190 | 191 |
| Yellow (12) | 192 | 193 | 194 | 195 | 196 | 197 | 198 | 199 | 200 | 201 | 202 | 203 | 204 | 205 | 206 | 207 |
| Blue (13) | 208 | 209 | 210 | 211 | 212 | 213 | 214 | 215 | 216 | 217 | 218 | 219 | 220 | 221 | 222 | 223 |
| Fire (14) | 224 | 225 | 226 | 227 | 228 | 229 | 230 | 231 | 232 | 233 | 234 | 235 | 236 | 237 | 238 | 239 |
| Brights (15) | 240 | 241 | 242 | 243 | 244 | 245 | 246 | 247 | 248 | 249 | 250 | 251 | 252 | 253 | 254 | 255 |

### palette.lmp

The palette is stored in gfx/palette.lmp. It consists of 256 RGB values using one byte per component, coming out to 768 bytes in total.

### Download

- [File:quake palette.zip](https://quakewiki.org/wiki/File:quake_palette.zip "File:quake palette.zip") - The Quake palette in following formats:.aco,.act,.ase,.pal and the original palette.lmp (raw lump of RGB values, 768-bytes). Also has a plaintext hex matrix and a.png preview.

## Fullbright colors

The last 32 colors in the palette (indices 224 - 255) are **fullbright**  -  they ignore lighting and always render at full intensity. Use them intentionally for glowing surfaces like lava, fire, or lights on model skins. Avoid them on surfaces that should look naturally lit.