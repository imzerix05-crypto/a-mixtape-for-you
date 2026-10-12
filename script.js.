/* ==========================================
   A MIXTAPE FOR YOU ♡
   Interactive mixtape creator
========================================== */

const startButton = document.getElementById("startButton");

const state = {
  theme: "blush",
  stickers: [],
  songs: [],
  note: "",
  recipient: "Someone Special",
  sender: ""
};

const themes = [
  { id: "blush", name: "Blush Pink", color: "#f8cde5", accent: "#d97ba5" },
  { id: "lavender", name: "Lavender", color: "#ddd5fa", accent: "#9482d9" },
  { id: "blue", name: "Baby Blue", color: "#c7e5ef", accent: "#719fb4" },
  { id: "cream", name: "Vanilla Cream", color: "#fff0d5", accent: "#c49b65" },
  { id: "mint", name: "Soft Mint", color: "#d8eadb", accent: "#7ca888" },
  { id: "rose", name: "Dusty Rose", color: "#e8b7b9", accent: "#aa626d" }
];

const stickerOptions = [
  { id: "heart", emoji: "💌", name: "Love Letter" },
  { id: "flower", emoji: "🌼", name: "Flower" },
  { id: "ribbon", emoji: "🎀", name: "Ribbon" },
  { id: "star", emoji: "⭐", name: "Star" },
  { id: "sparkles", emoji: "✨", name: "Sparkles" },
  { id: "bear", emoji: "🧸", name: "Teddy Bear" },
  { id: "butterfly", emoji: "🦋", name: "Butterfly" },
  { id: "moon", emoji: "🌙", name: "Moon" }
];

let currentStep = 1;
let currentScreen;

