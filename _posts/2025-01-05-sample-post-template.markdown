---
layout: single
title: "Sample Post Template"
date: 2025-01-05 21:00:00 -0800
categories: [tutorial, template]
tags: [jekyll, minimal-mistakes, blogging]
excerpt: "This is a template post showing various markdown features and front matter options for Minimal Mistakes theme."
header:
  # Uncomment and add path to use a header image
  # image: /assets/images/header-image.jpg
  # teaser: /assets/images/teaser-image.jpg
toc: true
toc_label: "Contents"
toc_icon: "cog"
---

This is a sample post template. You can copy this file to create new posts. Just remember to:
1. Use the naming format: `YYYY-MM-DD-title.markdown`
2. Update the date in the filename and front matter
3. Change the title, categories, tags, and content

## Front Matter Options

The section at the top between `---` marks is called "front matter". Here are common options:

- **layout**: Usually `single` for blog posts
- **title**: Your post title
- **date**: Post date and time
- **categories**: List of categories (e.g., `[android, tutorial]`)
- **tags**: List of tags for better organization
- **excerpt**: Short description shown in post lists
- **toc**: Set to `true` to show table of contents
- **header**: Add images to your post header

## Markdown Formatting

### Text Formatting

You can use **bold text**, *italic text*, or ***bold and italic***.

You can also use ~~strikethrough~~.

### Lists

Unordered list:
- Android development
- Web development
- Hardware projects
  - Arduino
  - Raspberry Pi
  - Drones

Numbered list:
1. Plan the project
2. Write the code
3. Test thoroughly
4. Deploy

### Code Blocks

Inline code: `npm install` or `bundle exec jekyll serve`

Code block with syntax highlighting:

```javascript
function greet(name) {
  console.log(`Hello, ${name}!`);
  return true;
}

greet('World');
```

```python
def calculate_fibonacci(n):
    if n <= 1:
        return n
    return calculate_fibonacci(n-1) + calculate_fibonacci(n-2)

print(calculate_fibonacci(10))
```

```kotlin
// Android/Kotlin example
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        Log.d("MainActivity", "App started")
    }
}
```

### Links

[Link to GitHub](https://github.com/HarrisonOg)

[Link with title](https://jekyllrb.com "Jekyll Documentation")

### Images

To add images, place them in an `assets/images/` directory and reference them:

```markdown
![Alt text](/assets/images/your-image.jpg)
```

Or with a caption:

```markdown
![Alt text](/assets/images/your-image.jpg)
*Image caption here*
```

### Blockquotes

> This is a blockquote. You can use it for highlighting important information
> or quoting someone.
>
> — Harrison Oglesby

### Tables

| Feature | Android | iOS | Web |
|---------|---------|-----|-----|
| Language | Kotlin/Java | Swift | JavaScript |
| Framework | Android SDK | UIKit | React/Next.js |
| Deployment | Play Store | App Store | Web Hosting |

### Task Lists

- [x] Install Minimal Mistakes theme
- [x] Configure navigation
- [x] Create About page
- [ ] Add first project post
- [ ] Create project portfolio section

## Notice Blocks

**Note**: Minimal Mistakes supports notice blocks for highlighting information.
{: .notice}

**Info**: This is an info notice block.
{: .notice--info}

**Warning**: Be careful with this approach!
{: .notice--warning}

**Success**: Everything worked perfectly!
{: .notice--success}

**Danger**: This could break things!
{: .notice--danger}

## Embedding Content

### YouTube Video

```html
{% raw %}
{% include video id="VIDEO_ID_HERE" provider="youtube" %}
{% endraw %}
```

### GitHub Gist

Since we have the jekyll-gist plugin:

```html
{% raw %}
{% gist USERNAME/GIST_ID %}
{% endraw %}
```

## Categories and Tags

Posts are organized by:
- **Categories**: Broad topics (e.g., Android, Web Development, Hardware)
- **Tags**: Specific keywords (e.g., kotlin, retrofit, arduino, drone)

You can have multiple categories and tags:

```yaml
categories: [android, tutorial]
tags: [kotlin, jetpack-compose, android-studio]
```

## Tips for Writing Posts

1. **Use descriptive titles**: Make it clear what the post is about
2. **Add an excerpt**: Write a compelling summary
3. **Include code examples**: Show, don't just tell
4. **Add images**: Visual content makes posts more engaging
5. **Use headings**: Break up long posts into sections
6. **Link to related content**: Help readers find more information

## Next Steps

After copying this template:
1. Rename the file with the current date and your topic
2. Update all front matter fields
3. Write your content
4. Save and run `bundle exec jekyll serve` to preview
5. Check the post at http://127.0.0.1:4000/posts/

Happy blogging! 🚀
