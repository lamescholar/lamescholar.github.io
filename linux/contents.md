---
layout: page
comments: true
title: PDF/DjVu Contents
---

Sadly, PDF & Djvu Bookmarker is rendered poorly by Wine. One must make do with native Linux applications. 

#### PDF

cpdf

`yay -S cpdf`

cpdf.py:

```
import re
import sys
from pathlib import Path


def build_bookmarks(lines: list[str], offset: int, level: int = 0) -> str:
    entries = []
    pattern = re.compile(r"^(.*?)(?:\s*(?:\.\s*){4,}|\s+)\s*(-?\d+)\s*$")

    for line in lines:
        line = line.strip()
        if not line:
            continue
        match = pattern.match(line)
        if not match:
            raise ValueError(f"Could not parse line: {line!r}")

        title = re.sub(r"\s+", " ", match.group(1)).strip()
        page = int(match.group(2)) + offset
        escaped_title = title.replace('"', '\\"')
        entries.append(f'{level} "{escaped_title}" {page}')

    return "\n".join(entries) + ("\n" if entries else "")


def main() -> None:
    base_dir = Path(__file__).resolve().parent
    input_path = base_dir / "outline.txt"
    output_path = base_dir / "outline2.txt"

    chapter_lines = [
        line.strip()
        for line in input_path.read_text(encoding="utf-8").splitlines()
        if line.strip()
    ]

    if not chapter_lines:
        raise ValueError("outline.txt is empty.")

    offset = int(sys.argv[1]) if len(sys.argv) > 1 else 0
    level = int(sys.argv[2]) if len(sys.argv) > 2 else 0

    result = build_bookmarks(chapter_lines, offset, level)
    output_path.write_text(result, encoding="utf-8")


if __name__ == "__main__":
    main()
```
<br>

#### DjVu

djvused

`sudo pacman -S djvulibre`

djvused.py:

```
import re
import sys
from pathlib import Path


def build_bookmarks(lines: list[str], offset: int) -> str:
    entries = []
    pattern = re.compile(r"^(.*?)(?:\s*(?:\.\s*){4,}|\s+)\s*(-?\d+)\s*$")

    for line in lines:
        line = line.strip()
        if not line:
            continue
        match = pattern.match(line)
        if not match:
            raise ValueError(f"Could not parse line: {line!r}")
            
        title = re.sub(r"\s+", " ", match.group(1)).strip()
        page = int(match.group(2)) + offset
        escaped_title = title.replace('"', '\\"')
        entries.append(f'  ("{escaped_title}" "#{page}")')

    return "(bookmarks\n" + "\n".join(entries) + "\n)\n"


def main() -> None:
    base_dir = Path(__file__).resolve().parent
    input_path = base_dir / "outline.txt"
    output_path = base_dir / "outline2.txt"

    chapter_lines = [
        line.strip()
        for line in input_path.read_text(encoding="utf-8").splitlines()
        if line.strip()
    ]

    if not chapter_lines:
        raise ValueError("outline.txt is empty.")

    offset = int(sys.argv[1]) if len(sys.argv) > 1 else 0

    result = build_bookmarks(chapter_lines, offset)
    output_path.write_text(result, encoding="utf-8")


if __name__ == "__main__":
    main()
```
