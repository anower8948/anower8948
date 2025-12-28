<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>anower8948 • GitHub README</title>

  <!-- Markdown renderer -->
  <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
  <!-- Sanitizer (recommended) -->
  <script src="https://cdn.jsdelivr.net/npm/dompurify@3.1.6/dist/purify.min.js"></script>

  <style>
    :root { color-scheme: light dark; }
    body {
      margin: 0;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji", "Segoe UI Emoji";
      line-height: 1.6;
    }
    header {
      padding: 18px 20px;
      border-bottom: 1px solid rgba(127,127,127,0.25);
      display: flex;
      gap: 12px;
      align-items: center;
      justify-content: space-between;
    }
    header a { text-decoration: none; }
    .wrap {
      max-width: 980px;
      margin: 0 auto;
      padding: 22px 18px;
    }
    .card {
      border: 1px solid rgba(127,127,127,0.25);
      border-radius: 14px;
      padding: 18px;
      overflow: hidden;
    }
    .muted { opacity: 0.75; font-size: 14px; }
    pre {
      overflow: auto;
      padding: 12px;
      border-radius: 10px;
      border: 1px solid rgba(127,127,127,0.25);
    }
    code { font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono", "Courier New", monospace; }
    img { max-width: 100%; height: auto; }
    blockquote {
      margin: 0;
      padding: 8px 12px;
      border-left: 4px solid rgba(127,127,127,0.35);
      opacity: 0.95;
    }
    .error {
      margin-top: 12px;
      padding: 12px;
      border-radius: 10px;
      border: 1px solid rgba(255,0,0,0.35);
    }
  </style>
</head>

<body>
  <header>
    <div>
      <strong>anower8948</strong>
      <span class="muted">• Profile README</span>
    </div>
    <nav class="muted">
      <a href="https://github.com/anower8948" target="_blank" rel="noreferrer">Profile</a>
      &nbsp;·&nbsp;
      <a href="https://github.com/anower8948/anower8948" target="_blank" rel="noreferrer">README Repo</a>
      &nbsp;·&nbsp;
      <a id="rawLink" href="#" target="_blank" rel="noreferrer">Raw</a>
    </nav>
  </header>

  <main class="wrap">
    <div class="card">
      <div id="status" class="muted">Loading README…</div>
      <article id="content"></article>

      <div id="err" class="error" style="display:none;"></div>
    </div>
  </main>

  <script>
    // ✅ Change branch here if you use "master" instead of "main"
    const user = "anower8948";
    const repo = "anower8948";
    const branch = "main";
    const path = "README.md";

    const rawUrl = `https://raw.githubusercontent.com/${user}/${repo}/${branch}/${path}`;
    document.getElementById("rawLink").href = rawUrl;

    // Configure marked
    marked.setOptions({
      breaks: true,
      gfm: true
    });

    function showError(message) {
      const err = document.getElementById("err");
      err.style.display = "block";
      err.textContent = message;
      document.getElementById("status").textContent = "Failed to load README.";
    }

    async function loadReadme() {
      try {
        const res = await fetch(rawUrl, { cache: "no-store" });
        if (!res.ok) throw new Error(`HTTP ${res.status} — ${res.statusText}`);

        const md = await res.text();

        const html = marked.parse(md);
        const safe = DOMPurify.sanitize(html);

        document.getElementById("content").innerHTML = safe;
        document.getElementById("status").textContent = `Loaded from ${rawUrl}`;
      } catch (e) {
        showError(
          `Could not fetch README from:\n${rawUrl}\n\n` +
          `Reason: ${e.message}\n\n` +
          `Tip: If your default branch is "master", change branch="master".`
        );
      }
    }

    loadReadme();
  </script>
</body>
</html>