function createStyles() {
  if (document.getElementById("mixtape-extra-styles")) return;

  const style = document.createElement("style");
  style.id = "mixtape-extra-styles";

  style.textContent = `
    .mixtape-builder {
      width: min(100%, 650px);
      margin: 24px auto;
      padding: 24px;
      border-radius: 24px;
      background: rgba(255,255,255,.86);
      box-shadow: 0 12px 45px rgba(130,70,100,.12);
      text-align: left;
      animation: mixtapeAppear .5s ease both;
    }

    .mixtape-builder h2 {
      font-family: 'Playfair Display', serif;
      text-align: center;
      font-size: clamp(23px, 5vw, 32px);
      margin: 0 0 10px;
    }

    .mixtape-builder p {
      line-height: 1.65;
      color: #795e6c;
    }

    .mixtape-progress {
      display: flex;
      justify-content: space-between;
      gap: 7px;
      margin-bottom: 25px;
    }

    .mixtape-progress span {
      flex: 1;
      text-align: center;
      padding: 9px 3px;
      background: #f8e7ef;
      border-radius: 30px;
      color: #91677b;
      font-size: 12px;
    }

    .mixtape-progress span.active {
      background: #d97ba5;
      color: white;
    }

    .cassette-preview {
      background: #f8f2ec;
      border: 5px solid rgba(255,255,255,.9);
      border-radius: 17px;
      padding: 20px 14px;
      box-shadow: 0 7px 18px rgba(70,40,50,.12);
      margin: 22px 0;
      transition: background .3s ease;
    }

    .cassette-preview-label {
      min-height: 110px;
      border-radius: 10px;
      padding: 14px;
      text-align: center;
      display: flex;
      flex-direction: column;
      justify-content: center;
      background: var(--tape-color, #f8cde5);
      color: #59414c;
    }

    .cassette-preview-label strong {
      font-family: 'Playfair Display', serif;
      font-size: 29px;
    }

    .cassette-preview-label small {
      letter-spacing: 2px;
      margin-top: 7px;
    }

    .theme-grid, .sticker-grid {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 10px;
      margin: 18px 0;
    }

    .theme-choice, .sticker-choice {
      border: 2px solid #f0e1e8;
      background: white;
      border-radius: 14px;
      padding: 12px 5px;
      cursor: pointer;
      color: #634c58;
      min-width: 0;
      font: inherit;
      transition: transform .2s, border-color .2s;
    }

    .theme-choice.selected, .sticker-choice.selected {
      border-color: #d97ba5;
      background: #fff5fa;
      transform: translateY(-2px);
    }

    .theme-swatch {
      width: 34px;
      height: 34px;
      border-radius: 50%;
      display: block;
      margin: 0 auto 8px;
      border: 2px solid rgba(0,0,0,.05);
    }

    .sticker-choice .emoji {
      display: block;
      font-size: 26px;
      margin-bottom: 5px;
    }

    .sticker-choice small, .theme-choice small {
      font-size: 11px;
    }

    .mixtape-field {
      width: 100%;
      box-sizing: border-box;
      padding: 13px 14px;
      margin: 8px 0 14px;
      border: 1px solid #e8d4df;
      border-radius: 12px;
      background: #fffdfd;
      color: #513e49;
      font: inherit;
    }

    .mixtape-field:focus {
      outline: 2px solid #e6a5c4;
      outline-offset: 2px;
    }

    .mixtape-label {
      display: block;
      font-weight: 700;
      font-size: 14px;
      color: #634c58;
      margin-top: 12px;
    }

    .mixtape-actions {
      display: flex;
      gap: 10px;
      margin-top: 24px;
    }

    .mixtape-actions button, .mixtape-primary {
      flex: 1;
      border: 0;
      border-radius: 12px;
      padding: 14px 12px;
      background: #d97ba5;
      color: white;
      font: inherit;
      font-weight: 700;
      cursor: pointer;
    }

    .mixtape-actions .secondary {
      background: white;
      border: 1px solid #e2c7d5;
      color: #795e6c;
    }

    .mixtape-primary:disabled {
      opacity: .45;
      cursor: not-allowed;
    }

    .song-list {
      display: grid;
      gap: 10px;
      margin: 16px 0;
    }

    .song-item {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 12px;
      border-radius: 12px;
      background: #fff5fa;
      overflow-wrap: anywhere;
    }

    .song-item .song-number {
      background: #f2d7e5;
      border-radius: 50%;
      min-width: 28px;
      height: 28px;
      display: grid;
      place-items: center;
    }

    .song-item .song-title {
      flex: 1;
      font-size: 13px;
    }

    .song-item button {
      border: 0;
      background: transparent;
      color: #a24d75;
      padding: 6px;
      cursor: pointer;
    }

    .mixtape-error {
      color: #a72c52 !important;
      font-size: 13px;
    }

    .mixtape-note-paper {
      padding: 18px;
      margin-top: 16px;
      border-radius: 8px;
      background: repeating-linear-gradient(
        to bottom,
        #fffdf8 0px,
        #fffdf8 31px,
        #d9dbe9 32px
      );
      border-left: 3px solid #e9a2b9;
    }

    .mixtape-note-paper textarea {
      min-height: 170px;
      resize: vertical;
      line-height: 32px;
      background: transparent;
      border: 0;
      margin: 0;
    }

    .mixtape-final {
      text-align: center;
    }

    .mixtape-final .final-heart {
      font-size: 45px;
      animation: mixtapeHeartbeat 1.6s infinite;
    }

    .mixtape-final .final-note {
      white-space: pre-wrap;
      overflow-wrap: anywhere;
      padding: 20px;
      border-radius: 15px;
      background: #fff7fa;
      text-align: left;
      line-height: 1.8;
    }

    .mixtape-final a {
      color: #a24d75;
      overflow-wrap: anywhere;
    }

    .mixtape-builder button:focus-visible {
      outline: 3px solid #a24d75;
      outline-offset: 3px;
    }

    @keyframes mixtapeAppear {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    @keyframes mixtapeHeartbeat {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.1); }
    }

    @media (max-width: 420px) {
      .mixtape-builder { padding: 17px; }
      .theme-grid, .sticker-grid { gap: 7px; }
      .theme-choice, .sticker-choice { padding: 10px 3px; }
    }
  `;

  document.head.appendChild(style);
}

function escapeHTML(value) {
  return String(value).replace(/[&<>"']/g, character => ({
    "&": "&amp;",
    "<": "&lt;",
    ">": "&gt;",
    '"': "&quot;",
    "'": "&#39;"
  })[character]);
}

function validYouTubeURL(value) {
  try {
    const url = new URL(value.trim());
    const host = url.hostname.toLowerCase().replace(/^www\./, "");

    if (host === "youtu.be") {
      return /^[a-zA-Z0-9_-]{11}$/.test(url.pathname.slice(1));
    }

    if (host === "youtube.com" || host === "m.youtube.com") {
      const id = url.searchParams.get("v");
      if (id && /^[a-zA-Z0-9_-]{11}$/.test(id)) return true;

      return /^\/(embed|shorts)\/[a-zA-Z0-9_-]{11}\/?$/.test(url.pathname);
    }

    return false;
  } catch {
    return false;
  }
}

