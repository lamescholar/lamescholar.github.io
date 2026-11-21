---
layout: page
comments: true
title: PDF/DjVu contents
---

Sadly, PDF & Djvu Bookmarker is rendered poorly by Wine. We must use native Linux applications.
<br><br>

#### PDF

cpdf

`yay -S cpdf`

cpdf.py

```
import re
import sys
from pathlib import Path


def get_tab_level(raw_line: str) -> int:
    return len(raw_line) - len(raw_line.lstrip("\t"))


def build_bookmarks(lines: list[str], offset: int, base_level: int = 0) -> str:
    entries = []
    pattern = re.compile(r"^(.*?)(?:\s*(?:\.\s*){4,}|\s+)\s*(-?\d+)\s*$")

    for raw_line in lines:
        if not raw_line.strip():
            continue

        line_level = base_level + get_tab_level(raw_line)
        cleaned = raw_line.strip()

        match = pattern.match(cleaned)
        if not match:
            raise ValueError(f"Could not parse line: {cleaned!r}")

        title = re.sub(r"\s+", " ", match.group(1)).strip()
        page = int(match.group(2)) + offset
        escaped_title = title.replace('"', '\\"')
        entries.append(f'{line_level} "{escaped_title}" {page}')

    return "\n".join(entries) + ("\n" if entries else "")


def main() -> None:
    base_dir = Path(__file__).resolve().parent
    input_path = base_dir / "outline.txt"
    output_path = base_dir / "outline2.txt"

    raw_lines = input_path.read_text(encoding="utf-8").splitlines()

    if not any(line.strip() for line in raw_lines):
        raise ValueError("outline.txt is empty.")

    offset = int(sys.argv[1]) if len(sys.argv) > 1 else 0
    base_level = int(sys.argv[2]) if len(sys.argv) > 2 else 0

    result = build_bookmarks(raw_lines, offset, base_level)
    output_path.write_text(result, encoding="utf-8")


if __name__ == "__main__":
    main()
```

Finally:

`cpdf -add-bookmarks outline2.txt 1.pdf -o 2.pdf`
<br><br>

#### DjVu

djvused

`sudo pacman -S djvulibre`

djvused.py

```
import re
import sys
from pathlib import Path


def get_tab_level(raw_line: str) -> int:
    return len(raw_line) - len(raw_line.lstrip("\t"))


def parse_line(line: str, offset: int, pattern: re.Pattern[str]) -> tuple[str, int]:
    match = pattern.match(line)
    if not match:
        raise ValueError(f"Could not parse line: {line!r}")

    title = re.sub(r"\s+", " ", match.group(1)).strip().replace('"', '\\"')
    page = int(match.group(2)) + offset
    return title, page


def format_node(node: list, indent: int = 1) -> str:
    title, page, children = node
    pad = "  " * indent
    if not children:
        return f'{pad}("{title}" "#{page}")'

    child_lines = "\n".join(format_node(child, indent + 1) for child in children)
    return f'{pad}("{title}" "#{page}"\n{child_lines}\n{pad})'


def build_bookmarks(lines: list[str], offset: int) -> str:
    pattern = re.compile(r"^(.*?)(?:\s*(?:\.\s*){4,}|\s+)\s*(-?\d+)\s*$")

    stack: list[tuple[int, list]] = []
    roots: list[list] = []

    for raw_line in lines:
        if not raw_line.strip():
            continue

        level = get_tab_level(raw_line)
        cleaned = raw_line.strip()
        title, page = parse_line(cleaned, offset, pattern)
        node: list = [title, page, []]

        while stack and stack[-1][0] >= level:
            stack.pop()

        if stack:
            stack[-1][1][2].append(node)
        else:
            roots.append(node)

        stack.append((level, node))

    body = "\n".join(format_node(root, indent=1) for root in roots)
    return f"(bookmarks\n{body}\n)\n"


def main() -> None:
    base_dir = Path(__file__).resolve().parent
    input_path = base_dir / "outline.txt"
    output_path = base_dir / "outline2.txt"

    raw_lines = input_path.read_text(encoding="utf-8").splitlines()

    if not any(line.strip() for line in raw_lines):
        raise ValueError("outline.txt is empty.")

    offset = int(sys.argv[1]) if len(sys.argv) > 1 else 0

    result = build_bookmarks(raw_lines, offset)
    output_path.write_text(result, encoding="utf-8")


if __name__ == "__main__":
    main()
```

Finally:

`djvused 1.djvu -e 'set-outline outline2.txt' -s`
