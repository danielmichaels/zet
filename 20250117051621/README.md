# Mermaid.js for Hugo blogs

Just implemented a mermaid.js shortcode in my Hugo blog.

All credit to:
<https://navendu.me/posts/adding-diagrams-to-your-hugo-blog-with-mermaid/>

This will only render on my Hugo blog and serves as a reference only.

ChatGPT generated this - I don't care if it makes sense its just a demo

{{< mermaid >}}

graph TD; A[Start] --> B{Is it raining?}; B -- Yes --> C[Take an umbrella]; B --
No --> D[Go outside]; C --> E[Proceed with your day]; D --> E;

{{< /mermaid >}}

Note: this isn't perfect and sometimes complex mermaid diagrams fail to render
when uploaded as a `zet`. WIP.

Tags:

#mermaid #hugo