function getYouTubeID(value) {
  const url = new URL(value);
  const host = url.hostname.toLowerCase().replace(/^www\./, "");

  if (host === "youtu.be") return url.pathname.slice(1);

  const queryID = url.searchParams.get("v");
  if (queryID) return queryID;

  return url.pathname.split("/")[2];
}

function createBuilder() {
  createStyles();

  const welcome = document.querySelector(".welcome-card");
  if (!welcome) return;

  welcome.style.display = "none";

  currentScreen = document.createElement("main");
  currentScreen.className = "mixtape-builder";
  currentScreen.setAttribute("aria-live", "polite");

  document.body.appendChild(currentScreen);

  renderStep();
  currentScreen.scrollIntoView({ behavior: "smooth", block: "start" });
}

function progressHTML() {
  const labels = ["Cassette", "Stickers", "Songs", "Your note"];

  return `
    <div class="mixtape-progress" aria-label="Creation progress">
      ${labels.map((label, index) => `
        <span class="${currentStep === index + 1 ? "active" : ""}">
          ${index + 1}. ${label}
        </span>
      `).join("")}
    </div>
  `;
}

function previewHTML() {
  const theme = themes.find(item => item.id === state.theme) || themes[0];

  return `
    <div class="cassette-preview" style="--tape-color:${theme.color}">
      <div class="cassette-preview-label">
        <small>♡ A LITTLE GIFT FOR YOU ♡</small>
        <strong>${escapeHTML(state.recipient || "mixtape")}</strong>
        <div style="font-size:25px;margin-top:9px">
          ${state.stickers.map(id => {
            const sticker = stickerOptions.find(item => item.id === id);
            return sticker ? sticker.emoji : "";
          }).join(" ")}
        </div>
        <small>${state.songs.length}/10 SONGS · MADE WITH LOVE</small>
      </div>
    </div>
  `;
}

function renderStep() {
  if (!currentScreen) return;

  const content = [
    renderThemeStep,
    renderStickerStep,
    renderSongsStep,
    renderNoteStep
  ][currentStep - 1]();

  currentScreen.innerHTML = `
    ${progressHTML()}
    <h2>${[
      "Choose your cassette ♡",
      "Decorate with love 🎀",
      "Add your favourite songs 🎧",
      "Write a little birthday note 💌"
    ][currentStep - 1]}</h2>
    ${previewHTML()}
    ${content}
  `;

  bindStepEvents();
}

function renderThemeStep() {
  return `
    <p>Choose the colours that feel just right. Your cassette will change as you explore.</p>

    <div class="theme-grid">
      ${themes.map(theme => `
        <button class="theme-choice ${state.theme === theme.id ? "selected" : ""}"
          data-theme="${theme.id}" aria-pressed="${state.theme === theme.id}">
          <span class="theme-swatch" style="background:${theme.color}"></span>
          <small>${theme.name}</small>
        </button>
      `).join("")}
    </div>

    <label class="mixtape-label" for="recipient">Who is this mixtape for?</label>
    <input class="mixtape-field" id="recipient" maxlength="50"
      placeholder="Someone special ♡" value="${escapeHTML(state.recipient === "Someone Special" ? "" : state.recipient)}">

    <div class="mixtape-actions">
      <button class="secondary" data-action="home">Back home</button>
      <button data-action="next">Next ♡</button>
    </div>
  `;
}

function renderStickerStep() {
  return `
    <p>Choose up to three little decorations for your cassette.</p>

    <div class="sticker-grid">
      ${stickerOptions.map(sticker => `
        <button class="sticker-choice ${state.stickers.includes(sticker.id) ? "selected" : ""}"
          data-sticker="${sticker.id}"
          aria-pressed="${state.stickers.includes(sticker.id)}">
          <span class="emoji">${sticker.emoji}</span>
          <small>${sticker.name}</small>
        </button>
      `).join("")}
    </div>

    <p>${state.stickers.length}/3 decorations selected</p>

    <div class="mixtape-actions">
      <button class="secondary" data-action="back">Back</button>
      <button data-action="next">Next ♡</button>
    </div>
  `;
}

