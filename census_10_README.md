# Maximum nullity of the connected graphs of order 10 — census output

`M10.txt` lists all 11,716,571 connected graphs of order 10 (the output of `geng -c 10`), one per line.
It is split into four gzip files (each under 25 MB) so it can be stored on GitHub:

| file | lines |
|---|---|
| `M10_part0.txt.gz` | 1 – 2,929,143 |
| `M10_part1.txt.gz` | 2,929,144 – 5,858,286 |
| `M10_part2.txt.gz` | 5,858,287 – 8,787,429 |
| `M10_part3.txt.gz` | 8,787,430 – 11,716,571 |

Each part is an independent gzip file of whole lines. To rebuild the full file:

```
gzip -dc M10_part0.txt.gz M10_part1.txt.gz M10_part2.txt.gz M10_part3.txt.gz > M10.txt
shasum -a 256 M10.txt      # compare with SHA256SUMS
```

## Line format

```
graph6   Z   Zhat   M   method
```

`Z` is the zero forcing number, `Zhat` the enhanced zero forcing number, `M` the maximum nullity, and `method` the step
of the census that settled it: `formula` (cut vertex / 2-separation formula), `gram` (integer matrix, plain search),
`del` (deletion bounds meet), `twin`, `twinC` (twins sharing a vector), `kant`, `kantD` (existence proof near a numerical
solution), `gram2` (vectors in special position), `structD` (copying the structure of a numerical solution).
Lines with `M = ?` (methods `nonum`, `deficient`) are the 23 graphs left open by the census; for these M is Zhat - 1 or
Zhat. Since then, 5 of the 23 have been settled with M = Zhat - 1 (`ICzff^m~_`, `ICzfbzmz_`, `ICxvBvmz_`, `ICxvF^m~_`
by the cover rule, `ICzvbp}xo` by a Gröbner basis computation); 18 remain open. See `census-workflow.pdf`.
