## Markdown Image Parser

### The Challenge

Convert a Markdown image syntax string (`![alt text](url)`) into a valid HTML `<img>` tag. This requires extracting two distinct variables from a single string while maintaining strict HTML attribute ordering.

### Technical Strategy: Regex Capture Groups

Instead of destructive string manipulation, this solution utilizes **Non-Greedy Capture Groups** to pull the relevant data points directly from the source.

    1. **The Pattern**: `/!\[(.*?)\]\((.*?)\)/`

        -   `!\[` and `\]\(`: Escape characters used to identify the literal brackets and parenthesis that define Markdown syntax.

        -   `(.*?)`: A capture group that lazily matches any character. The first group captures the **alt text**, the second captures the **URL**.

    2.  **The Extraction**: Used `String.prototype.match()` to generate an array where index `1` and `2` correspond to the captured groups.

    3.  **Template Literals**: Injected the extracted values into a standard HTML string template.

### Key Code Snippet

```JavaScript

const regex = /!\[(.*?)\]\((.*?)\)/;
const match = markdown.match(regex);

if (match) {
    const [fullMatch, altText, imageUrl] = match;
    return `<img src="${imageUrl}" alt="${altText}">`;
}
```

### Lessons Learned

    -   **Escaping Characters**: Understood that characters like `[` and `(` have special meanings in Regex and must be "escaped" with a backslash `\` to be treated as a literal text.

    -   **Destructuring Arrays**: Used array indices from the `match` result to cleanly assign variables, a common pattern in data parsing.

    -   **HTML Consistency**: Focused on the specific requirements for attribute order and quotes, which is vital when generating code meant for browser rendering.
