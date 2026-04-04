# How to Update the Communion Delivery Dashboard

Each month, follow these steps to update the dashboard with the new communion list.

---

## What You Need

- The new month's `.json` file (e.g. `may2026.json`)
- Terminal (already on your Mac)

---

## Step-by-Step

### 1. Name the JSON file correctly

The file must follow this naming pattern: **3-letter month + 4-digit year**, all lowercase.

Examples:
- `jan2026.json`
- `feb2026.json`
- `mar2026.json`
- `apr2026.json`
- `may2026.json`
- `jun2026.json`
- `jul2026.json`
- `aug2026.json`
- `sep2026.json`
- `oct2026.json`
- `nov2026.json`
- `dec2026.json`

### 2. Copy the file to the lists folder

Move or copy the JSON file into the `lists/` folder inside the project:

```
cp ~/Desktop/may2026.json ~/Desktop/nsbc-communion-delivery/lists/
```

Replace `may2026.json` with the actual file name for that month.

### 3. Open the project folder in Terminal

```
cd ~/Desktop/nsbc-communion-delivery
```

### 4. Add the new file to git

```
git add lists/may2026.json
```

Replace `may2026.json` with the actual file name.

### 5. Commit the change

```
git commit -m "Add May 2026 communion list"
```

Update the message to match the month.

### 6. Push to GitHub

```
git push
```

If git says you need to pull first, run:

```
git pull --rebase
```

Then run `git push` again.

### 7. Share the link

The dashboard link is always the same:

```
https://obsidianjuggernaut.github.io/nsbc-communion-delivery/
```

It automatically loads the current month's list. No need to change the link.

To share a specific month's list, add `?list=` with the file name (without `.json`):

```
https://obsidianjuggernaut.github.io/nsbc-communion-delivery/?list=apr2026
```

---

## Quick Reference (Copy-Paste Commands)

Replace `MONTH` with the file name (e.g. `may2026`):

```
cp ~/Desktop/MONTH.json ~/Desktop/nsbc-communion-delivery/lists/
cd ~/Desktop/nsbc-communion-delivery
git add lists/MONTH.json
git commit -m "Add MONTH communion list"
git push
```

---

## Dashboard Link

```
https://obsidianjuggernaut.github.io/nsbc-communion-delivery/
```

This link never changes. Share it once and it works every month.
