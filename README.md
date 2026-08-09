# Multilingual Lyrics Dataset — GitHub Parts

The original CSV is larger than GitHub's normal web-upload limit, so it has
been split into multiple CSV files. No rows were intentionally removed.

To reconstruct the original CSV, concatenate the parts in numeric order while
keeping only the first header:

```bash
python - <<'PY'
from pathlib import Path

parts = sorted(Path("datasets").glob("merged_multilingual_lyrics_part_*.csv"))

with open("merged_multilingual_lyrics.csv", "wb") as out:
    for i, p in enumerate(parts):
        with open(p, "rb") as f:
            if i == 0:
                out.write(f.read())
            else:
                f.readline()  # skip repeated header
                out.write(f.read())
PY
```
