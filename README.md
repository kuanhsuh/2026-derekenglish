# Grade 4 Vocabulary Trainer

A mobile-first Astro vocabulary practice site for US Grade 4 readers. It works entirely in the browser: there is no login, database, paid API, or server-side user data.

## Run locally

```bash
npm install
npm run dev
```

For a production build:

```bash
npm run build
```

The deployable files are generated in `dist/`.

## Vocabulary data

All vocabulary lives in `src/data/vocabulary.json`. Add a word by adding one JSON object to the array:

```json
{
  "id": "curious",
  "word": "curious",
  "chinese": "好奇的",
  "definition": "wanting to learn more about something",
  "sentence": "The curious student asked a question.",
  "sentenceZh": "好奇的學生問了一個問題。",
  "grade": 4,
  "topic": "Science",
  "source": "Reading 2"
}
```

`id` must be unique and should use lowercase letters and hyphens. The new word will automatically appear in the word list, search, filters, learning flow, quiz selection, and the Reading Collection.

## Add a new reading

1. Add the reading's words to `src/data/vocabulary.json`.
2. Give every word the same `source`, for example `"source": "Reading 2 — Volcanoes"`.
3. Optionally give the words a shared `topic`, such as `"topic": "Earth Science"`.
4. Build or deploy. The Reading Collection groups the words by `source` automatically; no page changes are required.

## Progress and review

Progress is stored only in the device browser's `localStorage`, under `grade4-vocabulary-progress-v1`. It records correct/wrong counts, consecutive correct answers, last review date, and status.

- **New:** no quiz record
- **Learning:** being practiced
- **Review:** recently answered incorrectly
- **Mastered:** at least 5 correct answers and a streak of 3

Quiz selection gives extra weight to Review, New, and long-unreviewed words. Clearing browser site data resets progress; a different device has its own progress.

## Speech

The Listen buttons use the browser's built-in Web Speech `SpeechSynthesis` API. Voice quality and availability vary by browser/device; Chrome, Edge, Safari, and most modern mobile browsers support it.

## Deploy to Netlify

### Git method

1. Upload this project to a GitHub repository.
2. In Netlify, choose **Add new site → Import an existing project**.
3. Select the repository.
4. Netlify reads `netlify.toml` automatically. The build command is `npm run build` and publish directory is `dist`.
5. Click **Deploy site**.

### Drag-and-drop method

Run `npm run build`, then drag the generated `dist` folder into Netlify Drop.

Before deploying, update `site` in `astro.config.mjs` to your real Netlify URL if you later add canonical URLs or sharing metadata.
