# Resume source

`resume.html` is the designed resume (same look as the site: Fraunces + Inter, bone/forest/copper).
Edit the HTML, then print it to the PDF the site serves:

```bash
PROF=/tmp/cprof-resume && rm -rf "$PROF" && "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless=new --disable-gpu --no-first-run --user-data-dir="$PROF" --virtual-time-budget=20000 \
  --no-pdf-header-footer --print-to-pdf="$PWD/Samara-Mehta-Resume.pdf" "file://$PWD/resume-src/resume.html"; pkill -f cprof-resume
```

Run it from the repo root. It must stay one page (the page clips overflow): check with a PDF viewer.
No phone number in it on purpose; the PDF is public.