function renderSongsStep() {
  return `
    <p>Add up to 10 YouTube songs. You can remove a song and replace it whenever you like.</p>

    <label class="mixtape-label" for="songTitle">Song title (optional)</label>
    <input class="mixtape-field" id="songTitle" maxlength="100"
      placeholder="e.g. A song that reminds me of you">

    <label class="mixtape-label" for="songURL">YouTube link</label>
    <input class="mixtape-field" id="songURL" type="url"
      placeholder="Paste a YouTube link here">

    <button class="mixtape-primary" id="addSong"
      ${state.songs.length >= 10 ? "disabled" : ""}>
      + Add song (${state.songs.length}/10)
    </button>

    <div id="songError" role="status"></div>

    <div class="song-list">
      ${state.songs.length ? state.songs.map((song, index) => `
        <div class="song-item">
          <span class="song-number">${index + 1}</span>
          <span class="song-title">
            <strong>${escapeHTML(song.title)}</strong><br>
            <small>YouTube song</small>
          </span>
          <button data-remove-song="${index}" aria-label="Remove ${escapeHTML(song.title)}">✕</button>
        </div>
      `).join("") : "<p>No songs added yet. Let's change that! ♡</p>"}
    </div>

    <div class="mixtape-actions">
      <button class="secondary" data-action="back">Back</button>
      <button data-action="next">Next ♡</button>
    </div>
  `;
}

function renderNoteStep() {
  return `
    <p>This is your chance to make their birthday a little more special.</p>

    <label class="mixtape-label" for="sender">Your name or nickname (optional)</label>
    <input class="mixtape-field" id="sender" maxlength="50"
      placeholder="With love, ..."
      value="${escapeHTML(state.sender)}">

    <label class="mixtape-label" for="birthdayNote">Your personal message</label>

    <div class="mixtape-note-paper">
      <textarea class="mixtape-field" id="birthdayNote" maxlength="1500"
        placeholder="Happy birthday, you special human... ♡">${escapeHTML(state.note)}</textarea>
    </div>

    <p id="noteCount">${state.note.length}/1500 characters</p>

    <div class="mixtape-actions">
      <button class="secondary" data-action="back">Back</button>
      <button data-action="finish">Finish mixtape 💌</button>
    </div>
  `;
}

function bindStepEvents() {
  currentScreen.querySelectorAll("[data-theme]").forEach(button => {
    button.addEventListener("click", () => {
      state.theme = button.dataset.theme;
      renderStep();
    });
  });

  currentScreen.querySelectorAll("[data-sticker]").forEach(button => {
    button.addEventListener("click", () => {
      const id = button.dataset.sticker;
      const index = state.stickers.indexOf(id);

      if (index >= 0) {
        state.stickers.splice(index, 1);
      } else if (state.stickers.length < 3) {
        state.stickers.push(id);
      } else {
        alert("You can choose up to 3 stickers, dude! 🎀");
        return;
      }

      renderStep();
    });
  });

  currentScreen.querySelectorAll("[data-action]").forEach(button => {
    button.addEventListener("click", () => {
      const action = button.dataset.action;

      if (action === "home") {
        currentScreen.remove();
        currentScreen = null;
        const welcome = document.querySelector(".welcome-card");
        if (welcome) welcome.style.display = "";
        welcome?.scrollIntoView({ behavior: "smooth" });
        return;
      }

      if (action === "back") {
        currentStep = Math.max(1, currentStep - 1);
        renderStep();
        return;
      }

      if (action === "next") {
        if (currentStep === 1) {
          const input = document.getElementById("recipient");
          state.recipient = input.value.trim() || "Someone Special";
        }

        currentStep = Math.min(4, currentStep + 1);
        renderStep();
        currentScreen.scrollIntoView({ behavior: "smooth", block: "start" });
        return;
      }

      if (action === "finish") {
        state.sender = document.getElementById("sender").value.trim();
        state.note = document.getElementById("birthdayNote").value.trim();
        renderFinalScreen();
      }
    });
  });

  const addSongButton = document.getElementById("addSong");

  if (addSongButton) {
    addSongButton.addEventListener("click", addSong);
  }

  currentScreen.querySelectorAll("[data-remove-song]").forEach(button => {
    button.addEventListener("click", () => {
      state.songs.splice(Number(button.dataset.removeSong), 1);
      renderStep();
    });
  });

  const note = document.getElementById("birthdayNote");

  if (note) {
    note.addEventListener("input", () => {
      document.getElementById("noteCount").textContent =
        `${note.value.length}/1500 characters`;
    });
  }
}

function addSong() {
  const titleInput = document.getElementById("songTitle");
  const urlInput = document.getElementById("songURL");
  const error = document.getElementById("songError");

  const url = urlInput.value.trim();
  const title = titleInput.value.trim();

  error.textContent = "";
  error.className = "";

  if (state.songs.length >= 10) {
    error.textContent = "Your mixtape already has 10 songs! ♡";
    error.className = "mixtape-error";
    return;
  }

  if (!validYouTubeURL(url)) {
    error.textContent = "Please paste a valid YouTube video link.";
    error.className = "mixtape-error";
    return;
  }

  const id = getYouTubeID(url);

  if (state.songs.some(song => song.id === id)) {
    error.textContent = "You've already added that song!";
    error.className = "mixtape-error";
    return;
  }

  state.songs.push({
    id,
    title: title || `Song ${state.songs.length + 1}`,
    url: `https://www.youtube.com/watch?v=${id}`
  });

  renderStep();
}

