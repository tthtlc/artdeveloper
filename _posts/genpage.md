
Got it. ✅
I’ll give you a **Python script** that:

1. Uses the **latest OpenAI Python SDK** (the `openai` package).
2. Queries the API with a **prompt** asking it to generate psychedelic HTML/JS code embedded in Markdown.
3. Saves the result to a filename in the format `YYYY-MM-DD-title_of_file.md`.

Here’s the script:

```python
import openai
from datetime import datetime
import random
import re

# Make sure you have installed the latest SDK:
# pip install openai

# Set your API key (use environment variable in real usage!)
openai.api_key = "YOUR_API_KEY_HERE"

def slugify_title(title, max_words=6):
    """Convert arbitrary title into safe filename slug."""
    # Remove non-word chars, lower case, and join first N words
    title = re.sub(r"[^\w\s-]", "", title).strip().lower()
    words = title.split()
    return "-".join(words[:max_words]) if words else "untitled"

def generate_filename():
    """Generate filename like YYYY-MM-DD-title_of_file.md"""
    today = datetime.now().strftime("%Y-%m-%d")
    # Arbitrary random title
    random_titles = [
        "psychedelic-art", "rainbow-chaos", "fractal-dreams",
        "cosmic-waves", "color-spirals", "acid-vision"
    ]
    title = random.choice(random_titles)
    return f"{today}-{slugify_title(title)}.md"

def query_openai():
    """Send a request to OpenAI to generate psychedelic HTML/JS webpage in Markdown."""
    prompt = """Generate a psychedelic HTML + JavaScript webpage that creates evolving colorful art.
    Return the answer in markdown fenced code block format, so it can be saved as a markdown file.
    The webpage should use <canvas> and JavaScript to animate psychedelic visuals.
    """

    response = openai.chat.completions.create(
        model="gpt-4.1",  # use latest available model
        messages=[
            {"role": "system", "content": "You are a code generator."},
            {"role": "user", "content": prompt}
        ]
    )

    return response.choices[0].message.content

def save_to_markdown(content, filename):
    with open(filename, "w", encoding="utf-8") as f:
        f.write(content)
    print(f"✅ Saved output to {filename}")

if __name__ == "__main__":
    filename = generate_filename()
    content = query_openai()
    save_to_markdown(content, filename)
```

---

### 🔍 How it works

* **`generate_filename()`** → Builds a date-based filename like `2025-09-30-psychedelic-art.md`.
* **`query_openai()`** → Sends a structured prompt to the latest `chat.completions` endpoint (`gpt-4.1`).
* **Markdown output** → The completion is expected to contain the webpage code inside fenced code blocks (` ```html ... ``` `).
* **File saved** → The result is stored in a `.md` file you can open in any Markdown viewer.

---

👉 Do you want me to also add a **section at the top of the Markdown file** (like metadata: title, date, description), so it looks like a proper blog-ready document (Jekyll/Hugo style)?