function renderFinalScreen() {
  const theme = themes.find(item => item.id === state.theme) || themes[0];

  currentScreen.innerHTML = `
    <div class="mixtape-final">
      <div class="final-heart">💌</div>
      <h2>A little piece of my heart ♡</h2>
      <p>Your mixtape for <strong>${escapeHTML(state.recipient)}</strong> is ready.</p>

      <div class="cassette-preview" style="--tape-color:${theme.color}">
        <div class="cassette-preview-label">
          <small>A LITTLE GIFT FOR YOU</small>
          <strong>${escapeHTML(state.recipient)}</strong>
          <div style="font-size:27px;margin:9px">
            ${state.stickers.map(id => {
              const sticker = stickerOptions.find(item => item.id === id);
              return sticker ? sticker.emoji : "";
            }).join(" ")}
          </div>
          <small>${state.songs.length} SONGS · MADE WITH LOVE ♡</small>
        </div>
      </div>

      <div class="final-note">${escapeHTML(state.note || "Wishing you a birthday filled with love, music, and beautiful memories. ♡")}
        ${state.sender ? `\n\nWith love,\n${escapeHTML(state.sender)}` : ""}
      </div>

      <h3>Your songs 🎧</h3>

      ${state.songs.length ? `
        <div class="song-list">
          ${state.songs.map((song, index) => `
            <div class="song-item">
              <span class="song-number">${index + 1}</span>
              <span class="song-title">${escapeHTML(song.title)}</span>
              <a href="${song.url}" target="_blank" rel="noopener noreferrer">Listen ↗</a>
            </div>
          `).join("")}
        </div>
      ` : "<p>Your mixtape is waiting for its soundtrack. ♡</p>"}

      <p>Made with a little extra love. 🎀</p>

      <div class="mixtape-actions">
        <button class="secondary" id="editMixtape">Edit mixtape</button>
        <button id="shareMixtape">Share note ♡</button>
      </div>

            <p id="shareStatus" role="status" aria-live="polite"></p>
    </div>
  `;

  // Edit the mixtape
  document.getElementById("editMixtape").addEventListener("click", () => {
    currentStep = 1;
    renderStep();
    currentScreen.scrollIntoView({
      behavior: "smooth",
      block: "start"
    });
  });

  // Share or copy the mixtape message
  document.getElementById("shareMixtape").addEventListener("click", async () => {
    const shareStatus = document.getElementById("shareStatus");

    const songsText = state.songs
      .map((song, index) => `${index + 1}. ${song.title}\n${song.url}`)
      .join("\n\n");

    const message = [
      `A little mixtape for ${state.recipient} ♡`,
      "",
      state.note || "Wishing you a birthday filled with love, music, and beautiful memories. ♡",
      state.sender ? `\nWith love,\n${state.sender}` : "",
      songsText ? `\n\nOur songs 🎧\n\n${songsText}` : ""
    ].join("\n");

    try {
      if (navigator.share) {
        await navigator.share({
          title: "A Mixtape for You ♡",
          text: message
        });

        shareStatus.textContent = "Your mixtape is ready to share! ♡";
      } else if (navigator.clipboard && window.isSecureContext) {
        await navigator.clipboard.writeText(message);

        shareStatus.textContent =
          "Your mixtape message has been copied! Send it to your special person. 💌";
      } else {
        const textarea = document.createElement("textarea");
        textarea.value = message;
        textarea.style.position = "fixed";
        textarea.style.opacity = "0";

        document.body.appendChild(textarea);
        textarea.select();

        const copied = document.execCommand("copy");
        textarea.remove();

        shareStatus.textContent = copied
          ? "Your mixtape message has been copied! ♡"
          : "Please copy your mixtape message manually.";
      }
    } catch (error) {
      if (error.name !== "AbortError") {
        shareStatus.textContent =
          "Couldn't open sharing. Please try again! ♡";
      }
    }
  });

  currentScreen.scrollIntoView({
    behavior: "smooth",
    block: "start"
  });
}

// Start creating the mixtape
if (startButton) {
  startButton.addEventListener("click", createBuilder);
}
